---
title: Technischer KdU-Modellvertrag
summary: Interner Vertrag für regionale Datensätze, Lookup, Übergangsregeln, Heizkosten und strukturierte KdU-Ergebnisse.
status: Spezifikation 0.1
last_updated: 2026-07-13
---

# Technischer KdU-Modellvertrag

## Zweck

Dieser Vertrag konkretisiert den KdU-Teil des Bürgergeld-Modellvertrags für `de-sim#19`. Der Rechner ist eine reine fachliche Funktion. React-Komponenten, Diagramme und Aggregationslogik dürfen keine eigenen Unterkunfts- oder Heizkostenregeln enthalten.

## Versionen

| Vertrag | Anfangsversion |
|---|---|
| KdU-Datenschema | `1` |
| KdU-Ergebnisschema | `1` |
| KdU-Rechenmodell | `sgb2-housing-0.1.0` |
| Berliner Datensatz | `sgb2-kdu-berlin-2026` |

## Eingaben

```text
calculateSgb2HousingCosts(
  benefitUnit,
  scenarioReference,
  runtimeFacts,
  policyBundle
) -> Sgb2HousingCostResult
```

`runtimeFacts` kann überschreiben oder ergänzen:

- Referenzmonat,
- Region und kommunalen Träger,
- Haushaltsgröße,
- tatsächliche Grundmiete,
- kalte Betriebskosten,
- tatsächliche Heizkosten,
- Wohnfläche,
- Energieträger,
- beheizte Gebäudefläche,
- Leistungsbeginn,
- Beginn eines Kostensenkungszeitraums,
- Härtefallstatus,
- ausdrücklich erzwungenen Datensatz.

Geldwerte werden als ganzzahlige Cent verarbeitet. Zeitwerte verwenden `YYYY-MM`.

## Datensatzvertrag

```text
HousingAllowanceDataset {
  id
  schemaVersion
  regionId
  providerId?
  validFrom
  validTo
  publicationDate
  method
  sourceId
  evidenceClass
  uncertaintyClass
  status
  modelCostIndexParameterId?
  rules[]
  heatingRules[]?
}
```

Eine Größenregel kann Basiswerte für 1 bis 5 Personen und Zuschlagsparameter für weitere Personen enthalten. Eine Heizregel enthält Energieträger, Gebäudeflächenintervall, fünf Betragsparameter und einen Zuschlagsparameter.

## Lookup

Die Auswahl ist stabil und deterministisch:

```text
1. providerId + regionId + month
2. regionId + month
3. longest suitable parent region + month
4. DE model fallback + month
5. error
```

Ein veralteter, aber regional passender Datensatz wird nicht verwendet. Er erscheint in der Fallback-Spur. Ein erzwungener Datensatz muss im Referenzmonat gültig sein.

## Bruttokaltmiete

```text
actualGrossColdRent
  = actualBaseRent + actualColdOperatingCosts
```

Außerhalb besonderer Zeiträume gilt:

```text
recognizedGrossColdRent
  = min(actualGrossColdRent, regionalGrossColdRentLimit)
```

Während der bundesrechtlichen Karenzzeit ab Juli 2026 gilt:

```text
recognizedGrossColdRent
  = min(actualGrossColdRent,
        regionalGrossColdRentLimit × graceCapFactor)
```

Der Baselineparameter `graceCapFactor` ist `1.5`. Ein ausdrücklich aktiver Härtefall oder Kostensenkungszeitraum kann die tatsächlichen Kosten vorübergehend anerkennen. Die Entscheidung muss als Status im Ergebnis erscheinen.

Die anerkannte Bruttokaltmiete wird proportional auf Grundmiete und kalte Betriebskosten zurückverteilt. Restcent werden stabil der Grundmiete zugeordnet.

## Heizkosten

Für einen vollständigen Regionaldatensatz werden Energieträger und beheizte Gebäudefläche gegen die Heizregeln geprüft. Haushaltsgrößen über fünf erhalten den definierten Zuschlag je weiterer Person.

```text
recognizedHeating
  = min(actualHeating, regionalHeatingLimit)
```

Fehlen Energieträger oder Gebäudefläche, darf der Rechner nicht `0` einsetzen. Die tatsächlichen Heizkosten werden als sichtbarer Modell-Fallback anerkannt, die Unsicherheit wird auf `hoch` gesetzt und eine Validierungswarnung erzeugt.

## Deutschland-Fallback

Der projektweite Datensatz besitzt keine behaupteten kommunalen Grenzwerte. Sein Modellindex wird auf die beobachteten tatsächlichen Kosten angewendet:

```text
recognized = min(actual, actual × modelCostIndex / 100)
```

Der Baselineindex `100` vermeidet in der Übergangsphase eine nicht belegte Kürzung. Der Status bleibt `model-fallback`, die Unsicherheit `hoch`. Für fiskalische Veröffentlichungen muss der Anteil der Fallback-Fälle separat ausgewiesen werden.

## Ergebnis

```text
Sgb2HousingCostResult {
  schemaVersion
  modelVersion
  runId
  benefitUnitId
  month
  regionId
  providerId?
  householdSize
  actualBaseRentCents
  actualColdOperatingCostsCents
  actualGrossColdRentCents
  actualHeatingCostsCents
  adequateFloorAreaSquareMeters?
  grossColdRentLimitCents?
  heatingLimitCents?
  recognizedBaseRentCents
  recognizedColdOperatingCostsCents
  recognizedGrossColdRentCents
  recognizedHeatingCostsCents
  recognizedHousingAndHeatingCents
  unrecognizedHousingCents
  unrecognizedHeatingCents
  recognitionStatus
  lookupLevel
  appliedDatasetId
  appliedRuleIds[]
  parameterIds[]
  sourceIds[]
  fallbackTrace[]
  uncertaintyClass
  validationIssues[]
}
```

## Invarianten

- alle Geldwerte sind nichtnegative ganze Cent,
- `actualGrossColdRent = actualBaseRent + actualColdOperatingCosts`,
- anerkannte Beträge überschreiten ohne Härtefall oder Übergangsregel nicht den tatsächlichen Betrag,
- nicht anerkannte Beträge sind tatsächlicher minus anerkannter Betrag,
- anerkannte Grundmiete plus anerkannte kalte Betriebskosten entspricht der anerkannten Bruttokaltmiete,
- ein Regional-Fallback ist im Ergebnis sichtbar,
- ein fehlender Datensatz erzeugt keinen stillen Nullwert,
- gleiche Eingaben und Policy-Versionen erzeugen bytegleich sortierbare Ergebnisse.

## Tests

Pflichtfälle:

- knapp unter, auf und über einer Mietgrenze,
- jede Größenstufe und mindestens eine Stufe über fünf Personen,
- alle Energieträger und Gebäudeflächenintervalle,
- Karenzzeit unter und über dem 1,5-fachen Deckel,
- Kostensenkungszeitraum und Härtefall,
- Regional-, Heizdaten- und vollständiger Fehler-Fallback,
- gezielte Szenario-Overrides,
- negative Beträge und ungültige Monate,
- deterministische Batchreihenfolge,
- Summeninvarianten der Komponenten.

## Weiterverwendung

Der Anspruchsrechner aus `de-sim#18` und der KdU-Rechner bleiben getrennte Kerne. `de-sim#20` führt beide Monatsresultate zusammen, ordnet Kostenträger zu und aggregiert gewichtet. Die UI aus `de-sim#21` konsumiert nur strukturierte Ergebnisse und Parameter.
