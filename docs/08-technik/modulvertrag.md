---
title: Vertrag eines Simulationsmoduls
summary: Einheitliche Schnittstelle für Eingaben, Ausgaben, Evidenz und Tests.
status: Entwurf
last_updated: 2026-07-13
---

# Vertrag eines Simulationsmoduls

Jedes Fachmodul muss unabhängig prüfbar und austauschbar sein.

## Eingaben

- Baseline-ID und Rechtsstand,
- Policy Lever mit altem und neuem Wert,
- Population oder Aggregate,
- Zeitraum und Preisbasis,
- aktivierte Verhaltens- und Szenarioannahmen,
- Daten- und Parameterversionen.

## Ausgaben

- zentrale Schätzung und Bandbreite,
- Einheit, Zeitraum und staatliche Ebene,
- betroffene Personen oder Haushalte,
- direkte, indirekte und langfristige Ergebnisse getrennt,
- Evidenzstatus, Quellen-IDs und Rechenbaum-ID,
- Warnungen bei Extrapolation oder fehlenden Daten.

## Fehlerzustände

Zulässig sind `not_applicable`, `insufficient_data`, `unsupported_combination`, `outside_validity_range` und `calculation_failed`. Ein Modul darf fehlende Daten niemals durch eine Fantasiezahl ersetzen.

## Tests

Referenzfälle, Grenzwerttests, Aggregatabgleich, Regressionstests, Prüfungen gegen Doppelzählung und reproduzierbare Zufallsseeds sind verpflichtend.

## Verwandte Kapitel

- [Technische Architektur](technische-architektur.md)
- [Definition of Done](../10-roadmap/mvp-und-roadmap.md#definition-of-done-fur-ein-modul)
- [Evidenzschema](../06-evidenz/evidenzschema.md)
