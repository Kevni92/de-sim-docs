---
title: Ausgabenmodule 2026
summary: Fachlicher Vertrag, Baselines, Parameter, Wirkungslogik und Grenzen der neun priorisierten Ausgabenmodule.
status: Arbeitsstand 0.6
last_updated: 2026-07-13
---

# Ausgabenmodule 2026

## Ziel und Abgrenzung

Milestone 6 führt neun priorisierte Ausgabenbereiche als eigenständige Module ein. Sie ersetzen die bisher statische Anzeige ausgewählter Haushaltspositionen durch veränderbare, nachvollziehbare Aggregatmodelle.

Die Module sind noch keine repräsentative Leistungsfall-Mikrosimulation. Sie verbinden gerundete Ausgangsaggregate mit amtlichen Rechts-, Haushalts- und Statistikquellen. Jede Änderung bleibt als Szenario erkennbar.

## Gemeinsamer Modellvertrag

Jedes Modul liefert mindestens:

- eine abgegrenzte Baseline in Milliarden Euro pro Jahr,
- veränderbare und versionierte Parameter,
- getrennt berechnete Teilaggregate,
- die direkte Ausgabenwirkung vor weiteren Anpassungen,
- eine separat ausgewiesene Folgewirkung nach Modellstufe,
- den resultierenden Szenariowert und die Veränderung zum Status quo,
- Begünstigten- oder Leistungskanäle,
- Konfidenz, Unsicherheitsband, Quellen und bekannte Grenzen.

Die allgemeine Darstellung lautet:

\[
A_s = \sum_k A_{k,0} \cdot f_k(p)
\]

\[
\Delta A_s = A_s - A_0
\]

\[
A = A_s - \Delta A_s \cdot \varepsilon_m \cdot g(l)
\]

Dabei ist \(A_0\) die Baseline, \(A_s\) die direkte Szenariowirkung, \(\varepsilon_m\) die dokumentierte Modulsensitivität und \(g(l)\) der Faktor der Modellstufe. Die Folgewirkung ist eine Szenarioannahme und keine Prognose.

## Modellstufen

| Modellstufe | Bedeutung |
|---|---|
| statisch | Nur direkte Wirkung veränderter Leistungs-, Fallzahl-, Preis- oder Investitionsparameter. |
| mit Folgewirkung | Moderate gegenläufige Rückwirkungen werden getrennt ergänzt. |
| langfristig | Stärkere mittelfristige Rückwirkungen; weiterhin keine Konjunktur- oder Verhaltensprognose. |

Bei Ausgabenerhöhungen kann die Folgewirkung einen Teil der Mehrausgabe durch spätere Entlastungen ausgleichen. Bei Kürzungen kann sie einen Teil der direkten Einsparung durch Folge- oder Ausweichkosten zurücknehmen. Der Mechanismus wird nicht verborgen oder mit der Erstwirkung saldiert dargestellt.

## 1. Bürgergeld und Unterkunft

**Baseline:** 53,8 Mrd. Euro, aufgeteilt auf Bürgergeld und Eingliederung sowie Unterkunft und Heizung.

Parameter:

- Regelbedarfsniveau,
- Index der Bedarfsgemeinschaften,
- Unterkunfts- und Heizkosten,
- Verwaltung und Eingliederung.

Die Regelbedarfsstruktur folgt dem SGB II. Für 2026 bleiben die Regelbedarfe laut BMAS auf dem Niveau von 2024 und 2025. Regionale Miet- und Heizkosten werden noch nicht als Einzelkreise modelliert.

## 2. Rente

**Baseline:** 128,4 Mrd. Euro bundesbezogene Rentenausgaben und Zuschüsse.

Parameter:

- Rentenwert,
- Zahl und Struktur der Leistungsbeziehenden,
- Bundeszuschuss,
- vereinfachtes Referenzalter.

Der Rentenversicherungsbericht dient als amtliche Strukturquelle. Individuelle Versicherungsbiografien, Übergangsregeln und Vertrauensschutz werden erst mit einer späteren Personen- und Erwerbsbiografie abgebildet.

## 3. Bildung und Schulen

**Baseline:** 22,6 Mrd. Euro innerhalb der derzeitigen Simulatorabgrenzung.

Parameter:

- Ausgaben je Lernendem,
- Zahl der Lernenden,
- Digital- und Gebäudeinvestitionen,
- tatsächlicher Mittelabfluss.

Das Modul ist wegen der föderalen Finanzierung besonders unsicher. Der ausgewiesene Wert ist nicht mit den gesamten deutschen Bildungsausgaben gleichzusetzen.

## 4. Kitas und Familienleistungen

**Baseline:** 63,7 Mrd. Euro, davon 55,3 Mrd. Euro Familienleistungen und 8,4 Mrd. Euro Kindertagesbetreuung.

Parameter:

- Familienleistungsniveau,
- Anspruchs- und Nutzungsquote,
- finanzierte Betreuungsplätze,
- Personal- und Qualitätskosten.

Monetäre Transfers und Betreuung werden getrennt berechnet. Erwerbs-, Bildungs- und Geburteneffekte gehören nicht in die direkte Ausgabenrechnung, sondern in spätere Wirkungsmodule.

## 5. Gesundheit und Pflege

**Baseline:** 153,8 Mrd. Euro, aufgeteilt auf 92,1 Mrd. Euro Gesundheit und 61,7 Mrd. Euro Pflege.

Parameter:

- Gesundheitsleistungsvolumen,
- Vergütungsniveau,
- Zahl und Struktur der Pflegebedürftigen,
- Pflegeleistungsniveau,
- präventionsbedingte Entlastung als ausdrücklich gekennzeichnete Annahme.

Die aktuelle Stufe ist ein Aggregatmodell. Diagnosen, Pflegegrade, Leistungserbringer und Eigenanteile werden noch nicht als Einzelfälle simuliert.

## 6. Verteidigung

**Baseline:** 71,8 Mrd. Euro in der Simulatorabgrenzung.

Parameter:

- Ausrüstung und Beschaffung,
- Personal,
- Betrieb und Einsatzbereitschaft,
- tatsächlicher Mittelabfluss.

Haushaltsabgrenzung, Sondervermögen und NATO-Ausgabendefinition werden nicht gleichgesetzt. Mehrjährige Beschaffung wird vorerst als Jahresaggregat behandelt.

## 7. Infrastruktur

**Baseline:** 34,1 Mrd. Euro.

Parameter:

- Neuinvestitionen,
- Erhalt und Sanierung,
- tatsächlicher Mittelabfluss.

Das Modul trennt politische Mittelansätze vom realisierten Ausgabenabfluss. Projektqualität, Nutzen, Baupreise und Kapazitätsengpässe sind noch nicht als eigene Projektmodelle enthalten.

## 8. Subventionen

**Baseline:** 41,7 Mrd. Euro innerhalb der Simulatorabgrenzung.

Parameter:

- direkte Finanzhilfen,
- Steuervergünstigungen,
- Zielgenauigkeits-Einsparung,
- auslaufender Anteil.

Die Baseline ist nicht mit dem Gesamtvolumen des Subventionsberichts identisch. Mitnahmeeffekte und Zielgenauigkeit sind Szenarioannahmen und müssen als solche ausgewiesen werden.

## 9. Migration und Asyl

**Baseline:** 29,8 Mrd. Euro, ausdrücklich getrennt in:

| Teilaggregat | Baseline |
|---|---:|
| Unterbringung und Existenzsicherung | 9,8 Mrd. € |
| Verfahren und Verwaltung | 5,1 Mrd. € |
| Integration | 4,4 Mrd. € |
| Bildung und weitere föderale Aufgaben | 10,5 Mrd. € |

Die Teilbereiche besitzen eigene Indizes. Ausgaben werden nicht mit Steuern, Beiträgen oder gesamtwirtschaftlichen Wirkungen zu einer scheinbar exakten Nettozahl vermischt. Diese Gegenpositionen gehören in ein späteres Bevölkerungs- und Erwerbsmodell.

## Dashboard- und Szenariointegration

Die Detailmodule und das Dashboard verwenden dieselben Ergebnisse. Kombinierte Module werden auf die vorhandenen Haushaltszeilen verteilt:

- Bürgergeld und Unterkunft auf `buerger` und `wohnen`,
- Kitas und Familienleistungen auf `kita` und `familie`,
- Gesundheit und Pflege auf `gesundheit` und `pflege`.

Die Ausgabenveränderung wirkt mit umgekehrtem Vorzeichen auf den Haushaltssaldo:

\[
\Delta Saldo = \Delta Einnahmen - \Delta Ausgaben
\]

Parameter werden im zentralen Szenario unter `expenseChanges` gespeichert. Der lokale Worker simuliert den späteren Server und persistiert Entwurf, Szenarien, Quellen und Nachweise in IndexedDB.

## Validierung

Mindestens folgende Prüfungen sind erforderlich:

1. Alle Baseline-Parameter reproduzieren die jeweilige Ausgangssumme.
2. Die Summe kombinierter Teilaggregate entspricht dem Modulwert.
3. Die Summe der zugeordneten Dashboardzeilen entspricht dem Modulwert.
4. In der statischen Modellstufe ist die Folgewirkung null.
5. Eine Ausgabenerhöhung verschlechtert den Saldo, sofern keine größere Gegenwirkung modelliert ist.
6. Migration und Asyl bleiben in vier Teilaggregaten getrennt.
7. Speichern, Exportieren, Importieren und Wiederherstellen erhalten alle Ausgabenparameter.
8. Jede zentrale Kennzahl öffnet einen Nachweis mit Quellen, Formel, Parametern, Unsicherheit und Grenzen.

## Bekannte Grenzen

- keine repräsentative Leistungsfallpopulation,
- keine regionalen Kosten- und Anspruchsstrukturen,
- keine individuelle Renten-, Gesundheits-, Pflege- oder Transferbiografie,
- vereinfachte föderale Konsolidierung,
- keine Projektbewertung einzelner Infrastruktur- oder Beschaffungsvorhaben,
- Folgewirkungen sind Bandbreiten und Szenarien, keine sicheren Einsparungen,
- Baselinewerte sind gerundete Modellaggregate und nicht automatisch mit einzelnen amtlichen Tabellen identisch.

## Verwandte Kapitel

- [Ausgaben und Leistungen](ausgaben-und-leistungen.md)
- [Systemgrenze und Baseline](systemgrenze-und-baseline.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Quellenregister](../06-evidenz/quellenregister.md)
