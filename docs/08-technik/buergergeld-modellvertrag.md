---
title: Technischer Modellvertrag – Bürgergeld
summary: Interner Vertrag für Datenmodelle, monatliche Anspruchsberechnung, Unterkunft und Heizung, Aggregation, Kalibrierung, Szenarien und Tests.
status: Spezifikation 0.1
last_updated: 2026-07-13
---

# Technischer Modellvertrag – Bürgergeld

## Zweck

Dieser Vertrag übersetzt die fachliche Spezifikation des Bürgergeld- beziehungsweise Grundsicherungsgeld-Moduls in stabile technische Grenzen. Er ist die Grundlage für die Anwendungs-Issues `de-sim#16` bis `de-sim#22`.

Die Implementierung wird in getrennten Pull Requests aufgebaut. Keine React-Komponente darf eigene Leistungslogik enthalten.

## Architekturgrenzen

Die Zielarchitektur besteht aus:

1. versionierten Politik- und Quelldaten,
2. SGB-II-relevanten Merkmalen der synthetischen Bevölkerung,
3. einer deterministischen Ableitung von Bedarfsgemeinschaften,
4. einem monatlichen Anspruchsrechner,
5. einem getrennten KdU-Rechner,
6. einer Aggregations- und Kostenträgerschicht,
7. einer Kalibrierungs- und Abgleichsschicht,
8. einer UI, die ausschließlich kanonische Parameter und strukturierte Ergebnisse verwendet.

Der Anspruchsrechner kennt keine UI-Indizes, Diagramme, React-Zustände oder Haushaltsbudgettitel. Die Kostenträgerschicht verändert keinen individuellen Anspruch.

## Versionsstrategie

Mindestens folgende Versionen sind getrennt zu führen:

| Vertrag | Anfangsversion |
|---|---:|
| SGB-II-Policy-Schema | `1` |
| SGB-II-Populationsschema | `1` |
| SGB-II-Rechenmodell | `sgb2-0.1.0` |
| KdU-Datenschema | `1` |
| SGB-II-Ergebnisschema | `1` |
| Szenario-JSON | nächste freie Gesamtversion |

Eine Änderung an Berechnungsreihenfolge, Rundung, Fallzuordnung oder Interpretation erhöht die Rechenmodellversion. Reine Quellenmetadaten ohne Ergebniswirkung erhöhen nur die Datensatzversion.

## Grundeinheiten

Intern gelten:

- Geldbeträge als ganzzahlige Cent,
- Prozentsätze als Dezimalzahl mit dokumentierter Präzision,
- Zeit als Kalendermonat `YYYY-MM`,
- Flächen in Quadratmetern,
- Gewichte als endliche positive Dezimalzahlen,
- Regionen über stabile amtliche oder projektinterne Kennungen.

Fließkommazahlen dürfen nicht als fachliche Geldquelle dienen. Konvertierungen in Euro erfolgen nur an Ein- und Ausgabeschichten.

## Kerntypen

### `Sgb2PolicyVersion`

```text
Sgb2PolicyVersion {
  id
  name
  legalStatusDate
  validFrom
  validTo
  terminology
  schemaVersion
  modelVersion
  parameterIds[]
  sourceIds[]
  changeNotes[]
}
```

### `Sgb2Parameter<T>`

```text
Sgb2Parameter<T> {
  id
  value: T
  unit
  validFrom
  validTo
  legalStatusDate
  dataStatusDate?
  sourceId
  evidenceClass
  uncertaintyClass
  roundingRule
  notes?
}
```

Parameter-IDs bleiben über Versionen stabil. Ein Wert ohne Einheit, Gültigkeitszeitraum und Quelle ist ungültig.

### `Sgb2PersonFacts`

```text
Sgb2PersonFacts {
  personId
  householdId
  referenceMonth
  age
  householdRole
  relationshipIds
  employableStatus
  eligibilityStatus
  pregnancyFacts?
  disabilityFacts?
  warmWaterFacts?
  incomeItems[]
  deductionItems[]
  priorityBenefitItems[]
  assetItems[]
  personWeight
}
```

### `Sgb2HouseholdFacts`

```text
Sgb2HouseholdFacts {
  householdId
  referenceMonth
  memberIds[]
  regionId
  municipalityProviderId?
  housingTenure
  moveInMonth?
  benefitStartMonth?
  floorAreaSquareMeters?
  baseRentCents
  coldOperatingCostsCents
  heatingCostsCents
  warmWaterMode
  householdWeight
}
```

### `Sgb2BenefitUnit`

```text
Sgb2BenefitUnit {
  benefitUnitId
  householdId
  referenceMonth
  memberIds[]
  eligibleMemberIds[]
  nonEligibleMemberIds[]
  type
  weight
  derivationTrace[]
}
```

Die Ableitung einer Bedarfsgemeinschaft ist deterministisch. Gleiche Personen- und Haushaltsdaten erzeugen bei gleicher Policy-Version dieselbe Zugehörigkeit.

## Regelbedarfsvertrag

```text
StandardNeedRule {
  id
  priority
  eligibilityPredicate
  monthlyAmountCents
  sourceId
}
```

Genau eine Regelbedarfsregel muss für jede relevante Person zutreffen. Keine oder mehrere Treffer sind Validierungsfehler.

Der Betrag wird dem Personenresultat direkt zugeordnet. Alters- oder Rollenwechsel werden pro Referenzmonat ausgewertet.

## Mehrbedarfsvertrag

```text
AdditionalNeedRule {
  id
  eligibilityPredicate
  basis
  rate?
  fixedAmountCents?
  startRule
  endRule
  capGroup?
  capRule?
  sourceId
  uncertaintyClass
}
```

Ablauf:

1. Voraussetzungen pro Person und Monat prüfen.
2. Rohbetrag je Regel berechnen.
3. individuelle Begrenzung anwenden.
4. gemeinsame Obergrenze je `capGroup` anwenden.
5. Restcent-Verteilung durchführen.
6. strukturierte Zwischenwerte speichern.

Das Ergebnis enthält angewandte und abgelehnte Regeln einschließlich Begründung.

## Einkommensvertrag

### Eingangsobjekt

```text
IncomeItem {
  id
  personId
  month
  type
  grossCents
  netCents?
  privilegedStatus
  sourceOrAssumptionId
}
```

### Absetzungen

```text
IncomeDeductionRule {
  id
  appliesToIncomeTypes[]
  predicate
  calculationType
  amountOrRate
  lowerBoundCents?
  upperBoundCents?
  priority
  sourceId
}
```

### Tarifsegmente für Erwerbstätigenfreibeträge

```text
EarnedIncomeAllowanceSegment {
  id
  lowerExclusiveCents
  upperInclusiveCents?
  rate
  childRelatedUpperBound?
  sourceId
}
```

Berechnungsreihenfolge:

```text
1. Einkommen klassifizieren
2. gesetzlich nicht zu berücksichtigende Einnahmen entfernen
3. Steuern und Pflichtbeiträge bestimmen
4. allgemeine und besondere Absetzungen anwenden
5. Erwerbstätigenfreibetrag segmentweise berechnen
6. personengebundenes anrechenbares Einkommen bilden
7. Einkommenszuordnung auf Bedarfe und Personen anwenden
8. nicht verbrauchte Beträge nach gesetzlicher Reihenfolge verteilen
```

Jeder Schritt liefert Betrag vor und nach Anwendung sowie Regel-ID.

## Vermögensvertrag

```text
AssetEligibilityResult {
  personResults[]
  benefitUnitTotalCents
  allowanceTotalCents
  protectedAssetTotalCents
  countableAssetTotalCents
  status
  appliedRuleIds[]
  uncertaintyClass
}
```

Mögliche Statuswerte:

- `eligible`
- `excluded_by_assets`
- `indeterminate_missing_facts`

Die Anspruchsberechnung darf bei `indeterminate_missing_facts` nicht still einen sicheren Anspruch ausgeben. Der Szenariolauf kann mit Warnung fortgesetzt werden, muss diesen Teil aber gesondert kennzeichnen.

## KdU-Datenvertrag

### Regionaler Datensatz

```text
HousingAllowanceDataset {
  id
  regionId
  providerId?
  validFrom
  validTo
  publicationDate
  method
  sourceId
  evidenceClass
  rules[]
}
```

### Regel

```text
HousingAllowanceRule {
  householdSizeMin
  householdSizeMax?
  adequateFloorArea?
  grossColdRentLimitCents?
  baseRentLimitCents?
  coldOperatingCostLimitCents?
  maxRentPerSquareMeterCents?
  heatingLimitModelId?
  hardshipRuleIds[]
}
```

### Lookup-Reihenfolge

1. exakter kommunaler Träger und Referenzmonat,
2. exakte Region und Referenzmonat,
3. übergeordnete Region mit expliziter Eignung,
4. fachlich dokumentierter Modell-Fallback,
5. fehlender Wert mit Fehlerstatus.

Ein Fallback enthält Ursprung, Begründung und erhöhte Unsicherheitsklasse. Ein fehlender Datensatz führt niemals zu `0` anerkannten Kosten.

## KdU-Rechenvertrag

```text
HousingCostResult {
  actualBaseRentCents
  actualColdOperatingCostsCents
  actualGrossColdRentCents
  actualHeatingCostsCents
  recognizedBaseRentCents
  recognizedColdOperatingCostsCents
  recognizedGrossColdRentCents
  recognizedHeatingCostsCents
  unrecognizedHousingCents
  unrecognizedHeatingCents
  appliedDatasetId
  appliedRuleIds[]
  fallbackTrace[]
  uncertaintyClass
}
```

Die Berechnung berücksichtigt mindestens:

- Bedarfsgemeinschafts- beziehungsweise Haushaltsgröße,
- regionale Grenze,
- Wohnfläche und optionale Quadratmeterhöchstmiete,
- Bezugsbeginn und Karenzstatus,
- Übergangs- und Kostensenkungszeitraum,
- Härtefallstatus,
- Heizkostenmodell, Fläche und Energieträger, sofern verfügbar.

Die Aufteilung gemeinsamer Wohnkosten auf mehrere Bedarfsgemeinschaften erfolgt über eine versionierte Regel. Der Standard darf nicht implizit aus der UI stammen.

## Monatlicher Anspruchsvertrag

### Hauptfunktion

```text
calculateMonthlySgb2Entitlement(
  policy,
  persons,
  household,
  benefitUnit,
  housingDatasets
) -> MonthlySgb2Result
```

### Reihenfolge

1. Eingaben und Gültigkeitszeiträume validieren.
2. Bedarfsgemeinschaft und grundsätzliche Berechtigung prüfen.
3. Vermögensstatus bestimmen.
4. Regelbedarf je Person bestimmen.
5. Mehrbedarfe je Person bestimmen und begrenzen.
6. Unterkunft und Heizung bestimmen.
7. Bruttobedarf je Person, Komponente und Bedarfsgemeinschaft bilden.
8. Einkommen, Absetzungen und Freibeträge berechnen.
9. vorrangige Leistungen zuordnen.
10. Einkommen nach gesetzlicher Reihenfolge auf Bedarfe verteilen.
11. Anspruch vor Minderung bestimmen.
12. Leistungsminderungen getrennt anwenden.
13. Restcent-Verteilung durchführen.
14. Ergebnisvalidierung und Erklärspur erzeugen.

### Ergebnis

```text
MonthlySgb2Result {
  benefitUnitId
  month
  policyVersionId
  modelVersion
  eligibilityStatus
  grossNeedCents
  standardNeedCents
  additionalNeedCents
  recognizedHousingCents
  recognizedHeatingCents
  countableIncomeCents
  priorityBenefitCents
  entitlementBeforeReductionCents
  reductionCents
  paymentEntitlementCents
  personResults[]
  componentResults[]
  housingResult
  assetResult
  calculationTrace[]
  validationIssues[]
  sourceIds[]
  uncertaintyClass
}
```

## Rundungsvertrag

- Geld wird intern in Cent geführt.
- Prozentbasierte Zwischenwerte werden mit der Regel des jeweiligen Parameters gerundet.
- Segmentberechnungen werden nicht vorzeitig auf volle Euro gerundet.
- Die Summe der Personen- und Komponentenresultate muss dem Bedarfsgemeinschaftsergebnis entsprechen.
- Restcent werden über eine stabile Regel verteilt, zum Beispiel nach absteigender ungerundeter Restgröße und anschließend stabiler Personen-ID.
- Ein Wechsel der Restcent-Regel erhöht die Modellversion.

## Aggregationsvertrag

```text
aggregateSgb2Results(
  monthlyResults,
  weightingContext,
  financingPolicy
) -> Sgb2AggregateResult
```

Ausgaben entstehen ausschließlich aus Monatsresultaten:

```text
weightedAmount = resultAmount × benefitUnitWeight
annualAmount = Summe der gewichteten Monatsbeträge
```

Aggregierbare Dimensionen:

- Leistungsbestandteil,
- Kostenträger,
- Bedarfsgemeinschaftstyp,
- Personengruppe,
- Bundesland und Region,
- Einkommensdezil,
- Erwerbsstatus,
- Bezugsmonat,
- Unsicherheitsklasse,
- verwendeter KdU-Datensatz beziehungsweise Fallback.

Unterstützte Maße:

- gewichtete Anzahl,
- Anteil,
- Summe,
- Mittelwert,
- Median,
- absolute und relative Szenariodifferenz.

## Finanzierungsvertrag

```text
FinancingRule {
  id
  component
  payer
  share
  validFrom
  validTo
  sourceId
}
```

Die Summe der Finanzierungsanteile einer Komponente muss innerhalb einer dokumentierten Toleranz `1` ergeben. Finanzierung wird nach der Anspruchsberechnung angewendet.

## Abgleichsvertrag

```text
OfficialReferenceValue {
  id
  period
  geography
  concept
  component?
  value
  unit
  sourceId
  comparability
  notes
}

ReconciliationEntry {
  referenceId
  modelValue
  officialValue
  absoluteDifference
  relativeDifference
  comparability
  causeCodes[]
  notes
}
```

Zulässige Vergleichbarkeitswerte:

- `direct`
- `partial`
- `not_comparable`

Typische Ursachencodes:

- `stock_vs_flow`
- `legal_status_mismatch`
- `reporting_lag`
- `payer_boundary`
- `missing_component`
- `synthetic_joint_distribution`
- `housing_fallback`
- `non_take_up_not_modelled`
- `rounding`

Es gibt keine freie Kalibrierkonstante, die nur dazu dient, die Gesamtsumme exakt anzugleichen.

## Qualitätsvertrag

Jeder Lauf enthält:

```text
Sgb2QualityReport {
  runId
  policyVersionId
  populationRunId
  sampleSize
  weightedBenefitUnits
  weightedPersons
  simulatedBenefitMonths
  calibrationEntries[]
  reconciliationEntries[]
  validationIssues[]
  uncertaintySummary
  knownLimitations[]
}
```

Ein Ergebnis kann fachlich verwendbar sein, obwohl einzelne Referenzen nur teilweise vergleichbar sind. Dieser Zustand wird als Warnung und nicht als Erfolg ohne Einschränkung ausgegeben.

## Szenariovertrag

Der zentrale Szenariozustand speichert:

```text
Sgb2ScenarioReference {
  policyVersionId
  parameterOverrides[]
  housingDatasetOverrides[]
  financingOverrides[]
  populationRunId
  modelVersion
}
```

Einfach- und Expertenmodus schreiben in denselben Vertrag. Der Einfachmodus erzeugt nachvollziehbare Overrides und keine parallelen Indizes.

Importregeln:

- bekannte ältere Schemas werden migriert,
- fehlende Quellenmetadaten führen zu Warnung oder Ablehnung nach Migrationsregel,
- unbekannte Modellversionen werden nicht still interpretiert,
- fehlende Bevölkerungsläufe und KdU-Datensätze werden sichtbar gemeldet.

## Persistenz und Worker

Die bestehende `LocalServerClient`-Grenze wird fortgeführt. Für das Bürgergeld-Modul sind fachliche Methoden vorzusehen:

- Policy-Versionen laden und validieren,
- regionale KdU-Datensätze laden,
- Bedarfsgemeinschaften für einen Population-Lauf ableiten,
- Monatsansprüche berechnen,
- Aggregate abfragen,
- Qualitäts- und Abgleichsberichte lesen,
- Szenarioläufe reproduzieren.

Personen-, Haushalts- und Bedarfsgemeinschaftsarrays verbleiben im Worker beziehungsweise Repository. React erhält nur benötigte Detailfälle, Aggregate und Erklärspuren.

## Fehlerklassen

- `policy_invalid`
- `parameter_missing`
- `parameter_out_of_period`
- `benefit_unit_invalid`
- `ambiguous_standard_need`
- `income_rule_invalid`
- `asset_facts_missing`
- `housing_dataset_missing`
- `housing_rule_ambiguous`
- `calculation_invariant_failed`
- `scenario_version_unsupported`

Fehler enthalten Code, fachliche Meldung, betroffene IDs und mögliche Nutzeraktion. Sie dürfen nicht ausschließlich in der Konsole erscheinen.

## Invarianten

Mindestens folgende Invarianten müssen gelten:

- keine negativen Bedarfe, Ansprüche oder Zahlungsbeträge,
- genau ein Regelbedarf je leistungsrelevanter Person,
- Summe der Komponenten entspricht dem Bedarfsgemeinschaftsergebnis,
- Summe der Personen entspricht dem Bedarfsgemeinschaftsergebnis,
- anerkannte Unterkunft und Heizung sind nicht negativ,
- nicht anerkannte Kosten entsprechen tatsächlichen minus anerkannten Kosten,
- höhere tatsächliche Kosten senken bei sonst gleichen Daten nicht den anerkannten Betrag,
- höheres anrechenbares Einkommen erhöht den Anspruch nicht,
- ein deaktivierter Mehrbedarf verändert keine fachlich fremde Komponente,
- Finanzierung verändert den Anspruch nicht,
- gleiche Eingaben und Versionen erzeugen gleiche Ergebnisse.

## Testvertrag

### Unit- und Property-Tests

- jede Regelbedarfsgruppe,
- alle Altersgrenzen,
- Mehrbedarfsbeginn, -ende und Obergrenzen,
- jedes Freibetragssegment und jeder Übergangspunkt,
- Einkommen exakt auf, unter und über Grenzen,
- Null-, Teil- und Vollanspruch,
- Vermögensstatus,
- KdU unter, auf und über regionaler Grenze,
- Karenz-, Übergangs- und Härtefall,
- KdU-Fallback und fehlender Datensatz,
- Restcent-Verteilung,
- Monotonie- und Summeninvarianten,
- deterministische Wiederholung.

### Golden Cases

Golden Cases speichern:

- Policy- und Modellversion,
- vollständige Eingaben,
- alle erwarteten Zwischenwerte,
- Personen- und Komponentenresultate,
- erwartete Erklärspur,
- Quellen-IDs.

### Aggregations- und Abgleichstests

- Monats- zu Jahreshochrechnung,
- Gewichte und Bezugsmonate,
- Komponentenzerlegung,
- Kostenträgerzerlegung,
- Baseline gegen Szenario,
- Referenzwert und Abstimmungsdifferenz,
- keine versteckte freie Restgröße.

### UI-Tests

- Einfach- und Expertenmodus erzeugen denselben Parametersatz,
- Baseline vollständig wiederherstellen,
- Szenario speichern, exportieren, importieren und neu laden,
- Quellen und Unsicherheit je Feld öffnen,
- Ergebnis bis auf Komponenten und Beispiel-Bedarfsgemeinschaft erklären,
- Desktop und Mobil,
- echte Browser-Screenshots im PR.

## Umsetzungspakete

| Issue | Vertragsteil |
|---|---|
| `de-sim#16` | Policy-Parameter, Quellenmetadaten, KdU-Schema und Migration |
| `de-sim#17` | SGB-II-Merkmale, Bedarfsgemeinschaften, Gewichte und Kalibrierung |
| `de-sim#18` | Regelbedarf, Mehrbedarf, Einkommen, Anspruch und Erklärspur |
| `de-sim#19` | regionale Unterkunft und Heizung |
| `de-sim#20` | Aggregation, Finanzierung und Abgleich |
| `de-sim#21` | Einfach- und Expertenmodus sowie Ergebnisdarstellung |
| `de-sim#22` | End-to-End-Abnahme, Qualitätsbericht und Releaseprüfung |

## Definition of Done für die Fachgrundlage

- öffentliche Fachbeschreibung vorhanden,
- interner Rechenvertrag vorhanden,
- Rechts-, Daten- und Haushaltsbaseline getrennt,
- Einheiten und Gültigkeitszeiträume definiert,
- Bedarfsgemeinschaft, Person, Einkommen, KdU und Bezugsmonate definiert,
- Berechnungsreihenfolge und Rundung festgelegt,
- Komponenten und Kostenträger getrennt,
- amtlicher Abgleich und Abstimmungsdifferenz definiert,
- Unsicherheit und Fallbacks definiert,
- Umsetzungspakete eindeutig zugeordnet.
