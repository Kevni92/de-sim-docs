---
title: Einkommensteuer-Modul 2026
summary: Gesetzliche Tarifbaseline, synthetische Bevölkerungsaggregation, Reformszenarien und Grenzen des Einkommensteuer-Moduls.
status: Implementiert 1.1
last_updated: 2026-07-13
---

# Einkommensteuer-Modul 2026

## Ziel und Systemgrenze

Das Einkommensteuer-Modul verbindet den gesetzlichen Tarifkern mit der aktiven synthetischen Bevölkerung. Eine Änderung der Tarifparameter aktualisiert konsistent:

- die tarifliche Einkommensteuer eines frei wählbaren Referenzfalls,
- das aggregierte Einkommensteueraufkommen,
- Einnahmen und Haushaltssaldo,
- gewichtete Gewinner und Verlierer,
- Wirkungen nach Einkommensdezilen,
- den gewichteten Median der monatlichen Wirkung,
- illustrative Referenzhaushalte,
- Tarifkurve, Szenariovergleich und Quellennachweis.

Berechnet wird die **tarifliche Einkommensteuer**. Nicht enthalten sind Solidaritätszuschlag, Kirchensteuer, Sozialversicherungsbeiträge, vollständige Werbungskosten und Sonderausgaben sowie die vollständige Günstigerprüfung zwischen Kindergeld und Kinderfreibetrag.

## Gesetzliche Baseline 2026

Baseline ist der Einkommensteuertarif 2026 nach § 32a EStG. Das zu versteuernde Einkommen `x` wird vor Anwendung der Formel auf volle Euro abgerundet.

| Tarifzone | Bereich | Tarifliche Einkommensteuer |
|---|---:|---|
| Grundfreibetrag | `x ≤ 12.348` | `0` |
| erste Progressionszone | `12.349 ≤ x ≤ 17.799` | `(914,51 × y + 1.400) × y`, `y = (x − 12.348) / 10.000` |
| zweite Progressionszone | `17.800 ≤ x ≤ 69.878` | `(173,10 × z + 2.397) × z + 1.034,87`, `z = (x − 17.799) / 10.000` |
| Proportionalzone | `69.879 ≤ x ≤ 277.825` | `0,42 × x − 11.135,63` |
| obere Proportionalzone | `x ≥ 277.826` | `0,45 × x − 19.470,38` |

Das Ergebnis wird auf volle Euro abgerundet.

Bei aktivem Ehegattensplitting gilt:

```text
T_gemeinsam(x) = 2 × T_einzeln(floor(x / 2))
```

Die gesetzliche Tariffunktion bleibt unverändert und wird nicht in der Bevölkerungskomponente dupliziert.

## Parametrisches Reformszenario

Veränderbar sind Grundfreibetrag, Eingangssteuersatz, Spitzensteuersatz, Beginn des Spitzensteuersatzes, Reichensteuersatz, Kinderfreibetrag und Ehegattensplitting.

Der Reformentarif ist ein **Szenariomodell**, kein Gesetzestext. Zwischen Eingangs- und Spitzensteuersatz werden lineare Grenzsteuersatzverläufe verwendet. Oberhalb der gewählten Spitzenschwelle gilt der Spitzensteuersatz; oberhalb der gesetzlichen oberen Schwelle gilt der Reichensteuersatz.

## Tarifprüfung

Die Tarifprüfung nimmt ein frei wählbares zu versteuerndes Einkommen und eine Veranlagungsart entgegen. Ausgegeben werden gesetzliche Steuer, Reformsteuer, jährliche und monatliche Differenz sowie die durchschnittliche Steuerquote.

Referenzwerte der automatisierten Validierung:

| Fall | Gesetzliche Steuer 2026 |
|---|---:|
| 30.000 € zvE, Einzelveranlagung | 4.217 € |
| 50.000 € zvE, Einzelveranlagung | 10.548 € |
| 100.000 € zvE, Einzelveranlagung | 30.864 € |
| 60.000 € gemeinsames zvE, Splitting | 8.434 € |

## Synthetische Bevölkerung und Kalibrierung

Die primäre sichtbare Verteilungsbasis ist seit Milestone 7 der aktive, vollständig synthetische Bevölkerungslauf. Erwachsene werden zu Steuerhaushalten zusammengeführt. Für jeden Haushalt werden gesetzliche und reformierte tarifliche Steuer berechnet und mit dem Haushaltsgewicht aggregiert.

Die Einkommensteuerseite zeigt:

- Lauf-ID,
- synthetische Stichprobengröße,
- gewichtete Bevölkerung,
- Datenstand,
- Modellversion,
- Kalibrierungsstatus.

Der aktive Lauf ist Bestandteil des Szenarios. Ein fehlender Lauf wird sichtbar gemeldet und nicht stillschweigend ersetzt.

Das Aggregataufkommen wird weiterhin auf die im Simulator verwendete Baseline von 358,2 Milliarden Euro normiert:

```text
k = 358,2 Mrd. € / Σ(Haushaltsgewicht_i × gesetzliche Steuer_i)
```

```text
Aufkommen_Szenario = k × Σ(Haushaltsgewicht_i × Reformsteuer_i)
```

Diese Aufkommensnormierung stellt Aggregatkonsistenz her. Die Bevölkerungsgewichte selbst werden getrennt gegen Alters-, Haushalts-, Erwerbs-, Einkommens-, Regional- und Wohnränder kalibriert. Weder die Aufkommensnormierung noch das Raking ersetzen eine amtliche Mikrosimulation.

Die frühere 50-Zellen-Referenzpopulation bleibt als technischer Fallback und Regressionstest erhalten. Sie ist bei vorhandenem Bevölkerungslauf nicht mehr die primäre sichtbare Verteilungsbasis.

## Statische und verhaltensbasierte Wirkung

### Statische Wirkung

Das steuerlich relevante Einkommen bleibt unverändert; nur der Tarif wird ersetzt:

```text
Δ_statisch = Aufkommen_Reform bei konstantem zvE − Aufkommen_Baseline
```

### Verhaltensanpassung

Für die Modellstufen **mit Verhaltenseffekt** und **Langfristszenario** wird das Aufkommen über eine begrenzte Elastizitätsannahme angepasst.

| Modellstufe | Basissensitivität |
|---|---:|
| statisch | 0,00 |
| mit Verhaltenseffekt | 0,15 |
| Langfristszenario | 0,30 |

Die Verhaltenskomponente ist eine explizite Annahme, keine Prognose. Sie wird getrennt von der statischen Erstwirkung angezeigt.

## Verteilungsgrößen

Für jeden gewichteten Steuerhaushalt gilt:

```text
Monatswirkung_i = (Steuer_Baseline_i − Steuer_Reform_i) / 12
```

Als Gewinner gilt ein Haushalt mit mehr als einem Euro Entlastung pro Monat. Als Verlierer gilt ein Haushalt mit mehr als einem Euro Mehrbelastung pro Monat. Dazwischen liegt die Gruppe „nahezu unverändert“.

Ausgegeben werden:

- gewichtete Gewinner, Verlierer und nahezu unveränderte Haushalte,
- gewichtete Mittelwerte nach Einkommensdezil,
- Spanne innerhalb jedes Dezils,
- gewichteter Median und Mittelwert,
- Gewicht der betroffenen Steuerfälle.

## Referenzhaushalte

Vier illustrative Profile bleiben als verständliche Tarifbeispiele sichtbar:

- Single,
- alleinerziehende Person mit einem Kind,
- zusammenveranlagtes Paar mit zwei Kindern,
- alleinstehende Person mit hohem Einkommen.

Diese Profile sind keine Datensätze des aktiven Bevölkerungslaufs, nicht repräsentativ und keine individuelle Steuerberatung.

## Unsicherheit und Interpretation

Die gesetzliche Tarifberechnung ist deterministisch. Unsicherheit entsteht bei:

- synthetischer gemeinsamer Verteilung,
- Haushalts- und Einkommensgewichtung,
- Kalibrierung der Randverteilungen,
- Aufkommensnormierung,
- vereinfachten steuerlichen Merkmalen,
- Verhaltenselastizitäten,
- fehlenden Wechselwirkungen mit Transfers und Sozialbeiträgen.

Daher gilt:

- Tarifwerte bekannter Testfälle sind exakt reproduzierbar.
- Aufkommens- und Verteilungsergebnisse sind Modellrechnungen.
- Kalibrierungswarnungen und Modellgrenzen bleiben sichtbar.
- Verhaltenswerte werden nicht mit der statischen Wirkung vermischt.
- Regionale Wirkungen bleiben bis zu einer fachlich belastbaren Berechnung als **nicht berechnet** gekennzeichnet.

## Validierung

Automatisch geprüft werden:

- bekannte Tarifwerte in wesentlichen Tarifzonen,
- Splitting und Abrundung,
- unveränderliche gesetzliche Baseline,
- deterministische Bevölkerung bei gleichem Seed,
- positive Gewichte und konsistente Haushaltsreferenzen,
- gewichtete Summen und Kalibrierungsbericht,
- Reaktion von Aufkommen, Gewinnern, Verlierern und Dezilen auf Tarifänderungen,
- Wiederherstellung des aktiven Laufs über IndexedDB,
- Desktop- und Mobilansicht.

## Quellen

- [BMF: Berechnung der Einkommensteuer 2026](https://www.bmf-steuerrechner.de/ekst/eingabeformekst.xhtml)
- [Destatis: Lohn- und Einkommensteuerstatistik](https://genesis.destatis.de/datenbank/online/statistic/73111/details)
- [BMF: Datensammlung zur Steuerpolitik](https://www.bundesfinanzministerium.de/Content/DE/Downloads/Broschueren_Bestellservice/datensammlung-zur-steuerpolitik-2026.html)
- [Synthetische Bevölkerung und Haushalte](../03-daten/synthetische-bevoelkerung.md)

## Verwandte Kapitel

- [Einnahmen und Steuern](einnahmen-und-steuern.md)
- [Synthetische Bevölkerung](../03-daten/synthetische-bevoelkerung.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Validierung, Neutralität und Ethik](../09-governance/validierung-governance-ethik.md)
