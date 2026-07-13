---
title: Synthetische Bevölkerung und Haushalte
summary: Fachliche Beschreibung der vollständig synthetischen Modellbevölkerung, ihrer Merkmale, Erzeugung, Kalibrierung, Gewichtung und Grenzen.
status: Implementiert 0.7
last_updated: 2026-07-13
---

# Synthetische Bevölkerung und Haushalte

## Ziel und Abgrenzung

Der HaushaltsKompass verwendet seit Milestone 7 eine gemeinsame, gewichtete und vollständig synthetische Bevölkerung als Datenbasis für Verteilungs-, Reichweiten- und Einkommensteuerberechnungen. Die Datensätze bilden statistische Randverteilungen und fachlich plausible Zusammenhänge ab, enthalten aber **keine echten Personen und keine kopierten amtlichen Mikrodaten**.

Ein synthetischer Datensatz repräsentiert über sein Gewicht viele vergleichbare Personen oder Haushalte. Die Standardstichprobe umfasst rund 10.000 synthetische Personen. Sie ist groß genug für Gruppen- und Dezilauswertungen, bleibt aber im Browser-Worker handhabbar.

Nicht Bestandteil sind:

- eine dynamische Demografie mit Geburten und Sterbefällen,
- kausale Verhaltens- oder Langfristprognosen,
- eine vollständige Regionalisierung unterhalb der Bundesländer,
- individuelle Steuer-, Beitrags- oder Leistungsberatung,
- eine perfekte multivariate Repräsentation aller Merkmalskombinationen.

## Vollständige Synthetizität und Datenschutz

Erzeugt und gespeichert werden keine Namen, Adressen, vollständigen Geburtsdaten, Arbeitgeber, Kontodaten oder anderen identifizierenden Merkmale. Die IDs von Personen und Haushalten sind rein synthetisch und nur innerhalb eines Generationslaufs gültig.

Amtliche oder wissenschaftliche Quellen liefern ausschließlich Randziele, Definitionen und Plausibilitätsrahmen. Der Generator rekonstruiert daraus keine realen Einzelfälle. Auch bei identischem Seed entsteht keine reale Person, sondern nur dieselbe reproduzierbare Modellstichprobe.

## Datenmodell

### Synthetische Person

Eine Person enthält mindestens:

- synthetische Personen- und Haushalts-ID,
- Alter und Altersgruppe,
- Rolle im Haushalt,
- Erwerbs- und Arbeitszeitstatus,
- Bruttoerwerbseinkommen,
- weitere steuerbare Einkommen,
- Renten- oder Pensionseinkommen,
- Transferbezug,
- sozialversicherungspflichtiges Einkommen,
- steuerlich relevantes Einkommen,
- Gewicht,
- Bundesland,
- Stadt-Land-Kategorie,
- modelliertes Einkommensdezil.

### Synthetischer Haushalt

Ein Haushalt enthält mindestens:

- synthetische Haushalts-ID,
- Haushaltstyp,
- Zahl der Erwachsenen und Kinder,
- Altersstruktur der Kinder,
- Erwerbskonstellation,
- Brutto- und verfügbares Einkommen,
- Transferkomponenten,
- Miete oder Eigentum,
- Bruttokaltmiete beziehungsweise Wohnkosten,
- Vermögen und Schulden,
- Bundesland und Stadt-Land-Kategorie,
- Haushaltsgewicht.

Unterstützt werden alleinlebende Personen, Paare ohne Kinder, Paare mit Kindern, Alleinerziehende, Mehrpersonenhaushalte und Rentnerhaushalte.

### Generationslauf

Jeder Lauf dokumentiert:

- Lauf-ID, Schema- und Modellversion,
- expliziten Seed,
- Erstellungszeitpunkt,
- Daten- und Rechtsstand,
- Baseline- und Quellen-IDs,
- Ziel- und tatsächliche Stichprobengröße,
- gewichtete Bevölkerung und Haushaltszahl,
- Kalibrierungsverfahren,
- Qualitätsmetriken,
- bekannte Einschränkungen.

## Deterministische Erzeugung

Die Erzeugung nutzt einen eigenen deterministischen Pseudozufallszahlengenerator. `Math.random()` ist nicht Bestandteil des fachlichen Generators.

Gleicher Seed, gleiche Baseline, gleiche Stichprobengröße und gleiche Modellversion erzeugen dieselben synthetischen Personen, Haushalte und Zusammenfassungen. Ein anderer Seed verändert die Mikrodaten, während kalibrierte Randverteilungen innerhalb der dokumentierten Toleranzen bleiben sollen.

Der Nutzer kann Seed und Stichprobengröße steuern sowie einen Lauf neu erzeugen, aktivieren oder löschen. Die Generierung und Aggregation laufen im Web Worker und blockieren nicht den React-Hauptthread.

## Datenquellen und Modellstatus

Die Baseline verbindet mehrere Ausgangspunkte:

| Bereich | Ausgangspunkt | Status in der Anwendung |
|---|---|---|
| Bevölkerung und Alter | Destatis Bevölkerungsfortschreibung | amtliches Randziel |
| Haushalte, Erwerb und Wohnen | Destatis Mikrozensus | amtliches Randziel beziehungsweise gerundete Projektbaseline |
| Einkommen und Konsum | EVS und SOEP als methodische Ausgangspunkte | modellierte gemeinsame Verteilung |
| Vermögen und Schulden | Bundesbank PHF | vorsichtig modellierte Verteilung |
| Bundesländer | amtliche Bevölkerungsstatistik | amtliches Randziel |
| Stadt-Land-Kategorie | verdichtete Projektbaseline | Modellannahme |
| gemeinsame Merkmalsabhängigkeiten | HaushaltsKompass-Generator | Modell |

Keine modellierte Größe wird als amtlicher Einzelwert ausgegeben. Quellen- und Modellstatus sind im Nachweis-Drawer sichtbar.

## Erzeugungsverfahren

Der Generator arbeitet in mehreren Schritten:

1. Seed und Baseline werden zu einem stabilen Zufallszustand kombiniert.
2. Haushaltstyp, Region, Gemeindetyp und Wohnstatus werden gezogen.
3. Erwachsene und Kinder werden mit konsistenter Haushaltsstruktur erzeugt.
4. Alter, Erwerbsstatus, Arbeitszeit und Einkommen werden regelbasiert verknüpft.
5. Wohnkosten, Vermögen und Schulden werden aus vorsichtig begrenzten Modellverteilungen abgeleitet.
6. Personen werden Einkommensdezilen zugeordnet.
7. Personen- und Haushaltsgewichte werden kalibriert.
8. Konsistenzregeln, Zusammenfassungen und Qualitätsmetriken werden berechnet.

Die gemeinsame Verteilung ist eine Modellkonstruktion. Sie ist keine Kopie einer Mehrzweck-Haushaltsbefragung.

## Kalibrierung und Gewichtung

Die Gewichte werden durch iteratives proportionales Anpassen, auch Raking genannt, an mehrere Randverteilungen angepasst. Die Implementierung verwendet 40 aufeinanderfolgende Anpassungsrunden. Kalibriert werden mindestens:

- Altersgruppen,
- Haushaltstypen,
- Haushaltsgrößen,
- Erwerbsstatus,
- Einkommensdezile,
- Kinderzahl,
- Bundesländer,
- Stadt-Land-Kategorie,
- Miete und Eigentum.

Jede Kategorie erhält Zielwert, synthetischen Istwert, absolute und relative Abweichung, Toleranz, Status und Quellen-ID. Die Toleranzen liegen dimensionsabhängig zwischen 2 und 4 Prozent relativer Abweichung. Überschreitungen werden als Warnung sichtbar hervorgehoben und nicht verborgen.

Raking trifft Randverteilungen, aber nicht automatisch alle mehrdimensionalen Abhängigkeiten. Aus einer guten Alters- und Einkommenskalibrierung folgt daher nicht, dass jede Kombination aus Alter, Haushaltstyp, Region und Einkommen repräsentativ ist.

## Qualitätsmetriken und Validierung

Automatisch geprüft werden unter anderem:

- endliche und positive Gewichte,
- zulässige Alterswerte,
- vorhandene Haushaltsreferenzen,
- Übereinstimmung von Haushaltsgröße und Personenzahl,
- genau ein erwachsener Elternteil bei Alleinerziehenden,
- plausible Altersstruktur von Rentnerhaushalten,
- Verhältnis von Erwerbsstatus und Erwerbseinkommen,
- keine normale Mietausgabe bei Eigentum,
- nichtnegative Vermögen und Schulden,
- plausible Beziehung von Brutto- und steuerbarem Einkommen,
- dokumentierte gewichtete Gesamtsummen,
- vollständige IDs und keine nicht endlichen Zahlen.

Fehler und Warnungen werden strukturiert gespeichert. Sie erscheinen in den Qualitätskennzahlen und nicht nur in der Browserkonsole.

## Aggregationen

Die gemeinsame Abfrageschicht unterstützt gewichtete Auswertungen nach:

- Alter und Altersgruppe,
- Haushaltstyp,
- Einkommensdezil,
- Erwerbsstatus,
- Bundesland,
- Gemeindetyp,
- Miet- und Eigentumsstatus,
- Transferbezug.

Verfügbar sind gewichtete Anzahl, Anteil, Summe, Mittelwert, gewichteter Median und gruppierte Verteilungen. Fachseiten sollen diese Schicht verwenden und keine eigene Gewichtungslogik duplizieren.

## Verwendung in der Einkommensteuer

Die gesetzliche Tarifberechnung nach § 32a EStG bleibt unverändert. Der aktive Bevölkerungslauf liefert die gewichteten Steuerfälle für:

- modelliertes Steueraufkommen,
- Gewinner und Verlierer,
- Wirkung nach Einkommensdezilen,
- gewichteten Median der monatlichen Wirkung,
- Zahl beziehungsweise Gewicht betroffener Haushalte.

Die sichtbare Einkommensteuerseite nennt Lauf-ID, Stichprobengröße, gewichtete Bevölkerung, Datenstand, Modellversion und Kalibrierungsstatus. Verständliche Referenzhaushalte bleiben als Tarifbeispiele erhalten; sie werden nicht mit der aktiven synthetischen Mikrostichprobe verwechselt.

Ist ein in einem Szenario referenzierter Lauf lokal nicht vorhanden, zeigt die Anwendung einen Fehler und fordert zur Auswahl oder Neugenerierung auf. Sie ersetzt die Referenz nicht stillschweigend durch einen anderen Lauf.

## Lokale Speicherung und Szenarien

Personen, Haushalte, Laufmetadaten, Kalibrierungsbericht und Validierung liegen in getrennten versionierten IndexedDB-Stores. Der aktive Lauf wird über eine stabile Lauf-ID und Modellversion im Szenario gespeichert. Undo und Redo kopieren keine Personendatensätze, sondern nur diese Referenz und die Konfiguration.

JSON-Export und -Import enthalten die Laufreferenz. Sämtliche Daten verbleiben lokal im Browser; Milestone 7 benötigt keinen externen Server und keine Benutzerkonten.

## Interpretation und bekannte Grenzen

Die synthetische Bevölkerung ist geeignet, um Modellwirkungen konsistent nach Gruppen zu vergleichen. Sie ist nicht geeignet, um:

- Aussagen über konkrete Personen oder kleine Orte zu treffen,
- seltene Merkmalskombinationen als exakt repräsentativ zu behandeln,
- Vermögensspitzen präzise abzubilden,
- kausale Verhaltensänderungen vorherzusagen,
- nicht implementierte Leistungs- oder Beitragslogik als Mikrosimulation auszugeben.

Ergebnisse sind deshalb zusammen mit Datenstand, Modellstatus, Kalibrierung, Unsicherheit und Einschränkungen zu lesen.

## Verwandte Kapitel

- [Einkommensteuer-Modul 2026](../02-fiskal/einkommensteuer-modul.md)
- [Einnahmen und Steuern](../02-fiskal/einnahmen-und-steuern.md)
- [Demografie und Alterspyramide](../05-module/demografie-und-alterspyramide.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Quellenregister](../06-evidenz/quellenregister.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
