---
title: Einnahmen und Steuern
summary: Fachliche Anforderungen und aktueller Ausbaustand der Einnahmen-, Steuer- und Beitragsmodule.
status: Arbeitsstand 0.6
last_updated: 2026-07-13
---

# Einnahmen und Steuern

Der Simulator enthält einen gemeinsamen fachlichen Rahmen für Einnahmen. Gesetzliche Baseline, Szenarioparameter, statische Erstwirkung, Verhaltenskomponente, Unsicherheit und Quellen werden getrennt ausgewiesen.

## Implementierter Ausbaustand

### Einkommensteuer

Die Einkommensteuer ist als tarifbasiertes Modul mit gesetzlicher Baseline 2026, Referenzpopulation, Aufkommensaggregation und Verteilungsdarstellung umgesetzt.

[Zum Einkommensteuer-Modul 2026](einkommensteuer-modul.md)

Veränderbar sind Grundfreibetrag, Eingangs-, Spitzen- und Reichensteuersatz, Tarifschwelle, Ehegattensplitting und Kinderfreibetrag. Ausgegeben werden Tarifsteuer, Grenz- und Durchschnittssteuersatz, Aufkommen, Gewinner und Verlierer, Dezile sowie Referenzhaushalte.

### Weitere Einnahmen

Milestone 5 ergänzt folgende Aggregatmodule:

- Umsatzsteuer,
- Erbschaft- und Schenkungsteuer,
- Vermögensteuer als hypothetisches Szenario mit Null-Baseline,
- Sozialversicherungsbeiträge,
- Körperschaftsteuer,
- Kapitalertragsteuer,
- Energie- und Verbrauchsteuern.

[Zu den weiteren Einnahmemodulen](weitere-einnahmemodule.md)

Alle sieben Module verwenden denselben Bedien- und Transparenzvertrag, behalten aber ihre unterschiedlichen Steuerobjekte, Bemessungsgrundlagen und Unsicherheiten.

## Noch nicht vollständig umgesetzt

Folgende Bereiche benötigen weitere fachliche Vertiefung oder eigene Module:

- Gewerbesteuer und kommunale Hebesätze,
- Grundsteuer,
- Zölle, Gebühren und staatliche Beteiligungserträge,
- CO₂-Bepreisung außerhalb der Verbrauchsteuerindizes,
- Luftverkehr- und Kraftfahrzeugsteuer,
- vollständige Unternehmensbesteuerung einschließlich Gewerbesteuer, Organschaften und Mindeststeuer,
- detaillierte Produktgruppen und Konsumprofile,
- vollständige Verteilung der Sozialbeiträge auf Personengruppen,
- Wechselwirkungen zwischen Steuern, Beiträgen, Preisen, Löhnen und Transfers.

## Gemeinsame Regeln aller Einnahmenmodule

Jedes Modul muss:

1. gesetzliche oder statistische Baseline und Szenario trennen,
2. statische Erstwirkung vor Verhaltenseffekten zeigen,
3. Verhaltensreaktionen als Annahme und nicht als sichere Prognose kennzeichnen,
4. aggregierte Werte aus derselben Logik wie die Detailansicht ableiten,
5. Datenstand, Rechtsstand und Modellversion ausweisen,
6. nicht berechnete Größen als nicht berechnet kennzeichnen,
7. Rechenweg, Quellen, Unsicherheit, Inzidenz und bekannte Grenzen öffnen können,
8. Szenarioparameter verlustfrei speichern, laden, exportieren und importieren.

## Methodische Trennung

Die aktuelle Implementierung umfasst zwei unterschiedliche Reifestufen:

- Die Einkommensteuer verwendet einen gesetzlichen Tarifkern und eine kalibrierte Referenzpopulation.
- Die weiteren Einnahmen verwenden transparente Aggregatmodelle mit kalibrierten Ausgangswerten und expliziten Annahmen.

Ergebnisse dieser Stufen dürfen nicht ohne Kennzeichnung miteinander gleichgesetzt werden. Insbesondere sind Inzidenzangaben der zusätzlichen Module noch keine repräsentativen Haushaltsverteilungsrechnungen.

## Verwandte Kapitel

- [Einkommensteuer-Modul 2026](einkommensteuer-modul.md)
- [Weitere Einnahmemodule](weitere-einnahmemodule.md)
- [Systemgrenze und Baseline](systemgrenze-und-baseline.md)
- [Synthetische Bevölkerung](../03-daten/synthetische-bevoelkerung.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
