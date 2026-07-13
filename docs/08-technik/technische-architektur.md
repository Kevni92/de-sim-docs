---
title: Technische Architektur
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.3
last_updated: 2026-07-13
---

# 18. Technische Architektur

## 18.1 Komponenten

1. Web-Frontend,
2. Szenario- und Benutzerprofilservice,
3. statische Mikrosimulationsengine,
4. dynamische Wirkungsengine,
5. Demografieengine,
6. Evidenz- und Provenienzdatenbank,
7. Datenpipeline und Versionierung,
8. Export- und Reproduzierbarkeitsservice.

## 18.2 Rechenkern

Für Steuer- und Transferregeln sind regelbasierte, testbare Modelle erforderlich. OpenFisca oder GETTSIM können geprüft werden. EUROMOD ist ein wichtiger methodischer Referenzpunkt für statische Steuer- und Transfersimulationen. Dynamische Verhaltens- und Demografiemodule bleiben getrennt, damit statische und spekulativere Ergebnisse nicht vermischt werden.

## 18.3 Datenhaltung

Empfohlene Trennung:

- relationale Metadatenbank,
- versionierter Objektspeicher für Rohdaten und Exporte,
- analytische Spaltenformate für Modellhaushalte,
- Graphdarstellung für Wirkungsketten,
- unveränderliches Laufprotokoll.

## 18.4 Versionierung

Jeder Lauf referenziert:

- Szenarioversion,
- Regelversion,
- Datenversion,
- Parameterversion,
- Code-Commit,
- Zufallsseed bei stochastischen Läufen.

## 18.5 Berechnungsmodus

- schnelle Live-Vorschau mit aggregierten Elastizitäten,
- präziser statischer Modelllauf im Hintergrund,
- optionaler Langfristszenariolauf,
- Vergleich der Unterschiede zwischen den Stufen.

## 18.6 API

Die interne API liefert nicht nur Ergebniswerte, sondern auch Metadaten:

- Einheit,
- Preisjahr,
- staatliche Ebene,
- Quellen-IDs,
- Unsicherheitsstatus,
- Rechenbaum-ID.

## 18.7 Testbarkeit

Jede Regel erhält Referenzfälle. Aggregate werden gegen amtliche Statistiken validiert. Änderungen am Rechenkern müssen automatische Regressionstests bestehen.

## Verwandte Kapitel

- [Synthetische Bevölkerung und Haushalte](../03-daten/synthetische-bevoelkerung.md)
- [Evidenzdatenbank und Quellenprovenienz](../06-evidenz/evidenzdatenbank.md)
- [Validierung, Governance und Ethik](../09-governance/validierung-governance-ethik.md)
