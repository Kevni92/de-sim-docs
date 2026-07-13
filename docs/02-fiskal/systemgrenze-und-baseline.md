---
title: Systemgrenze und Baseline
summary: Fachliche Abgrenzung des öffentlichen Sektors und Regeln für den Referenzzustand.
status: Arbeitsstand 0.4
last_updated: 2026-07-13
---

# Systemgrenze und Baseline

## Öffentlicher Sektor

Der Simulator unterscheidet konsequent:

- Bund,
- Länder,
- Gemeinden und Gemeindeverbände,
- gesetzliche Sozialversicherungen,
- Sondervermögen,
- konsolidierter Gesamtstaat.

Transfers zwischen staatlichen Ebenen dürfen in der Gesamtansicht nicht doppelt gezählt werden.

## Baseline

Jede Simulation basiert auf einer versionierten Ausgangslage:

- Rechtsstand,
- Haushaltsjahr,
- Bevölkerungsstand,
- Preisjahr,
- Konjunkturannahmen,
- Zinsannahmen,
- Datenstand der verwendeten Statistiken.

Die Baseline ist nicht „die Wahrheit“, sondern ein reproduzierbarer Referenzlauf.

## Reale und nominale Werte

Nutzer können zwischen nominalen Eurobeträgen und preisbereinigten Werten wechseln. Langfristige Vergleiche zeigen standardmäßig reale Werte und nennen die angenommene Inflation.

## Staatliche Einnahmen und Ausgaben

Folgende Größen werden getrennt ausgewiesen:

- Bruttoeinnahmen,
- Bruttoausgaben,
- Finanzierungssaldo,
- Nettokreditaufnahme,
- Zinsausgaben,
- implizite langfristige Verpflichtungen,
- Steuervergünstigungen als entgangene Einnahmen.

## Fachliche Konsistenzregeln

- Jede Kennzahl trägt eine sichtbare Ebenenkennzeichnung.
- Die Gesamtsumme entspricht nach Rundung der Summe der Unterposten.
- Konsolidierungsbuchungen sind in der Berechnungsansicht sichtbar.
- Jeder Vergleich kann auf den unveränderten Referenzlauf zurückgeführt werden.

## Verwandte Kapitel

- [Einnahmen und Steuern](einnahmen-und-steuern.md)
- [Ausgaben und Leistungen](ausgaben-und-leistungen.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
