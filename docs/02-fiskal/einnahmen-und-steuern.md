---
title: Einnahmen und Steuern
summary: Fachliche Anforderungen an Einnahmen-, Steuer- und Beitragsmodule des Simulators.
status: Arbeitsstand 0.5
last_updated: 2026-07-13
---

# Einnahmen und Steuern

## Einkommensteuer

Die Einkommensteuer ist das erste vollständig implementierte Steuer-Modul. Die gesetzliche Baseline, das Reformszenario, die aggregierte Aufkommenswirkung und die Verteilung werden in einem eigenen Kapitel beschrieben:

[Zum Einkommensteuer-Modul 2026](einkommensteuer-modul.md)

Veränderbare Parameter:

- Grundfreibetrag,
- Eingangssteuersatz,
- Progressionszonen,
- Schwelle und Satz des Spitzensteuersatzes,
- Reichensteuersatz,
- Ehegattensplitting,
- kombinierter Kinderfreibetrag.

Ausgegeben werden:

- tarifliche Steuer für Referenzfälle,
- Grenz- und Durchschnittssteuersatz,
- aggregiertes Einkommensteueraufkommen,
- verfügbare Einkommensänderung,
- Gewinner und Verlierer,
- Wirkung nach Einkommensdezil,
- getrennte statische und verhaltensbasierte Wirkung.

Noch nicht enthalten sind Werbungskosten, Rentenbesteuerung, Kapitalertragsteuer, Solidaritätszuschlag, Kirchensteuer, Sozialbeiträge und die vollständige Günstigerprüfung mit Kindergeld. Diese Grenzen werden in der Oberfläche und im Nachweis ausdrücklich ausgewiesen.

## Vermögen- und Erbschaftsteuern

Das Modell benötigt:

- Freibeträge,
- Steuersätze und Progression,
- Verwandtschaftsgrade,
- Immobilien- und Betriebsvermögen,
- Verschonungsregeln,
- Bewertungsabschläge,
- Aufkommens- und Ausweichannahmen.

Topvermögen werden nicht aus normalen Haushaltsbefragungen allein abgeleitet. Eine eigene Topvermögens-Korrektur mit konservativem, mittlerem und hohem Szenario ist erforderlich.

## Konsumsteuern

- Regel- und ermäßigter Umsatzsteuersatz,
- Produktgruppen,
- Energiesteuern,
- Stromsteuer,
- Tabak- und Alkoholsteuern,
- CO2-Bepreisung,
- Luftverkehrsteuer,
- Kraftfahrzeugsteuer.

Konsumsteuern werden über haushaltsspezifische Ausgabenprofile modelliert. Eine reine Multiplikation mit dem Gesamtkonsum reicht nicht aus.

## Unternehmens- und Kommunalsteuern

- Körperschaftsteuer,
- Gewerbesteuer,
- Verlustverrechnung,
- Investitionsanreize,
- Abschreibungsregeln,
- Quellensteuern.

Verhaltensreaktionen von Unternehmen werden als eigenes Szenario geführt. Sie dürfen die statische Erstwirkung nicht verdecken.

## Sozialbeiträge und sonstige Einnahmen

- Renten-, Kranken-, Pflege- und Arbeitslosenversicherung,
- Beitragsbemessungsgrenzen,
- Arbeitgeber- und Arbeitnehmeranteile,
- Gebühren,
- Dividenden staatlicher Beteiligungen,
- Zölle,
- Kreditaufnahme.

## Gemeinsame Regeln aller Einnahmenmodule

Jedes Modul muss:

1. gesetzliche oder statistische Baseline und Szenario trennen,
2. statische Erstwirkung vor Verhaltenseffekten zeigen,
3. aggregierte Werte aus derselben Logik wie die Einzelfallansicht ableiten,
4. Datenstand, Rechtsstand und Modellversion ausweisen,
5. nicht berechnete Größen als nicht berechnet kennzeichnen,
6. Rechenweg, Quellen, Unsicherheit und bekannte Grenzen öffnen können.

## Verwandte Kapitel

- [Einkommensteuer-Modul 2026](einkommensteuer-modul.md)
- [Systemgrenze und Baseline](systemgrenze-und-baseline.md)
- [Synthetische Bevölkerung](../03-daten/synthetische-bevoelkerung.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
