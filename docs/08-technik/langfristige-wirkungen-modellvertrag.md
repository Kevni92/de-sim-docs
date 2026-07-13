---
title: Technischer Modellvertrag – langfristige Wirkungen
summary: Interner Vertrag für Wirkungsregister, Berechnung, Worker, Persistenz, Szenariomigration und Tests.
status: Implementiert 0.8
last_updated: 2026-07-13
---

# Technischer Modellvertrag – langfristige Wirkungen

> Diese Seite ist eine interne Entwicklungsunterlage und durch `exclude_docs` von der öffentlichen Website ausgeschlossen.

## Architekturgrenze

Die Wirkungs-Engine ist in folgende Schichten getrennt:

1. versionierte Verträge in `src/lib/effect-contracts.ts`,
2. Modulregister und Evidenzdaten,
3. reine Zeitpfad- und Unsicherheitsberechnung,
4. Bevölkerungsauswahl und gewichtete Aggregation,
5. dedizierter Web Worker,
6. versionierte IndexedDB-Persistenz,
7. `LocalServerClient` als austauschbare Servergrenze,
8. React-Seite ohne Fachberechnung.

Zeitreihen- und Populationsberechnungen laufen vollständig im Worker. React-Komponenten greifen weder direkt auf IndexedDB noch auf vollständige Personen- oder Haushaltsarrays zu.

## Versionen

| Vertrag | Version |
|---|---:|
| Wirkungsmodell | `long-term-effects-0.8.0` |
| Szenario-JSON | `3` |
| Wirkungs-IndexedDB | `1` |
| Bevölkerung | `synthetic-population-0.7.0` |

Schema 1 und 2 bleiben importierbar und werden normalisiert. Schema 3 ergänzt zentral gespeicherte Wirkungsparameter.

## Modulvertrag

Ein Wirkungsmodul enthält mindestens:

- Modul-ID, Titel und Beschreibung,
- Kategorie und Status,
- Modellversion, Datenstand und Rechtsstand,
- Zeithorizont und unterstützte Modellstufen,
- Eingangsparameter und Zielpopulation,
- direkte und indirekte Wirkung,
- Zeitfunktion und Unsicherheitsmodell,
- Evidenz- und Quellen-IDs,
- bekannte Grenzen,
- Abhängigkeiten und Rückkopplungen.

Module dürfen keine UI-Abhängigkeiten besitzen.

## Parametervertrag

Jeder Parameter enthält ID, Bezeichnung, Beschreibung, Einheit, Baseline, Minimum, Maximum, Schrittweite, Standardwert, Status, Quelle, Unsicherheit, Sensitivität und fachliche Begründung.

Die zentrale Szenarionormalisierung entfernt unbekannte oder nicht endliche Werte und ergänzt fehlende Standardparameter. Undo, Redo, Autosave, Speichern, Duplizieren sowie JSON-Import und -Export verwenden denselben normalisierten Zustand.

## Ergebnisvertrag

Ein Ergebnis enthält:

- Modul-ID und Zeitraum,
- direkte, indirekte und gesamte Wirkung,
- Untergrenze, Zentralwert und Obergrenze,
- betroffene Personen und Haushalte,
- monetäre und nicht monetäre Wirkungen,
- Zielgruppen,
- Evidenzstatus und Kausalitätseinordnung,
- Warnungen und verwendete Annahmen,
- Modellversion, Bevölkerungslauf-ID und Szenario-ID.

Nicht berechnete Module liefern keinen künstlichen Zentralwert. Stattdessen enthalten sie Status, Begründung, Grenzen und gegebenenfalls qualitative Richtung.

## Zeitreihenvertrag

Jeder Punkt enthält Periode, Baseline, Szenariowert, direkte Wirkung, indirekte Wirkung, Rückkopplung, Untergrenze und Obergrenze.

Zeitfunktionen müssen Wirkungsbeginn, Anlaufzeit, Maximum, Abklingen und temporären oder permanenten Charakter explizit beschreiben. Rundung erfolgt erst für die Darstellung, nicht innerhalb der Kernberechnung.

## Bevölkerungsauswahl

Die Engine referenziert einen aktiven Bevölkerungslauf. Zielgruppen werden im Worker aus gewichteten Personen und Haushalten ausgewählt. Für das Kita-Modul sind insbesondere Kinderalter, Haushaltsform, Erwerbskonstellation, Arbeitszeitstatus und Einkommensdezil relevant.

Ein fehlender Bevölkerungslauf ist ein sichtbarer Fehler. Die Engine darf nicht still auf einen anderen Lauf wechseln.

## Unsicherheit

Unsicherheit wird als deterministisches Szenarioband berechnet. Die aktuelle Version führt keine stochastische Monte-Carlo-Simulation aus. Unter- und Obergrenzen ergeben sich aus dokumentierten Parameterräumen und modulspezifischen Bandfaktoren.

Breitere Horizonte und schwächere Evidenz müssen mindestens gleich breite oder breitere Intervalle erzeugen. Untergrenze, Zentralwert und Obergrenze dürfen nicht vertauscht sein.

## Rückkopplungen und Überlappungen

Rückkopplungen sind explizite Kanten zwischen Modulen. Sie werden nur einmal aggregiert. Module deklarieren Abhängigkeiten, damit Arbeitsvolumen, Steuer- und Beitragswirkung oder Produktivität nicht mehrfach vollständig addiert werden.

Die Aggregation erzeugt Warnungen, wenn überlappende Pfade nicht vollständig aufgelöst werden können.

## Worker-Protokoll

Der Wirkungs-Worker unterstützt mindestens:

- `effects:list-modules`,
- `effects:calculate`,
- `effects:get-run`,
- `effects:list-runs`,
- `effects:delete-run`.

Jede Nachricht enthält eine Request-ID. Erfolgsantworten verwenden `ok: true`; Fehler liefern `ok: false` und eine verständliche Meldung.

## IndexedDB

Datenbank: `de-sim-effects-server`

Version: `1`

Stores:

| Store | Inhalt |
|---|---|
| `effect-runs` | Laufmetadaten, Modulresultate und Zeitreihen |
| `effect-settings` | aktive Laufreferenz und Schemaeinstellungen |

Direkte Zugriffe außerhalb des Worker-/Server-Layers sind unzulässig.

## Tests

Modultests prüfen mindestens:

- statische Stufe ohne indirekte Wirkung,
- monotone Zeitpfade innerhalb definierter Grenzen,
- geordnete Unsicherheitsintervalle,
- gewichtete Kita-Zielgruppen,
- bewusste Nichtberechnung schwach belegter Module,
- Szenariomigration von Schema 1 und 2 auf Schema 3.

Playwright prüft mindestens:

- Aufruf der Route `/wirkungen`,
- sichtbaren Prognosehinweis,
- Modellstufen und Zeithorizonte,
- Zeitreihentabelle und Unsicherheitsband,
- nicht berechnete Demografiemodule,
- Desktop- und Mobilansicht,
- Screenshot `test-results/milestone-8-long-term-effects.png`.

## Spätere Servermigration

Ein späterer Server ersetzt Transport und Persistenz. Stabil bleiben sollen Modul-, Parameter-, Ergebnis- und Zeitreihenverträge sowie die Methoden des `LocalServerClient`.
