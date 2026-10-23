---
title: Visualisierungen
summary: Fachliche Darstellungsformen für Haushalt, Verteilung, Wirkungsketten, Regionen und Zeit.
status: Arbeitsstand 0.5
last_updated: 2026-10-23
---

# Visualisierungen

## Visuelle Orientierung in Reformansichten

Eine Reformansicht verwendet eine klare Hierarchie: Der Modulkopf bleibt sichtbar, die primäre Stellschraube erhält einen eigenen Arbeitsbereich, und Baseline, direkte staatliche Wirkung, hauptsächlich betroffene Gruppe sowie Belastbarkeit erscheinen als zusammenhängende Ergebnisleiste. Vertiefungen bleiben geschlossen visuell leichter als der primäre Arbeitsbereich; beim Öffnen bleiben vollständige Fachdetails erreichbar.

Fachliche Icons stammen aus einem konsistenten lokalen SVG-System. Emoji und Unicode-Piktogramme ersetzen keine UI-Symbole. Dekorative Icons sind für Screenreader verborgen; eine interaktive Symbolaktion erhält einen sichtbaren Text oder einen eindeutigen zugänglichen Namen.

Die Farbakzente haben einen eng begrenzten Sinn: Türkis zeigt aktive Bedienung und Auswahl, Blau oder neutrale Töne Baseline und Information, Grün und Rot das fiskalische Vorzeichen im dargestellten Kontext, Gelb oder Orange Unsicherheit, Vorsicht und Extrapolation. Grün und Rot sind keine politische Gesamtbewertung. Keine Information hängt allein von Farbe ab; sichtbare Labels, Werte und zugängliche Statusangaben bleiben erhalten.

Desktop und Mobil behalten dieselbe fachliche Reihenfolge. Auf schmalen Ansichten dürfen Elemente umbrechen oder untereinander stehen, ohne dass Kerninformation, Einheit oder Bedeutung durch horizontales Pflichtscrollen verloren gehen.

## Haushaltsbilanz

- Einnahmen,
- Ausgaben,
- Saldo,
- Veränderung zur Baseline,
- Schuldenpfad und Zinsen.

## Budgetbalken und Zeitbezug

Saldo und Änderungen werden mit einer sichtbaren Nullachse und derselben linearen Skala dargestellt. Nullwerte bleiben ohne Balkenhöhe; positive und negative Werte sind an ihrer Richtung erkennbar. Einheit, Jahresbezug und Zahlenwerte stehen direkt an der Grafik.

Die gemeinsame Beschriftung ordnet diese Geldwerte der staatlichen Einnahmen- und Ausgabenperspektive zu und benennt die ausgewiesenen Posten. Haushaltswirkungen erscheinen mit ihrer eigenen Monats- oder Jahresangabe. Eine Preisbasis oder ein Preisjahr wird nur aus dem Kennzahlenvertrag übernommen; fehlt die Festlegung, wird „Preisgrundlage nicht ausgewiesen“ angezeigt.

Eine Änderung des Jahressaldos ist keine Zeitreihe. Ohne berechnete Folgejahre wird sie nicht automatisch fortgeschrieben oder mit einem pauschalen Wachstum versehen. Für tatsächlich modellierte Mehrjahresszenarien führt ein klarer Einstieg in die Langfristansicht.

## Sankey-Diagramm

Zeigt Geldflüsse zwischen Einnahmen, staatlichen Ebenen und Ausgaben. Konsolidierte interne Transfers sind gesondert markiert.

## Wirkungsgraph

Interaktive Knoten und Kanten zeigen direkte und indirekte Folgen. Linienart und Badge kennzeichnen Evidenz und Quantifizierbarkeit.

## Verteilungsdiagramme

- Einkommensdezile,
- Haushaltstypen,
- Alter,
- Erwerbsstatus,
- Vermögensgruppen,
- Bundesländer.

## Deutschlandkarte

Die Karte kann anzeigen:

- Einnahmen und Ausgaben pro Kopf,
- Betreuungsangebot,
- Arbeitsmarkt,
- Demografie,
- Wirkung eines Szenarios.

Regionale Unterschiede werden nur bis zur belastbaren Datenauflösung gezeigt.

## Alterspyramide

Baseline und Szenario können überlagert oder als Differenz dargestellt werden. Ein Zeitregler steuert das Jahr.

## Zeit- und Lebensqualitätsindikatoren

- Betreuungsstunden,
- Wartezeiten,
- Pendelzeit,
- Krankheitstage,
- Unterrichtsausfall,
- Verwaltungsminuten.

## Langfristtabellen

Vergleichstabellen trennen Baseline, Szenario, Differenz und Szenarioband in eigene Spalten. Eine Differenz hat dasselbe Bezugsjahr und dieselbe Einheit wie die verglichenen Werte. Ein nicht berechnetes Band wird als solches benannt; ein Unter- oder Oberpfad steht nie unter Baseline oder Zentralwert.

Langfristige Geldwerte tragen das Zieljahr und die staatliche Ebene beziehungsweise den betroffenen Teilhaushalt. Im aktuellen Produkt ist ihre Preisgrundlage nicht ausgewiesen; sie werden weder als reale Werte bezeichnet noch in andere Preise umgerechnet. Ein monatlicher Haushaltswert bleibt klar von einem staatlichen Jahresstrom getrennt.

Der Rentenindikator lautet durchgehend „Beitragszahlende je 100 Rentenbeziehende“. Er bleibt als Strukturquote von einer Finanzkennzahl getrennt. Auf schmalen Ansichten bleibt notwendiger Tabellenscroll innerhalb des benannten, per Tastatur erreichbaren Tabellenbereichs.

## Barrierefreie Alternativen

Jede Grafik besitzt eine Tabelle, eine Textzusammenfassung und einen Datenexport. Farben sind nie der einzige Bedeutungsträger.

## Verwandte Kapitel

- [Informationsarchitektur und progressive Offenlegung](../01-produkt/informationsarchitektur-und-progressive-offenlegung.md)
- [Indirekte und nicht monetäre Wirkungen](../04-modell/indirekte-und-nichtmonetaere-wirkungen.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
