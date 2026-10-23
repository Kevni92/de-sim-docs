---
title: Systemgrenze und Baseline
summary: Fachliche Abgrenzung des öffentlichen Sektors und Regeln für den Referenzzustand.
status: Arbeitsstand 0.4
last_updated: 2026-10-23
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

## Preisbasis und Preisjahr

Das Datenjahr einer Quelle ist nicht automatisch das Preisjahr eines Geldwerts. Preisbasis und Preisjahr werden nur genannt, wenn der zugrunde liegende Kennzahlenvertrag sie festlegt. Fehlt diese Festlegung, lautet die Einordnung „Preisgrundlage nicht ausgewiesen“; aus Datenjahr, Rechtsstand oder Zieljahr wird keine nominale oder reale Preisbasis abgeleitet.

In der aktuellen Produktfassung ist für die Geldwerte der Langfristansicht keine Preisgrundlage ausgewiesen. Diese Werte dürfen deshalb nicht als real oder inflationsbereinigt bezeichnet werden. Eine Auswahl zwischen nominalen und realen Werten oder eine Umrechnung wird erst angeboten, wenn ein fachlich freigegebener Vertrag Preisjahr, Index, Bezugszeitraum und Quellen festlegt.

## Zeitraum, Ebene und Perspektive

Jede zentrale Kennzahl wird mit ihrer fachlichen Bezugsgröße lesbar gemacht: Jahresstrom, Monatswirkung, Zieljahr oder Bestand zu einem belegten Stichtag. Staatliche Einnahmen und Ausgaben werden als staatliche Perspektive gekennzeichnet; Wirkungen auf Referenzhaushalte werden als private Haushaltsperspektive mit ihrer eigenen Einheit ausgewiesen. Werte aus Teilhaushalten, etwa der Alterssicherung, werden nicht als Gesamtsaldo des öffentlichen Sektors bezeichnet.

Jahreswerte des öffentlichen Gesamthaushalts beruhen auf den ausgewiesenen Einnahmen und Ausgaben von Bund, Ländern, Kommunen und Sozialversicherung. Sie sind ohne vollständige Abdeckung keine vollständige Haushaltsrechnung. Ein Eurobetrag pro Monat für einen Haushalt und ein staatlicher Jahresbetrag sind verschiedene Kennzahlen und dürfen weder in Tabellen noch in Summen gleichgesetzt werden.

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

### Unterschiedliche Szenariogrundlagen

Der Vergleich verwendet die Parameter und verfügbaren Modellreferenzen jeder Spalte unverändert. Er zeigt den aktuellen Arbeitsentwurf neben einer ausdrücklich ausgewählten gespeicherten Szenariofassung; eine feste Beispielannahme ersetzt keine gespeicherte Alternative. Die Auswahl bleibt schreibgeschützt und darf weder den Entwurf noch die gespeicherte Fassung verändern.

Rechts- und Datenstand, Modellstufe, Zeithorizont, Bevölkerungslauf und versionierte Fachmodelle werden vor der Gegenüberstellung geprüft. Abweichungen sind mit ihrer konkreten Bedeutung sichtbar zu machen. Ergebnisse aus abweichenden Grundlagen sind keine gleichgrundige Differenz: Die App berechnet dafür keine zusammenfassende Vergleichswirkung und harmonisiert die Werte nicht stillschweigend. Fehlt eine notwendige Referenz oder ist ein Ergebnis veraltet, wird der betreffende Wert als nicht verfügbar beziehungsweise nicht aktuell gekennzeichnet.

## Fachliche Konsistenzregeln

- Jede Kennzahl nennt Zeitraum, Ebene und Perspektive; Geldwerte nennen die belegte Preisgrundlage oder weisen sie als nicht ausgewiesen aus.
- Die ausgewiesene Summe entspricht nach Rundung der sichtbaren Unterposten und behauptet keine vollständige Haushaltsrechnung.
- Übersicht und Vergleich verwenden für gleiche Szenarien dieselben Werte und denselben Umfang.
- Gleiche Kennzahlen tragen in Übersicht, Vergleich und Nachweis dieselbe Einheit und Perspektive.
- Fehlende oder veraltete Ergebnisse erscheinen nicht als null oder aktueller Gesamtwert.
- Konsolidierungsbuchungen sind in der Berechnungsansicht sichtbar.
- Jeder Vergleich kann auf den unveränderten Referenzlauf zurückgeführt werden.

## Verwandte Kapitel

- [Einnahmen und Steuern](einnahmen-und-steuern.md)
- [Ausgaben und Leistungen](ausgaben-und-leistungen.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
