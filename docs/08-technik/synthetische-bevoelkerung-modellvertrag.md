---
title: Technischer Modellvertrag – synthetische Bevölkerung
summary: Interner Vertrag für Datenmodell, Generator, Kalibrierung, Worker, IndexedDB, Aggregation, Szenarien, Performance und Tests.
status: Implementiert 0.7
last_updated: 2026-07-13
---

# Technischer Modellvertrag – synthetische Bevölkerung

## Architekturgrenze

Die Bevölkerungskomponente ist in folgende Schichten getrennt:

1. versionierte Datenverträge in `src/lib/types.ts`,
2. Baseline, Quellen, Generator, Raking, Validierung und Aggregation in `src/lib/population-model.ts`,
3. lokaler RPC-Worker in `src/workers/population.worker.ts`,
4. versionierte IndexedDB-Persistenz,
5. abstrahierter Zugriff über `LocalServerClient`,
6. React-Seiten für aggregierte Darstellung,
7. fachliche Integration in Einkommensteuer und Szenariozustand.

React-Komponenten erzeugen und gewichten keine Bevölkerung. Einzelpersonen und Haushalte werden nicht in den zentralen React-Zustand übertragen.

## Schema-Versionen

| Vertrag | Version |
|---|---:|
| Population-Schema | `1` |
| Population-Modell | `synthetic-population-0.7.0` |
| Szenario-JSON | `2` |
| lokale Population-IndexedDB | `1` |

Änderungen an Struktur, Interpretation oder Determinismus benötigen eine neue Modell- beziehungsweise Schema-Version. Gleicher Seed ist nur innerhalb derselben Baseline- und Modellversion reproduzierbar.

## Kerntypen

### `SyntheticPerson`

Pflichtfelder sind synthetische ID, Lauf- und Haushalts-ID, Alter, Altersgruppe, Haushaltsrolle, Erwerbs- und Arbeitszeitstatus, Einkommenskomponenten, sozialversicherungspflichtiges und steuerbares Einkommen, Gewicht, Bundesland, Gemeindetyp und Einkommensdezil.

### `SyntheticHousehold`

Pflichtfelder sind synthetische ID, Lauf-ID, Haushaltstyp, Erwachsene, Kinder, Kinderalter, Erwerbskonstellation, Brutto- und verfügbares Einkommen, Transfers, Wohnstatus, Miete beziehungsweise Wohnkosten, Vermögen, Schulden, Region und Gewicht.

### `PopulationRunMetadata`

Der Vertrag enthält Lauf-ID, Schema- und Modellversion, Seed, Erstellungszeitpunkt, Daten- und Rechtsstand, Baseline, Quellen-IDs, Stichprobengröße, gewichtete Summen, Kalibrierungsverfahren, Qualitätsmetriken, Einschränkungen und Aktivstatus.

### `CalibrationEntry`

Jede Zeile enthält Dimension, Kategorie, Ziel, Modellwert, absolute und relative Abweichung, Toleranz, Status, Quellen-ID und Einheit.

### `PopulationValidationIssue`

Validierungen liefern Code, Schweregrad, Entitätstyp, optionale Entitäts-ID und verständliche Meldung. Fehler dürfen nicht ausschließlich geloggt werden.

## Generatorvertrag

Eingabe:

```text
PopulationGenerationOptions {
  seed: string
  sampleSize: number
  baselineId: string
}
```

Ausgabe:

```text
{
  run: PopulationRun
  households: SyntheticHousehold[]
  persons: SyntheticPerson[]
}
```

Der Generator verwendet einen projektinternen deterministischen PRNG. Die Lauf-ID wird aus Seed, Stichprobengröße, Baseline und Modellversion abgeleitet. Für dieselben Eingaben bleiben Mikrodaten und Zusammenfassungen stabil; der Erstellungszeitpunkt ist reine Laufmetadaten-Provenienz.

Die letzte erzeugte Haushaltsstruktur wird an die noch offene Personenzahl angepasst. Dadurch entspricht die tatsächliche Stichprobengröße exakt der angeforderten und zulässigen Größe.

Zulässige Stichprobengrößen werden browserseitig auf 500 bis 50.000 Personen begrenzt. Die UI bietet 2.000, 5.000, 10.000, 25.000 und 50.000 an. Standard sind 10.000 Personen.

## Kalibrierungsvertrag

Das Raking setzt zunächst konstante Gewichte und passt diese in **40 Iterationen** nacheinander an die Zielmargen an. Personen- und Haushaltsgewichte werden getrennt kalibriert.

Personendimensionen:

- Altersgruppe,
- Erwerbsstatus,
- Bundesland,
- Gemeindetyp.

Die Einkommensdezile werden anschließend anhand der kalibrierten Personengewichte als gewichtete Quantile gebildet und separat berichtet.

Haushaltsdimensionen:

- Haushaltstyp,
- Bundesland,
- Gemeindetyp,
- Wohnstatus,
- Haushaltsgröße,
- Kinderzahl.

Nach dem letzten Durchlauf werden die Gewichte auf das dokumentierte Gesamtziel normiert. Die Berichtslogik berechnet Ziel, Ist, absolute und relative Abweichung. Der Laufstatus ist `warnung`, sobald mindestens eine Kategorie ihre Toleranz überschreitet.

Die implementierten relativen Toleranzen liegen dimensionsabhängig zwischen 2 und 4 Prozent:

- 2 Prozent für Altersgruppen,
- 3 Prozent für Haushaltstyp, Erwerbsstatus, Einkommensdezile, Bundesländer, Gemeindetyp und Wohnen,
- 4 Prozent für Haushaltsgröße und Kinderzahl.

Die Implementierung darf nicht behaupten, dass Raking alle gemeinsamen Verteilungen identifiziert.

## Validierungsvertrag

Mindestens geprüft werden:

- positive endliche Personen- und Haushaltsgewichte,
- Alter von 0 bis 110,
- vorhandene Haushaltsreferenz,
- konsistente Erwachsenen- und Kinderzahl,
- genau ein erwachsener Elternteil bei Alleinerziehenden,
- plausible Rentnerhaushalte,
- Erwerbseinkommen passend zum Erwerbsstatus,
- keine normale Miete bei Eigentum,
- nichtnegative Vermögen und Schulden,
- plausible steuerbare Einkommen,
- gewichtete Gesamtziele,
- vollständige IDs und endliche Zahlen.

Ein Generationslauf darf gespeichert werden, wenn nur Warnungen vorliegen. Fehler werden im Lauf gespeichert und in der Zusammenfassung gezählt; fachliche Verbraucher müssen diesen Status berücksichtigen.

## Aggregationsvertrag

`PopulationQuery` definiert:

- Entität: Personen oder Haushalte,
- Gruppierung,
- Maß: Anzahl, Anteil, Summe, Mittelwert oder Median,
- optionales numerisches Feld.

Unterstützte Gruppen sind Altersgruppe, Haushaltstyp, Einkommensdezil, Erwerbsstatus, Bundesland, Gemeindetyp, Wohnstatus und Transferbezug.

Alle Maße verwenden Gewichte. Der Median ist ein gewichteter Stichprobenmedian. Einzelne Fachseiten dürfen keine alternative Gewichtungslogik implementieren.

## Worker-Protokoll

Der Population-Worker unterstützt:

- `population:generate`
- `population:get-active`
- `population:list-runs`
- `population:activate`
- `population:get-summary`
- `population:get-calibration`
- `population:query`
- `population:delete-run`
- `population:income-tax`

Jede Nachricht besitzt eine Request-ID. Erfolgsantworten enthalten `ok: true` und Daten; Fehler enthalten `ok: false` und eine verständliche Meldung.

Der `LocalServerClient` kapselt den Worker. Eine spätere HTTP- oder RPC-Implementierung muss dieselben fachlichen Methoden anbieten, nicht dieselbe Browsertechnik.

## IndexedDB

Datenbank: `de-sim-population-server`

Version: `1`

Stores:

| Store | Inhalt | Schlüssel/Index |
|---|---|---|
| `population-runs` | Laufmetadaten, Zusammenfassung, Bericht | `metadata.id` |
| `population-persons` | synthetische Personen | `id`, Index `runId` |
| `population-households` | synthetische Haushalte | `id`, Index `runId` |
| `population-calibration` | Kalibrierungszeilen | `storageId`, Index `runId` |
| `population-validation` | Fehler und Warnungen | `storageId`, Index `runId` |
| `population-settings` | aktive Lauf-ID | `id` |

Eine Schemaerweiterung erhöht `DB_VERSION` und legt fehlende Stores beziehungsweise Indizes in `onupgradeneeded` an. Migrationen dürfen keine direkten IndexedDB-Zugriffe in React einführen.

Die Generierung ersetzt einen vorhandenen Lauf mit derselben deterministischen ID nach dem Löschen seiner Detaildaten. Nach erfolgreicher Speicherung wird der Lauf aktiviert. Beim Löschen des aktiven Laufs wird ein verbleibender Lauf gewählt; fehlt einer, wird beim nächsten Zugriff der Standardlauf erzeugt.

## Szenariointegration

`ScenarioDraft` enthält ausschließlich:

```text
populationRunId: string | null
populationModelVersion: string | null
```

Personen und Haushalte sind niemals Teil der Undo-/Redo-Historie oder des JSON-Exports. Schema 2 exportiert die Referenz; Schema 1 bleibt importierbar und wird normalisiert.

Bei fehlender lokaler Referenz zeigt die Anwendung einen Fehler. Sie darf nicht still einen anderen Lauf als fachlich gleichwertig behandeln. Zulässige Nutzeraktionen sind vorhandenen Lauf aktivieren oder neu erzeugen.

## Einkommensteuerintegration

Die Tariffunktionen bleiben in `income-tax.ts`. Der Population-Worker gruppiert Erwachsene zu Steuerhaushalten, berechnet gesetzliche und reformierte tarifliche Steuer und aggregiert mit Haushaltsgewichten.

Das Ergebnis enthält zusätzlich Lauf-ID, Stichprobengröße, gewichtete Bevölkerung, Datenstand und Kalibrierungsstatus. Die bisherige 50-Zellen-Referenzpopulation bleibt als expliziter Fallback und Regressionstest erhalten, ist bei vorhandenem Lauf aber nicht die primäre sichtbare Verteilungsbasis.

## Performancekonzept

- Erzeugung, Raking, Validierung, Speicherung und Steueraggregation laufen im Worker.
- React erhält Laufmetadaten, Zusammenfassungen und Kalibrierungszeilen.
- Große Personen- und Haushaltsarrays verbleiben im Worker beziehungsweise IndexedDB.
- Abfragen liefern gruppierte Ergebnisse statt vollständiger Datensätze.
- Standard sind 10.000 Personen; 50.000 ist die angebotene Obergrenze.
- Speicherbedarf und Laufzeit hängen von Browser, Gerät und Anzahl gespeicherter Läufe ab.
- Fehler dürfen den Hauptthread nicht blockieren; der letzte bedienbare UI-Zustand bleibt erhalten.

Gemessene Entwicklungswerte sind erst nach stabiler CI- und Browsermessung in die öffentliche Dokumentation aufzunehmen. Vorher werden keine exakten Laufzeitversprechen gemacht.

## Testvertrag

Modultests prüfen mindestens:

- PRNG-Sequenzen,
- identischen und abweichenden Seed,
- Haushalts- und Personenverknüpfung,
- positive Gewichte und Zielaggregate,
- Kalibrierungsmetriken,
- strukturierte Validierung,
- gruppierte Anzahl und gewichteten Median,
- Einkommensteuerintegration.

Playwright prüft mindestens:

- Navigation und Standardlauf,
- Seed und Generierung,
- reproduzierbare Zusammenfassung,
- neuen Lauf bei anderem Seed,
- Summen und Verteilungen,
- Kalibrierungstabelle,
- Aktivierung und Löschung,
- IndexedDB-Wiederherstellung,
- Einkommensteuer-Verteilungswirkung,
- Quellen-Drawer,
- Desktop und Mobil,
- Screenshot `test-results/milestone-7-synthetic-population.png`.

## Spätere Servermigration

Für einen echten Server bleiben UI und fachliche Verträge stabil. Ausgetauscht werden:

- Worker-Transport gegen HTTP/RPC,
- IndexedDB-Repository gegen serverseitige Persistenz,
- lokale Generierung gegen einen versionierten Job,
- lokale Laufaktivierung gegen eine Szenario-/Benutzerreferenz.

Nicht verändert werden sollen `PopulationGenerationOptions`, Laufmetadaten, Kalibrierungsbericht, Aggregationsvertrag und Szenarioreferenz, sofern keine fachliche Schemaänderung erforderlich ist.
