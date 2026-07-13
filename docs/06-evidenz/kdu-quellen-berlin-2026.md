---
title: KdU-Quellen Berlin 2026
summary: Quellen- und Verwendungsnachweis für den regionalen Berliner Unterkunfts- und Heizkostendatensatz 2026.
status: Quellenstand 0.1
last_updated: 2026-07-13
---

# KdU-Quellen Berlin 2026

## Registrierte Quellen

### `source-sgb2-kdu-berlin-2026`

| Feld | Wert |
|---|---|
| Institution | Land Berlin, Senatsverwaltung für Arbeit, Soziales, Gleichstellung, Integration, Vielfalt und Antidiskriminierung |
| Titel | Kosten der Unterkunft und Heizung – AV-Wohnen |
| Daten- und Gültigkeitsstand | ab 1. Januar 2026 |
| Evidenzklasse | amtliche Ausführungsvorschrift |
| Modellverwendung | Bruttokaltmietrichtwerte, Referenzflächen, Heizkostengrenzen, Größen- und Energieträgerzuordnung |
| Unsicherheit der übernommenen Tabellenwerte | niedrig |
| regionale Abdeckung | Berlin |

Primärquellen:

- [Berlin.de: Kosten der Unterkunft und Heizung – AV-Wohnen](https://www.berlin.de/sen/soziales/soziale-sicherung/kosten-der-unterkunft/kosten-der-unterkunft-av-wohnen/)
- [Berliner Sozialrecht: AV-Wohnen](https://sozialrecht.berlin.de/kategorie/ausfuehrungsvorschriften/av-wohnen-573488.html)
- [Berliner Sozialrecht: Anlage 2 – Heiz- und Warmwasserbereitungskosten](https://sozialrecht.berlin.de/kategorie/ausfuehrungsvorschriften/av-wohnen-571939-v9-anlage-2.html)

Die Berlin.de-Seite bestätigt die Änderungen ab 1. Januar 2026, die getrennte Prüfung von Bruttokaltmiete und Heizkosten sowie die Aktualisierung der Anlagen. Die tabellarischen Werte werden in Cent pro Monat gespeichert und ohne implizite Euro- oder Jahresumrechnung verwendet.

### `source-sgb2-law`

| Feld | Wert |
|---|---|
| Institution | Bundesrepublik Deutschland / BMAS |
| Rechtsstand | 1. Juli 2026 |
| Modellverwendung | Karenzzeit, Deckel auf 1,5-fache örtliche Angemessenheitsgrenze, Übergangs- und Kostensenkungsregeln |
| Evidenzklasse | Gesetz und amtliche Erläuterung |
| Unsicherheit | niedrig |

Primärquellen:

- [SGB II § 22](https://www.gesetze-im-internet.de/sgb_2/__22.html)
- [BMAS: Leistungen und Bedarfe in der Grundsicherung für Arbeitsuchende](https://www.bmas.de/DE/Arbeit/Grundsicherung-fuer-Arbeitsuchende/Leistungen-und-Bedarfe-in-der-Grundsicherung-fuer-Arbeitsuchende/leistungen-und-bedarfe-in-der-grundsicherung-fuer-arbeitsuchende.html)
- [BMAS: Ziele, Regeln und Änderungen der Grundsicherung](https://www.bmas.bund.de/DE/Arbeit/Grundsicherung-fuer-Arbeitsuchende/Ziele-Regeln-Aenderungen/ziele-regeln-aenderungen.html)

Die bundesrechtliche Regel wird vom regionalen Tabellenstand getrennt versioniert. Ein Berliner Richtwert kann daher ab Januar 2026 gültig sein, während der Karenzzeitdeckel erst für die Rechtsbaseline ab Juli 2026 angewendet wird.

### `source-sgb2-kdu-model`

| Feld | Wert |
|---|---|
| Institution | Deutschland-Simulator |
| Status | Modell-Fallback |
| Modellverwendung | Fälle ohne passenden regionalen Datensatz oder ohne vollständige Heizmerkmale |
| Evidenzklasse | Modell |
| Unsicherheit | hoch |

Der Fallback behauptet keine kommunale Angemessenheitsgrenze. Er verhindert ausschließlich einen stillen Nullwert und hält die Fälle für spätere regionale Ergänzungen rechenbar. Ergebnis, Fallback-Grund, verwendeter Index und Unsicherheit bleiben sichtbar.

## Übernahmekontrollen

Für jede Tabellenübernahme werden geprüft:

- Einheit und monatlicher Zeitbezug,
- Zahl der Personen beziehungsweise Zuschlag weiterer Personen,
- Energieträger und Gebäudeflächenintervall,
- Gültigkeitsbeginn,
- Übereinstimmung von Parameter-ID, Quelle und Datensatz-ID,
- Grenzfälle knapp unter, exakt auf und knapp über dem Richtwert.

## Nicht als amtliche Tatsache behandelt

Nicht aus den Berliner Quellen abgeleitet werden:

- gemeinsame Verteilung von Miete, Heizkosten, Energieträger und Haushaltsstruktur in der synthetischen Bevölkerung,
- fehlende Gebäudeflächen und Energieträger,
- kommunale Werte außerhalb Berlins,
- individuelle Härtefallentscheidungen,
- tatsächliche Verfügbarkeit angemessener Wohnungen.

Diese Bestandteile sind Modell oder Laufzeitfakt und müssen getrennt von den amtlichen Tabellenwerten gekennzeichnet werden.
