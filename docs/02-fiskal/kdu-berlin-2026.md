---
title: Unterkunft und Heizung – Referenzdatensatz Berlin 2026
summary: Vollständig dokumentierter regionaler KdU-Datensatz für Berlin mit Bruttokaltmiet-, Wohnflächen- und Heizkostengrenzen sowie Fallback- und Übergangsregeln.
status: Fachspezifikation 0.1
last_updated: 2026-07-13
---

# Unterkunft und Heizung – Referenzdatensatz Berlin 2026

## Zweck und Geltungsbereich

Berlin ist der erste vollständig hinterlegte regionale Referenzdatensatz für die Kosten der Unterkunft und Heizung im Deutschland-Simulator. Der Datensatz übersetzt die ab **1. Januar 2026** geltende Berliner AV-Wohnen in versionierte Modellparameter. Die bundesrechtliche Anspruchslogik verwendet die Rechtsbaseline **1. Juli 2026**.

Der Datensatz ist keine individuelle Leistungsberatung. Sondertatbestände, Einzelfallentscheidungen und Nachweise können in der Verwaltungspraxis zu anderen Ergebnissen führen.

## Getrennte Prüfung

Unterkunft und Heizung werden getrennt bewertet:

```text
tatsächliche Bruttokaltmiete
  = Grundmiete + kalte Betriebskosten

anerkannte Bruttokaltmiete
  = Anerkennungsregel(
      tatsächliche Bruttokaltmiete,
      regionaler Richtwert,
      Haushaltsgröße,
      Karenz-, Übergangs- und Härtefallstatus)

anerkannte Heizkosten
  = Anerkennungsregel(
      tatsächliche Heizkosten,
      Energieträger,
      beheizte Gebäudefläche,
      Haushaltsgröße)
```

Tatsächliche, anerkannte und nicht anerkannte Beträge bleiben im Ergebnis separat sichtbar.

## Bruttokaltmiete und Referenzfläche

Die Berliner Richtwerte ab 1. Januar 2026 lauten:

| Personen | Referenzfläche | monatliche Bruttokaltmiete |
|---:|---:|---:|
| 1 | 50 m² | 449,00 € |
| 2 | 65 m² | 543,40 € |
| 3 | 80 m² | 668,80 € |
| 4 | 90 m² | 752,40 € |
| 5 | 102 m² | 903,72 € |
| jede weitere Person | +12 m² | +106,32 € |

Die Referenzfläche ist ein Prüf- und Erklärwert. Für die monetäre Anerkennung ist der jeweils anwendbare Bruttokaltmietrichtwert maßgeblich, soweit keine speziellere Regel greift.

## Heizkostengrenzen

Die monatlichen Heizkostengrenzen hängen vom Energieträger, der beheizten Gebäudefläche und der Zahl der Personen ab. Die letzte Spalte enthält den Zuschlag für jede weitere Person ab sechs Personen.

| Energieträger | beheizte Gebäudefläche | 1 Person | 2 Personen | 3 Personen | 4 Personen | 5 Personen | weitere Person |
|---|---:|---:|---:|---:|---:|---:|---:|
| Heizöl | 100–250 m² | 109,00 € | 141,70 € | 174,40 € | 196,20 € | 222,36 € | 26,16 € |
| Heizöl | 251–500 m² | 101,50 € | 131,95 € | 162,40 € | 182,70 € | 207,06 € | 24,36 € |
| Heizöl | 501–1.000 m² | 94,50 € | 122,85 € | 151,20 € | 170,10 € | 192,78 € | 22,68 € |
| Heizöl | über 1.000 m² | 90,50 € | 117,65 € | 144,80 € | 162,90 € | 184,62 € | 21,72 € |
| Erdgas | 100–250 m² | 133,00 € | 172,90 € | 212,80 € | 239,40 € | 271,32 € | 31,92 € |
| Erdgas | 251–500 m² | 123,50 € | 160,55 € | 197,60 € | 222,30 € | 251,94 € | 29,64 € |
| Erdgas | 501–1.000 m² | 115,00 € | 149,50 € | 184,00 € | 207,00 € | 234,60 € | 27,60 € |
| Erdgas | über 1.000 m² | 110,00 € | 143,00 € | 176,00 € | 198,00 € | 224,40 € | 26,40 € |
| Fernwärme | 100–250 m² | 102,00 € | 132,60 € | 163,20 € | 183,60 € | 208,08 € | 24,48 € |
| Fernwärme | 251–500 m² | 99,50 € | 129,35 € | 159,20 € | 179,10 € | 202,98 € | 23,88 € |
| Fernwärme | 501–1.000 m² | 98,00 € | 127,40 € | 156,80 € | 176,40 € | 199,92 € | 23,52 € |
| Fernwärme | über 1.000 m² | 96,50 € | 125,45 € | 154,40 € | 173,70 € | 196,86 € | 23,16 € |
| Wärmepumpe | 100–250 m² | 121,00 € | 157,30 € | 193,60 € | 217,80 € | 246,84 € | 29,04 € |
| Wärmepumpe | 251–500 m² | 124,50 € | 161,85 € | 199,20 € | 224,10 € | 253,98 € | 29,88 € |
| Wärmepumpe | 501–1.000 m² | 117,50 € | 152,75 € | 188,00 € | 211,50 € | 239,70 € | 28,20 € |
| Wärmepumpe | über 1.000 m² | 115,50 € | 150,15 € | 184,80 € | 207,90 € | 235,62 € | 27,72 € |

Die Berliner AV-Wohnen verwendet den bundesweiten Heizspiegel als fachliche Grundlage, weil kein vergleichbarer kommunaler Heizspiegel vorliegt. Die Anwendung erfolgt tabellengetrieben; Änderungen der Werte benötigen keine Änderung des Rechenalgorithmus.

## Karenzzeit ab Juli 2026

Mit der bundesrechtlichen Umgestaltung der Grundsicherung ab 1. Juli 2026 bleibt eine einjährige Karenzzeit für Unterkunftskosten bestehen. Die Anerkennung ist in dieser Zeit jedoch auf das **Eineinhalbfache der abstrakten örtlichen Angemessenheitsgrenze** begrenzt.

```text
Karenzzeitdeckel
  = 1,5 × örtlicher Bruttokaltmietrichtwert

anerkannte Bruttokaltmiete während der Karenzzeit
  = min(tatsächliche Bruttokaltmiete, Karenzzeitdeckel)
```

Heizkosten werden weiterhin getrennt auf Erforderlichkeit und Angemessenheit geprüft. Ein Härtefall oder ein ausdrücklich laufender Kostensenkungszeitraum ist ein eigener Laufzeitfakt und darf nicht aus der Höhe der Miete erraten werden.

## Lookup- und Fallback-Hierarchie

Der Rechner sucht in dieser Reihenfolge:

1. exakter kommunaler Träger und Referenzmonat,
2. exakte Region und Referenzmonat,
3. geeignete übergeordnete Region,
4. dokumentierter Deutschland-Modell-Fallback,
5. Fehlerstatus, wenn auch kein Fallback verfügbar ist.

Der Modell-Fallback ist **kein örtliches Recht**. Er führt die Unsicherheitsklasse `hoch`, nennt den verwendeten Index und bleibt in der Erklärspur sichtbar. Ein fehlender Datensatz erzeugt niemals automatisch null Euro anerkannte Kosten.

Fehlen bei einem vorhandenen Regionaldatensatz Energieträger oder beheizte Gebäudefläche, werden tatsächliche Heizkosten übergangsweise mit hoher Unsicherheit anerkannt. Das Ergebnis enthält eine Warnung und die fehlenden Merkmale.

## Ergebnisfelder

Das regionale KdU-Ergebnis enthält mindestens:

- tatsächliche Grundmiete und kalte Betriebskosten,
- tatsächliche Bruttokaltmiete und Heizkosten,
- anerkannte Grundmiete und kalte Betriebskosten,
- anerkannte Bruttokaltmiete und Heizkosten,
- nicht anerkannte Unterkunfts- und Heizkosten,
- verwendeten Datensatz und Regeln,
- Gültigkeitsmonat und Lookup-Stufe,
- Parameter-, Quellen- und Fallback-Spur,
- Unsicherheitsklasse und Validierungshinweise.

## Versionierung

| Bestandteil | Wert |
|---|---|
| Datensatz-ID | `sgb2-kdu-berlin-2026` |
| KdU-Datenschema | `1` |
| KdU-Ergebnisschema | `1` |
| Rechenmodell | `sgb2-housing-0.1.0` |
| regionale Gültigkeit | Berlin |
| gültig ab | 1. Januar 2026 |
| bundesrechtliche Baseline | 1. Juli 2026 |
| Evidenzklasse | amtliche Ausführungsvorschrift |
| Unsicherheit der Tabellenwerte | niedrig |

Eine Änderung der Tabelle erhöht die Datensatzversion. Eine Änderung der Lookup-, Karenz-, Übergangs-, Härtefall- oder Rundungslogik erhöht die Rechenmodellversion.

## Quellen

- [Berlin.de: Kosten der Unterkunft und Heizung – AV-Wohnen](https://www.berlin.de/sen/soziales/soziale-sicherung/kosten-der-unterkunft/kosten-der-unterkunft-av-wohnen/)
- [Berliner Sozialrecht: AV-Wohnen](https://sozialrecht.berlin.de/kategorie/ausfuehrungsvorschriften/av-wohnen-573488.html)
- [Berliner Sozialrecht: Anlage 2 – Heiz- und Warmwasserbereitungskosten](https://sozialrecht.berlin.de/kategorie/ausfuehrungsvorschriften/av-wohnen-571939-v9-anlage-2.html)
- [BMAS: Leistungen und Bedarfe in der Grundsicherung für Arbeitsuchende](https://www.bmas.de/DE/Arbeit/Grundsicherung-fuer-Arbeitsuchende/Leistungen-und-Bedarfe-in-der-Grundsicherung-fuer-Arbeitsuchende/leistungen-und-bedarfe-in-der-grundsicherung-fuer-arbeitsuchende.html)
- [SGB II § 22](https://www.gesetze-im-internet.de/sgb_2/__22.html)

## Bekannte Grenzen

- Berlin ist zunächst der einzige vollständig parametrierte regionale Datensatz.
- Besondere Zuschläge, Klimabonus, sozialer Wohnungsbau, Neuanmietung und weitere Berliner Einzelfallregeln sind noch nicht vollständig als eigene Entscheidungstatbestände umgesetzt.
- Gebäudefläche und Energieträger fehlen in Teilen der synthetischen Bevölkerung und werden erst in einem späteren Datenpaket flächendeckend ergänzt.
- Der KdU-Rechner liefert die Anspruchskomponente; Kostenträgeraggregation und UI folgen in getrennten Arbeitspaketen.
