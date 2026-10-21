---
title: Systemgrenze und Baseline
summary: Fachliche Abgrenzung des öffentlichen Sektors und Regeln für den Referenzzustand.
status: Arbeitsstand 0.4
last_updated: 2026-10-21
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

Im aktuellen Produktumfang verwenden gesetzliche Berechnungen den festen Rechtsstand 2026. Eine globale Datenjahresauswahl ist fachlich nicht zutreffend: Jede Kennzahl nennt den Stand ihrer eigenen Quelle. Ein Betrachtungsjahr oder der Startpunkt einer Wirkungsrechnung beschreibt den Zeitraum eines Szenariopfads und ist weder Rechtsstand noch Datenherkunft.

Importierte Szenarien können abweichende Jahresmetadaten enthalten. Diese Angaben bleiben beim Laden und Export erhalten. Die Oberfläche kennzeichnet sie sichtbar als Altmetadaten und erklärt getrennt, welche gesetzliche Grundlage unterstützt wird und welchen Zeitbezug der Szenariopfad verwendet. Abweichende Altjahre werden nicht still umgedeutet oder als unterstützte gesetzliche Tarife ausgegeben.

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

## Schuldenbestand und jährlicher Saldo

Ein Schuldenstand ist eine Bestandsgröße zu einem konkreten Stichtag. Die Oberfläche darf ihn nur als historischen Referenzwert ausweisen, wenn Quelle, Abgrenzung und Stichtag nachvollziehbar zusammenpassen. Fehlt dieser Nachweis, wird ein angezeigter Festwert ausdrücklich als Beispiel markiert oder aus der Hauptübersicht genommen.

Der Saldo der ausgewiesenen Einnahmen und Ausgaben ist eine Jahresgröße. Seine Änderung im Szenario beschreibt die jährliche Wirkung auf die ausgewiesenen Posten; sie ist keine Veränderung des historischen Schuldenbestands und wird nicht zu einer Schuldenprognose fortgeschrieben. Eine Quote zum Bruttoinlandsprodukt erscheint nur, wenn Zähler und Nenner auf denselben belegten Referenzzeitraum und dieselbe Abgrenzung bezogen sind. Ein pauschales Unsicherheitsband ersetzt diesen Nachweis nicht.

## Summen in Übersicht und Vergleich

Die Kennzahlen in Übersicht und Vergleich beruhen auf denselben ausgewiesenen Einnahme- und Ausgabenposten des aktiven Szenarios. Der Vergleich übernimmt damit die sichtbare Bezugsgröße der Übersicht, statt daneben eine abweichende feste Gesamtsumme zu verwenden.

Diese Summen bilden nur die dargestellten Posten ab und sind keine vollständige Haushaltsrechnung. Nicht enthaltene Teilbereiche werden weder ergänzt noch als unverändert oder null behandelt. Fehlt ein benötigter Modulwert, muss die Gesamtsumme als unvollständig erkennbar sein.

Die Werte des aktiven Szenarios verwenden die dort angezeigte Modellstufe. Direkte Modulwirkung und davon getrennte Wirkungsregister-Pfade bleiben benannt; veraltete oder noch berechnete Wirkungspfade dürfen nicht als aktuelle Zahlen erscheinen. Eine Vergleichsannahme ohne gleichwertige Modulergebnisse ist bei Gesamtsummen als nicht vergleichbar zu kennzeichnen.

## Fachliche Konsistenzregeln

- Jede Kennzahl trägt eine sichtbare Ebenenkennzeichnung.
- Die ausgewiesene Summe entspricht nach Rundung der sichtbaren Unterposten und behauptet keine vollständige Haushaltsrechnung.
- Übersicht und Vergleich verwenden für gleiche Szenarien dieselben Werte und denselben Umfang.
- Fehlende oder veraltete Ergebnisse erscheinen nicht als null oder aktueller Gesamtwert.
- Konsolidierungsbuchungen sind in der Berechnungsansicht sichtbar.
- Jeder Vergleich kann auf den unveränderten Referenzlauf zurückgeführt werden.

## Verwandte Kapitel

- [Einnahmen und Steuern](einnahmen-und-steuern.md)
- [Ausgaben und Leistungen](ausgaben-und-leistungen.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
