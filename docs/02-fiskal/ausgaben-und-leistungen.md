---
title: Ausgaben und Leistungen
summary: Fachliche Übersicht der öffentlichen Ausgaben, Leistungen und priorisierten Simulationsmodule.
status: Arbeitsstand 0.6
last_updated: 2026-07-13
---

# Ausgaben und Leistungen

## Implementierter Stand

Neun priorisierte Ausgabenbereiche sind als veränderbare Aggregatmodule umgesetzt. Baseline, Parameter, Teilaggregate, direkte Wirkung, Folgewirkung, Begünstigtenstruktur, Unsicherheit und Quellen werden in einem eigenen Kapitel beschrieben:

[Zu den Ausgabenmodulen 2026](ausgabenmodule.md)

Umgesetzt sind:

- Bürgergeld und Unterkunft,
- Rente,
- Bildung und Schulen,
- Kitas und Familienleistungen,
- Gesundheit und Pflege,
- Verteidigung,
- Infrastruktur,
- Subventionen,
- Migration und Asyl mit getrennten Teilaggregaten.

Die Module ersetzen für diese Positionen die statischen Demonstrationswerte. Sie sind noch keine repräsentative Leistungsfall-Mikrosimulation. Nicht implementierte Ausgabenpositionen bleiben unverändert und werden als solche behandelt.

## Soziale Sicherung

Zum fachlichen Zielbild gehören:

- Renten und Bundeszuschüsse,
- Pensionen,
- Kranken- und Pflegeleistungen,
- Bürgergeld und Kosten der Unterkunft,
- Arbeitslosengeld,
- Grundsicherung im Alter,
- Kindergeld, Kinderzuschlag und Elterngeld,
- Wohngeld,
- Eingliederungs- und Jugendhilfe.

Jeder Posten soll sowohl Geld als auch Leistungsindikatoren zeigen. Das Bürgergeld-Modul enthält bereits Regelbedarfsniveau, Zahl der Bedarfsgemeinschaften, Unterkunftskosten sowie Verwaltung und Eingliederung. Individuelle Anspruchsprüfungen folgen erst mit einer synthetischen Leistungsfallpopulation.

## Bildung und Betreuung

Zum Zielbild gehören:

- Kitas und Tagespflege,
- Schulen,
- Ganztagsbetreuung,
- Hochschulen,
- berufliche Bildung,
- BAföG,
- Forschung,
- Gebäude und Digitalisierung.

Die aktuelle Stufe modelliert Bildung und Schulen sowie Kitas und Familienleistungen als getrennte Module. Föderale Ebenen, regionale Kosten und Schularten sind noch aggregiert.

## Gesundheit und Prävention

Berücksichtigt werden sollen:

- ambulante und stationäre Versorgung,
- Arzneimittel,
- Pflege,
- Rehabilitation,
- Prävention,
- öffentlicher Gesundheitsdienst,
- Digitalisierung und Verwaltung.

Das implementierte Modul trennt Gesundheit und Pflege. Eine Präventionsentlastung kann als unsichere Szenarioannahme gesetzt werden; sie wird nicht als sichere Einsparung behandelt.

## Infrastruktur und Daseinsvorsorge

Zum Zielbild gehören:

- Bahn und ÖPNV,
- Straßen und Brücken,
- Breitband und Mobilfunk,
- Wohnungsbau,
- Energie- und Wärmenetze,
- Wasser und Abwasser,
- kommunale Infrastruktur einschließlich Spielplätzen.

Die aktuelle Modellstufe trennt Neuinvestitionen, Erhalt und tatsächlichen Mittelabfluss. Einzelne Projekte und ihre Nutzen-Kosten-Wirkung werden noch nicht bewertet.

## Sicherheit, Verteidigung und Verwaltung

Zum Zielbild gehören:

- Verteidigung,
- Polizei,
- Justiz,
- Bevölkerungsschutz,
- allgemeine Verwaltung,
- Zinsausgaben,
- EU-Beiträge,
- Entwicklungszusammenarbeit.

Verteidigung ist als erstes Modul dieses Bereichs umgesetzt. Personal, Beschaffung, Betrieb und Mittelabfluss bleiben getrennte Treiber. Die Haushaltsabgrenzung wird nicht mit der NATO-Abgrenzung gleichgesetzt.

## Subventionen

Direkte Finanzhilfen und Steuervergünstigungen werden getrennt dargestellt. Jede Subvention soll enthalten:

- Ziel,
- Empfängergruppe,
- Bruttokosten,
- mögliche Mitnahmeeffekte,
- Evaluationsstatus,
- Auslaufdatum,
- bekannte Wirkungsindikatoren.

Das aktuelle Aggregatmodul bietet getrennte Indizes für Finanzhilfen und Steuervergünstigungen sowie Annahmen zu Zielgenauigkeit und auslaufenden Maßnahmen. Eine maßnahmenscharfe Datenbank folgt später.

## Migration und Asyl

Migration und Asyl wird nicht als pauschale Einzelzahl modelliert. Die aktuelle Baseline bleibt getrennt nach:

- Unterbringung und Existenzsicherung,
- Verfahren und Verwaltung,
- Integration,
- Bildung und weiteren föderalen Aufgaben.

Steuern, Beiträge und gesamtwirtschaftliche Wirkungen werden nicht mit diesen Ausgaben zu einer scheinbar exakten Nettozahl vermischt. Sie benötigen eine gemeinsame Bevölkerungs- und Erwerbsmodellierung.

## Gemeinsame Regeln

Alle Ausgabenmodule müssen:

1. Baseline und Szenario trennen,
2. direkte Haushaltswirkung vor Folgewirkungen zeigen,
3. Teilaggregate einzeln berechnen,
4. konsistente Werte in Detailansicht und Dashboard verwenden,
5. Datenstand, Rechtsstand und Modellversion nennen,
6. nicht berechnete Größen als nicht berechnet kennzeichnen,
7. Quellen, Formel, Parameter, Unsicherheit und Grenzen öffnen können.

## Verwandte Kapitel

- [Ausgabenmodule 2026](ausgabenmodule.md)
- [Systemgrenze und Baseline](systemgrenze-und-baseline.md)
- [Einnahmen und Steuern](einnahmen-und-steuern.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
- [Kita, Familie und Bildung](../05-module/kita-familie-und-bildung.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
