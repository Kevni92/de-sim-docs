---
title: Synthetische Bevölkerung und Haushalte
summary: Fachliche Beschreibung der Modellbevölkerung, ihrer Merkmale, Datenquellen und Kalibrierung.
status: Arbeitsstand 0.4
last_updated: 2026-07-13
---

# Synthetische Bevölkerung und Haushalte

## Grundkonzept

Es werden nicht 85 Millionen reale Personen gespeichert. Der Simulator nutzt eine gewichtete synthetische Bevölkerung aus Modellpersonen und Modellhaushalten. Ein Datensatz kann beispielsweise 2.400 vergleichbare Haushalte repräsentieren.

## Merkmale

- Alter und Geschlecht,
- Haushaltsform und Partnerschaft,
- Kinderzahl und Alter der Kinder,
- Bundesland und Raumtyp,
- Erwerbsstatus und Arbeitszeit,
- Brutto- und Nettoeinkommen,
- Selbstständigkeit,
- Renten- und Transfereinkommen,
- Miete, Eigentum und Kredit,
- Konsumprofile,
- Vermögen und Schulden,
- Pendelweg,
- Betreuungssituation,
- Gesundheits- und Ausfallrisiken nur in aggregierter, nicht identifizierbarer Form.

## Datenquellen

Der Merkmalskern wird aus mehreren Quellen kalibriert:

- Mikrozensus,
- Einkommensteuerstatistik,
- Einkommens- und Verbrauchsstichprobe,
- SOEP,
- PHF und Distributional Wealth Accounts,
- Statistik der Bundesagentur für Arbeit,
- Regionaldaten und Bevölkerungsfortschreibung.

## Kalibrierung

Gewichte werden so angepasst, dass wichtige Randverteilungen gleichzeitig getroffen werden:

- Bevölkerung nach Alter und Geschlecht,
- Haushaltsgrößen,
- Erwerbsstatus,
- Einkommen,
- Leistungsempfänger,
- regionale Verteilung,
- Steuer- und Beitragsaggregate.

## Datenschutz

Es werden keine echten Einzeldatensätze öffentlich ausgeliefert. Forschungsdaten mit Zugangsbeschränkungen werden nur in zugelassenen Umgebungen verarbeitet; öffentliche Exporte enthalten synthetische oder ausreichend aggregierte Daten.

## Verwandte Kapitel

- [Einnahmen und Steuern](../02-fiskal/einnahmen-und-steuern.md)
- [Demografie und Alterspyramide](../05-module/demografie-und-alterspyramide.md)
- [Evidenzdatenbank](../06-evidenz/evidenzdatenbank.md)
