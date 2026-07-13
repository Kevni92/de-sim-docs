---
title: Einheitliches Detailseitenmuster
summary: Gemeinsamer Aufbau für Einkommensteuer, weitere Einnahmen und Ausgabenmodule.
status: Arbeitsstand 0.7
last_updated: 2026-07-13
---

# Einheitliches Detailseitenmuster

## Ausgangslage

Die Einkommensteuer wurde als eigenständige Detailseite in Milestone 4 ausgebaut. Die weiteren Einnahmen- und Ausgabenmodule folgten später in Milestone 5 und 6 mit einer gemeinsamen Modulliste und einem anderen Seitenraster. Dadurch entstanden zwei technisch getrennte UI-Muster für fachlich vergleichbare Detailansichten.

## Verbindlicher Aufbau

Detailseiten für Einnahmen und Ausgaben verwenden künftig dieselbe Reihenfolge:

1. Seitenkopf mit Rückkehr zum Dashboard, Bereichsbezeichnung, Titel und Kurzbeschreibung
2. Modulliste mit aktuellem Szenariowert und Änderung
3. Modulzusammenfassung mit Evidenz- oder Rechtsstatus
4. gemeinsam gruppierte Aktionen für **Berechnung und Quellen** sowie **Baseline wiederherstellen**
5. vier Kennzahlen für Baseline, Szenariowert, direkte beziehungsweise statische Wirkung und Verhaltens- beziehungsweise Folgewirkung
6. Parametereditor und Modellstufe im gemeinsamen Raster
7. modulspezifische Vertiefungen unterhalb des gemeinsamen Kerns

## Einkommensteuer

Die Einkommensteuer bleibt fachlich umfangreicher als Aggregatmodule. Tarifprüfung, Tarifkurve, Dezile und Referenzhaushalte bleiben erhalten. Sie werden jedoch unter denselben Seitenkopf, dieselbe Modulliste, dieselbe Zusammenfassung, dieselben Kennzahlkarten und dieselbe Modellstufensteuerung eingeordnet.

## Header und Aktionen

Der Seitenkopf enthält keine losgelösten Modulaktionen. Quellen- und Rücksetzaktionen gehören zur Modulzusammenfassung. Rückkehrlink und Bereichsbezeichnung werden blockweise angeordnet, damit sie bei allen Breiten getrennt lesbar bleiben.

## Responsive Verhalten

Auf breiten Bildschirmen steht die Modulliste links neben dem Inhalt. Unterhalb der definierten Umbruchbreite wird sie oberhalb des Inhalts dargestellt. Aktionsgruppen, Kennzahlkarten, Parameter und Modellstufen müssen ohne horizontale Überlagerung auf mobile Breiten umbrechen.

## Tests

Playwright prüft mindestens:

- identische Strukturklassen auf Einkommensteuer, weiteren Einnahmen und Ausgaben,
- Platzierung von **Berechnung und Quellen** in der Modulzusammenfassung,
- Platzierung von **Baseline wiederherstellen** in derselben Aktionsgruppe,
- Navigation zwischen Einkommensteuer und weiteren Einnahmenmodulen,
- Desktop-Screenshot der vereinheitlichten Detailansicht.
