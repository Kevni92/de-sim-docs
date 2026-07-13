---
title: Einkommensteuer-Modul 2026
summary: Gesetzliche Tarifbaseline, Reformszenarien, Aggregation und Grenzen des ersten vollständigen Steuer-Moduls.
status: Arbeitsstand 1.0
last_updated: 2026-07-13
---

# Einkommensteuer-Modul 2026

## Ziel und Systemgrenze

Das Einkommensteuer-Modul ist der erste vollständige vertikale Modellpfad des Deutschland-Simulators. Eine Änderung der Tarifparameter aktualisiert konsistent:

- die tarifliche Einkommensteuer eines Referenzfalls,
- das aggregierte Einkommensteueraufkommen,
- Einnahmen und Haushaltssaldo,
- Gewinner und Verlierer,
- Wirkungen nach Einkommensdezilen,
- ausgewählte Referenzhaushalte,
- Tarifkurve und Szenariovergleich,
- den zugehörigen Rechen- und Quellennachweis.

Die derzeitige Fassung berechnet die **tarifliche Einkommensteuer**. Nicht enthalten sind Solidaritätszuschlag, Kirchensteuer, Sozialversicherungsbeiträge, Werbungskosten, Sonderausgaben sowie die vollständige Günstigerprüfung zwischen Kindergeld und Kinderfreibetrag.

## Gesetzliche Baseline 2026

Baseline ist der Einkommensteuertarif 2026 nach § 32a EStG. Das zu versteuernde Einkommen `x` wird vor Anwendung der Formel auf volle Euro abgerundet.

### Einzelveranlagung

Für `x` in Euro gilt:

| Tarifzone | Bereich | Tarifliche Einkommensteuer |
|---|---:|---|
| Grundfreibetrag | `x ≤ 12.348` | `0` |
| erste Progressionszone | `12.349 ≤ x ≤ 17.799` | `(914,51 × y + 1.400) × y`, mit `y = (x − 12.348) / 10.000` |
| zweite Progressionszone | `17.800 ≤ x ≤ 69.878` | `(173,10 × z + 2.397) × z + 1.034,87`, mit `z = (x − 17.799) / 10.000` |
| Proportionalzone | `69.879 ≤ x ≤ 277.825` | `0,42 × x − 11.135,63` |
| obere Proportionalzone | `x ≥ 277.826` | `0,45 × x − 19.470,38` |

Das Ergebnis wird auf volle Euro abgerundet.

### Zusammenveranlagung

Bei aktivem Ehegattensplitting wird die tarifliche Steuer auf die Hälfte des gemeinsamen zu versteuernden Einkommens angewendet und anschließend verdoppelt:

```text
T_gemeinsam(x) = 2 × T_einzeln(floor(x / 2))
```

Die Anwendung trennt die unveränderliche gesetzliche Baseline sichtbar vom frei parametrierbaren Reformszenario.

## Parametrisches Reformszenario

Veränderbar sind:

- Grundfreibetrag,
- Eingangssteuersatz,
- Spitzensteuersatz,
- Beginn des Spitzensteuersatzes,
- Reichensteuersatz,
- kombinierter Kinderfreibetrag je Kind,
- Ehegattensplitting.

Der Reformentarif ist eine stetige, stückweise Funktion. Zwischen Eingangs- und Spitzensteuersatz werden lineare Grenzsteuersatzverläufe verwendet. Oberhalb der frei gewählten Spitzenschwelle gilt der Spitzensteuersatz; oberhalb der gesetzlichen oberen Schwelle gilt der Reichensteuersatz.

Der Reformentarif ist ein **Szenariomodell**, kein Gesetzestext. Die gesetzliche Tarifformel wird nicht durch die Parametrisierung überschrieben.

## Tarifprüfung in der Oberfläche

Die Tarifprüfung nimmt ein frei wählbares zu versteuerndes Einkommen und eine Veranlagungsart entgegen. Ausgegeben werden:

1. tarifliche Steuer nach Gesetz 2026,
2. tarifliche Steuer im Reformszenario,
3. jährliche und monatliche Differenz des verfügbaren Einkommens,
4. durchschnittliche Steuerquote beider Varianten.

Referenzwerte der automatisierten Validierung:

| Fall | Gesetzliche Steuer 2026 |
|---|---:|
| 30.000 € zu versteuerndes Einkommen, Einzelveranlagung | 4.217 € |
| 50.000 € zu versteuerndes Einkommen, Einzelveranlagung | 10.548 € |
| 100.000 € zu versteuerndes Einkommen, Einzelveranlagung | 30.864 € |
| 60.000 € gemeinsames zu versteuerndes Einkommen, Splitting | 8.434 € |

## Referenzpopulation und Kalibrierung

Die aktuelle Aggregation verwendet noch keine synthetische Bevölkerung auf Mikrodatenbasis. Sie arbeitet mit einer transparenten Referenzpopulation:

- zehn Einkommensdezile,
- fünf Einkommenspunkte je Dezil,
- insgesamt 50 Modellzellen,
- Gewichte für zusammen 42 Millionen Steuerfälle,
- vereinfachte Merkmale für Zusammenveranlagung und Kinder.

Für jede Zelle wird die gesetzliche Baseline berechnet. Anschließend wird ein einheitlicher Kalibrierungsfaktor bestimmt:

```text
k = 358,2 Mrd. € / Σ(Gewicht_i × gesetzliche Steuer_i)
```

Damit reproduziert die Referenzpopulation das im Simulator verwendete Baseline-Aufkommen von 358,2 Milliarden Euro. Das Szenarioaufkommen lautet:

```text
Aufkommen_Szenario = k × Σ(Gewicht_i × Reformsteuer_i)
```

Die Kalibrierung stellt Aggregatkonsistenz her. Sie ersetzt keine repräsentativen Einzelfalldaten und keine amtliche Mikrosimulation.

## Statische und verhaltensbasierte Wirkung

Die Anwendung weist zwei Komponenten getrennt aus.

### Statische Wirkung

Das zu versteuernde Einkommen jeder Modellzelle bleibt unverändert. Nur der Tarif wird ersetzt:

```text
Δ_statisch = Aufkommen_Reform bei konstantem zvE − Aufkommen_Baseline
```

### Verhaltensanpassung

Für die Modellstufen **mit Verhaltenseffekt** und **Langfristszenario** wird das zu versteuernde Einkommen über eine Elastizitätsannahme angepasst. Maßgeblich ist die Änderung des Nettosatzes nach Steuern.

Verwendete Basissensitivitäten:

| Modellstufe | Basissensitivität |
|---|---:|
| statisch | 0,00 |
| mit Verhaltenseffekt | 0,15 |
| Langfristszenario | 0,30 |

Für höhere Einkommen wird die Sensitivität erhöht. Reaktionen werden begrenzt, damit einzelne Modellzellen keine unplausiblen Sprünge erzeugen.

Diese Komponente ist eine **explizite Szenarioannahme**. Sie ist keine Prognose und wird getrennt von der statischen Erstwirkung angezeigt.

## Verteilungsgrößen

Für jede Modellzelle wird die monatliche Änderung berechnet:

```text
Monatswirkung_i = (Steuer_Baseline_i − Steuer_Reform_i) / 12
```

Als Gewinner gilt ein Steuerfall mit mehr als einem Euro Entlastung pro Monat. Als Verlierer gilt ein Steuerfall mit mehr als einem Euro Mehrbelastung pro Monat. Dazwischen liegt die Gruppe „nahezu unverändert“.

Die Dezilwerte sind gewichtete Mittelwerte. Zusätzlich zeigt das Modul den gewichteten Median und die Spanne der fünf Referenzpunkte je Dezil.

## Referenzhaushalte

Vier illustrative Profile machen die Tarifwirkung verständlich:

- Single,
- alleinerziehende Person mit einem Kind,
- zusammenveranlagtes Paar mit zwei Kindern,
- alleinstehende Person mit hohem Einkommen.

Für jedes Profil werden gesetzliche Jahressteuer, Reformsteuer und monatliche Differenz angezeigt. Die Profile sind nicht repräsentativ und stellen keine individuelle Steuerberatung dar.

## Unsicherheit und Interpretation

Die gesetzliche Tarifberechnung ist deterministisch. Unsicherheit entsteht erst bei:

- Verteilung und Gewichtung der Referenzpopulation,
- Kalibrierung des Aggregataufkommens,
- vereinfachten Haushaltsmerkmalen,
- Verhaltenselastizitäten,
- fehlenden Wechselwirkungen mit Transfers und Sozialbeiträgen.

Daher gilt:

- Tarifwerte einzelner Testfälle können exakt reproduziert werden.
- Aufkommens- und Verteilungsergebnisse sind Modellrechnungen.
- Verhaltenswerte werden niemals mit der statischen Wirkung vermischt.
- Regionale Wirkungen werden bis zur Anbindung geeigneter Daten als **nicht berechnet** ausgewiesen.

## Validierung

Die automatisierte Validierung umfasst:

- bekannte Referenzwerte in allen wesentlichen Tarifzonen,
- Splittingberechnung,
- Abrundung auf volle Euro,
- unveränderliche gesetzliche Baseline bei Änderungen des Reformszenarios,
- identische Ergebniswerte in Detailseite, Dashboard und Transparenzregister,
- responsive Bedienung auf Desktop und Mobilgeräten.

Die Referenzwerte werden mit dem offiziellen Einkommensteuerrechner des Bundesministeriums der Finanzen gegengeprüft.

## Quellen

- [BMF: Berechnung der Einkommensteuer 2026](https://www.bmf-steuerrechner.de/ekst/eingabeformekst.xhtml)
- [Destatis: Lohn- und Einkommensteuerstatistik](https://genesis.destatis.de/datenbank/online/statistic/73111/details)
- [BMF: Datensammlung zur Steuerpolitik](https://www.bundesfinanzministerium.de/Content/DE/Downloads/Broschueren_Bestellservice/datensammlung-zur-steuerpolitik-2026.html)

## Verwandte Kapitel

- [Einnahmen und Steuern](einnahmen-und-steuern.md)
- [Synthetische Bevölkerung](../03-daten/synthetische-bevoelkerung.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Validierung, Neutralität und Ethik](../09-governance/validierung-governance-ethik.md)
