---
title: Technischer Vertrag des Einkommensteuer-Moduls
summary: Implementierungsvertrag für Tarifkern, Aggregation, UI-Anbindung und Tests.
status: Arbeitsstand 1.0
last_updated: 2026-07-13
---

# Technischer Vertrag des Einkommensteuer-Moduls

## Schichten

```text
ScenarioDraft.incomeTax
  → income-tax.ts
    → IncomeTaxResult
      → DashboardPage
      → IncomeTaxPage
      → ComparisonPage
      → Transparenzregister
```

Die Seiten implementieren keine eigene Tarif- oder Aufkommensformel. Alle sichtbaren Einkommensteuerwerte werden aus demselben `IncomeTaxResult` abgeleitet.

## Öffentliche Funktionen

`income-tax.ts` stellt mindestens bereit:

- `calculateStatutoryIncomeTax2026(zvE, joint)`,
- `statutoryMarginalRate2026(zvE)`,
- `calculateReformIncomeTax(settings, zvE, joint, partnerShare)`,
- `reformMarginalRate(settings, zvE)`,
- `estimateIncomeTaxRevenue(settings, modelLevel)`.

## Ergebnisvertrag

`IncomeTaxResult` enthält:

- Rechtsstand und Modellstufe,
- Baseline-, statisches und modelliertes Aufkommen,
- statische Wirkung und Verhaltensanpassung,
- Gewinner, Verlierer und nahezu unveränderte Steuerfälle,
- gewichteten Median und Mittelwert,
- Kalibrierungsfaktor,
- Dezilergebnisse,
- Referenzhaushalte,
- Tarifkurvenpunkte.

## Referenzpopulation

Die aktuelle Referenzpopulation wird deterministisch aus zehn Dezilprofilen und fünf Einkommensmultiplikatoren aufgebaut. Jede der 50 Zellen besitzt:

- Dezil,
- zu versteuerndes Einkommen vor Kinderfreibetrag,
- Gewicht,
- Veranlagungsart,
- Partneranteil,
- Kinderzahl.

Die Summe der Gewichte beträgt 42 Millionen Steuerfälle. Der Kalibrierungsfaktor ist ein Bestandteil des Ergebnisses und muss im Nachweis sichtbar bleiben.

## Modellstufen

- `statisch`: kein angepasstes Einkommen,
- `verhalten`: Basissensitivität 0,15,
- `langfrist`: Basissensitivität 0,30.

Der Verhaltenspfad verändert das zu versteuernde Einkommen anhand der relativen Änderung des Nettosatzes. Die Reaktion ist begrenzt. Die statische Berechnung wird unabhängig davon immer ausgeführt und separat zurückgegeben.

## Persistenz und Versionierung

Der Szenariozustand speichert ausschließlich veränderbare Parameter und die Modellstufe. Abgeleitete Werte werden beim Laden neu berechnet.

Aktuelle Modellversion:

```text
income-tax-2026-1.0.0
```

Die lokalen Referenz- und Nachweisdaten werden über den Worker in IndexedDB Version 4 aktualisiert. Die UI greift nicht direkt auf IndexedDB zu.

## Testvertrag

Playwright prüft mindestens:

- 30.000 € Einzelveranlagung → 4.217 €,
- 60.000 € Zusammenveranlagung → 8.434 €,
- gesetzliche Baseline bleibt bei Reformänderungen unverändert,
- Reformwerte reagieren live,
- Aufkommen und Dashboard aktualisieren sich konsistent,
- Nachweise lassen sich öffnen,
- Desktop- und Mobilansicht funktionieren,
- ein echter Screenshot wird im CI-Lauf erzeugt.

## Verwandte Kapitel

- [Einkommensteuer-Modul 2026](../02-fiskal/einkommensteuer-modul.md)
- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Transparenzregister und Metrikvertrag](transparenzregister-und-metrikvertrag.md)
- [Lokaler Worker und Persistenz](lokaler-worker-und-persistenz.md)
