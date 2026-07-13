---
title: Bürgergeld – Bedienoberfläche und Szenarien
summary: Bedienlogik für konkrete SGB-II-Parameter, Live-Neuberechnung, Nachweise und Ergebnisdarstellung.
status: Implementierungsdokumentation 0.1
last_updated: 2026-07-13
---

# Bürgergeld – Bedienoberfläche und Szenarien

## Zweck

Die Bürgergeld-Oberfläche ersetzt pauschale Kostenindizes durch konkrete, versionierte Parameter. Jede Änderung wird auf einen vollständigen SGB-II-Parametersatz angewendet und mit dem aktiven synthetischen Bevölkerungslauf neu berechnet.

Einfach- und Expertenmodus sind zwei Ansichten auf denselben Szenariozustand. Es gibt keine getrennte vereinfachte Rechenlogik.

## Einfachmodus

Der Einfachmodus fasst konkrete Parameter zu vier Gruppen zusammen:

| Gruppe | Inhalt |
|---|---|
| Regelbedarfe | Eurobeträge für Erwachsene, Partner und Kinder |
| Mehrbedarfe | Prozentsätze und Obergrenzen für Schwangerschaft, Alleinerziehung und Teilhabe |
| Freibeträge | Grundabzug, Einkommensgrenzen und Erwerbstätigenfreibeträge |
| Unterkunft und Heizung | regionale Miet- und Heizgrenzen sowie Karenz- und Fallbackparameter |

Eine Änderung auf beispielsweise 105 Prozent skaliert jeden numerischen Parameter der gewählten Gruppe gegenüber seiner Baseline. Die daraus entstehenden Einzelwerte werden als reguläre `parameterOverrides` gespeichert.

Wurden einzelne Werte im Expertenmodus unterschiedlich verändert, kennzeichnet der Einfachmodus die Gruppe als **gemischte Einzelwerte**. Beim erneuten Verschieben des Gruppenreglers werden die Einzelwerte wieder proportional zur Baseline gesetzt.

## Expertenmodus

Der Expertenmodus zeigt die konkreten Werte mit ihrer fachlichen Einheit. Dazu gehören insbesondere:

- Regelbedarfe in Euro pro Monat,
- Mehrbedarfe in Prozent,
- Grundabzüge und Einkommensgrenzen in Euro pro Monat,
- Karenz- und Übergangszeiträume in Monaten,
- regionale Bruttokaltmietgrenzen,
- Heizkostengrenzen,
- Modell- und Fallbackparameter.

Eurobeträge werden in der Oberfläche in Euro angezeigt und im Rechenvertrag als ganzzahlige Centbeträge gespeichert. Prozentwerte werden sichtbar als Prozent und intern als Anteil zwischen null und eins geführt.

Jedes Feld zeigt:

- Baseline und Szenariowert,
- Einheit,
- Quellen-ID,
- Rechtsstand,
- Datenstand, soweit getrennt vorhanden,
- Evidenzklasse,
- Unsicherheitsklasse,
- bekannte fachliche Einschränkungen.

Der vollständige Nachweis kann aus dem Feld heraus geöffnet werden.

## Gemeinsamer Szenariozustand

Beide Modi verändern denselben versionierten SGB-II-Vertrag. Der maßgebliche Szenarioausschnitt enthält mindestens:

```text
sgb2.policyVersionId
sgb2.modelVersion
sgb2.populationRunId
sgb2.parameterOverrides
sgb2.housingDatasetOverrides
sgb2.financingOverrides
```

Beim Speichern, Exportieren, Importieren, Duplizieren, Rückgängig-Machen und Wiederherstellen bleibt dieser kanonische Zustand erhalten. Ältere Szenarien mit pauschalen Sozialindizes werden einmalig migriert. Liegt bereits ein expliziter SGB-II-Vertrag vor, darf eine alte Aggregatposition dessen konkrete Werte nicht überschreiben.

**Baseline wiederherstellen** entfernt die SGB-II-Parameter-, Unterkunfts- und Finanzierungs-Overrides. Andere Ausgabenmodule bleiben davon unberührt.

## Live-Neuberechnung

Nach einer Änderung startet mit kurzer Verzögerung eine lokale Neuberechnung in einem eigenen Worker. Ein Seitenneuladen ist nicht erforderlich.

Für jeden simulierten Monat und jede Bedarfsgemeinschaft werden nacheinander berechnet:

1. persönliche Regel- und Mehrbedarfe,
2. Einkommen, Absetzungen und Erwerbstätigenfreibeträge,
3. Einkommensanrechnung innerhalb der Bedarfsgemeinschaft,
4. regional anerkannte Unterkunfts- und Heizkosten,
5. potenzieller und zahlbarer Monatsanspruch,
6. Berücksichtigung des modellierten Bezugsfensters,
7. gewichtete Aggregation nach Leistungsbestandteil und Kostenträger.

Die Mikrodaten verbleiben im lokalen Worker und in IndexedDB. Die sichtbare Anwendung erhält nur die für die Darstellung benötigten Ergebnisse.

Ohne aktiven synthetischen Bevölkerungslauf zeigt die Oberfläche keinen erfundenen Kostenwert, sondern fordert zur Aktivierung oder Erzeugung eines Laufs auf.

## Ergebnisdarstellung

Die Live-Ansicht weist gemeinsam aus:

- Baseline,
- Szenariowert,
- absolute Differenz,
- hochgerechnete betroffene Bedarfsgemeinschaften,
- hochgerechnete betroffene Personen,
- Regelbedarf,
- Mehrbedarfe,
- Unterkunft,
- Heizung,
- Nettofinanzierung nach Bund und kommunalen Trägern,
- Unsicherheitsklasse,
- Rechenweg und Modellgrenzen.

Die Werte werden anschließend konsistent in die Bürgergeld-Ausgabenlinie, die Ausgabenübersicht, den Haushaltssaldo und den Szenarioexport übernommen.

## Kostenträger und Kalibrierung

Die Kostenträgerzuordnung ist von der individuellen Anspruchsberechnung getrennt. Eine geänderte Finanzierungsquote darf den Anspruch der Bedarfsgemeinschaft nicht verändern.

Solange keine landesspezifische Quote hinterlegt ist, wird die bundesweite KdU-Modellquote sichtbar als Annahme gekennzeichnet. Die kommunale Zahlstellenperspektive und die Nettofinanzierungsperspektive bleiben unterscheidbar.

Eine freie Kalibrier- oder Restgröße wird nicht verwendet. Abweichungen zu Statistik- oder Haushaltsreferenzen werden ausgewiesen, aber nicht in das Ergebnis zurückgeschrieben.

## Responsivität und Zugänglichkeit

Die Gruppen- und Expertenansicht sind für Desktop und Mobilgeräte ausgelegt. Eingabefelder besitzen eindeutige Beschriftungen, Modusschalter einen sichtbaren Auswahlzustand und Live-Ergebnisse eine Statusausgabe für laufende oder fehlgeschlagene Berechnungen.

## Modellgrenzen

Die Oberfläche ist keine individuelle Leistungsberatung. Das Ergebnis hängt von der synthetischen Bevölkerung, den verfügbaren Regionaldaten, modellierten Bezugsverläufen und den dokumentierten Fallbacks ab.

Insbesondere gilt:

- fehlende kommunale KdU-Daten erhöhen die Unsicherheit,
- medizinische und verwaltungsrechtliche Einzelfallmerkmale sind nur modelliert, soweit dafür ein expliziter Parameter oder eine Prävalenzannahme besteht,
- Verwaltungskosten, Eingliederungsleistungen und weitere außerhalb der Anspruchsrechnung liegende Positionen werden nicht stillschweigend in den Regelbedarf eingerechnet,
- langfristige Verhaltens- und Arbeitsmarktwirkungen sind nicht Bestandteil dieser unmittelbaren Live-Anspruchsrechnung.

## Verwandte Kapitel

- [Bürgergeld- und Grundsicherungsgeld-Modul](buergergeld-modul.md)
- [Unterkunft und Heizung – Berlin 2026](kdu-berlin-2026.md)
- [Synthetische Bevölkerung](../03-daten/synthetische-bevoelkerung.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
