---
title: Technischer Modellvertrag der Ausgabenmodule
summary: Interne Schnittstellen, IDs, Persistenz, Worker-Seeding und Testvertrag für Milestone 6.
status: Intern 0.6
last_updated: 2026-07-13
---

# Technischer Modellvertrag der Ausgabenmodule

> Diese Seite ist eine interne Entwicklungsunterlage und durch `exclude_docs` von der öffentlichen Website ausgeschlossen.

## Modul-IDs

```text
social
pension
education
family
health
defense
infrastructure
subsidies
migration
```

Die Implementierung liegt in `src/lib/expense-modules.ts`. Jede Definition enthält ID, Beschriftung, Baseline, Konfidenz, Rechts- und Quellenhinweise, Sensitivität, Unsicherheit, Begünstigtenanteile, zugeordnete Dashboardzeilen und Parameterdefinitionen.

## Parameterschlüssel

Szenarioparameter werden unter einem stabilen Namensraum gespeichert:

```text
expense.param.<moduleId>.<parameterKey>
```

Beispiele:

```text
expense.param.social.benefitIndex
expense.param.health.preventionSavings
expense.param.migration.integrationIndex
```

Die Parameter liegen im bestehenden Feld `ScenarioDraft.expenseChanges`. Dadurch bleiben das JSON-Schema, der zentrale History-Reducer, Undo/Redo, Autosave und die spätere Server-API kompatibel.

## Ergebnisvertrag

`ExpenseModuleResult` enthält:

```text
id
label
baseline
staticValue
value
staticDelta
feedbackAdjustment
delta
confidence
uncertaintyPercent
modelLevel
beneficiaries
parameters
lineValues
components
```

`lineValues` verteilt kombinierte Module auf die bestehenden Dashboardzeilen. `components` liefert fachlich getrennte Teilaggregate für die Detailansicht.

## Dashboardzuordnung

```text
buerger   -> social
wohnen    -> social
rente     -> pension
bildung   -> education
familie   -> family
kita      -> family
gesundheit -> health
pflege    -> health
vert      -> defense
infra     -> infrastructure
sub       -> subsidies
migration -> migration
```

`expenseLineResultsById()` stellt sicher, dass Dashboard und Detailseite dieselben berechneten Werte verwenden. Nicht zugeordnete Ausgabenzeilen behalten bis zu einem späteren Modul ihren bisherigen Baselinewert.

## Budgetintegration

Der Saldo verwendet:

```text
budgetDelta = revenueDelta - expenseDelta
```

Die direkte Wirkung und die modellierte Folgewirkung werden ebenfalls mit dem passenden Vorzeichen in den Saldo übertragen. Eine höhere Ausgabe verschlechtert den Saldo, eine niedrigere Ausgabe verbessert ihn.

## Worker und IndexedDB

Der Browser-Worker `local-server-v6.worker.ts` erweitert die vorherige Worker-Version und schreibt die zusätzlichen Quellen und Metriken in die vorhandenen Stores:

```text
sources
metrics
scenarios
drafts
```

Die Datenbankversion bleibt 4, da keine neue Store-Struktur erforderlich ist. Die neue Worker-Datei ist ausschließlich der aktuelle Einstiegspunkt des `LocalServerClient`. Der fachliche Zugriff aus React erfolgt weiterhin nur über den Client und nicht direkt auf IndexedDB.

Ein späterer Server kann dieselben semantischen Operationen übernehmen:

```text
sources:list
metrics:list
scenarios:list
scenarios:save
scenarios:delete
draft:get
draft:save
```

## Transparenzdaten

`src/lib/expense-transparency.ts` liefert:

- Quellen mit Institution, URL, Daten- und Rechtsstand,
- Metrikdefinitionen mit Formel und Parametern,
- Rechenschritte,
- Unsicherheitsband,
- Einschränkungen,
- Änderungsverlauf.

Die Metrik-ID folgt:

```text
metric-expense-<moduleId>
```

## UI-Vertrag

`ExpenseModulesPage` erhält ausschließlich berechnete Ergebnisse und Callbacks. Die Seite berechnet keine eigene Haushaltslogik. Sichtbare Änderungen folgen dem bestehenden Designsystem von `staat-sklarheit` und den Komponentenmustern der Einnahmenseite.

Erforderliche UI-Bestandteile:

- Modulliste,
- Baseline und Szenariowert,
- direkte Wirkung,
- Folgewirkung,
- Parametereditor,
- Modellstufe,
- Begünstigtenstruktur,
- getrennte Komponenten, sofern vorhanden,
- Gesamtübersicht,
- Quellen-Drawer.

## Playwright-Vertrag

`e2e/expense-modules.spec.ts` prüft mindestens:

1. Navigation vom Dashboard in ein Ausgabenmodul,
2. Live-Reaktion eines Parameters,
3. getrennte Migrationsteilaggregate,
4. Laden von Quellen und Metriken aus dem Worker,
5. Autosave und Wiederherstellung über IndexedDB,
6. mobile Navigation,
7. Erzeugung des echten UI-Screenshots.

Der Screenshotpfad lautet:

```text
test-results/milestone-6-expense-modules.png
```

CI lädt den Playwright-Bericht und den Screenshot als getrennte Artefakte hoch.

## Verwandte Kapitel

- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Szenario- und Zustandsmodell](szenario-und-zustandsmodell.md)
- [Fachliche Ausgabenmodule](../02-fiskal/ausgabenmodule.md)
