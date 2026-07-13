---
title: Szenario- und Zustandsmodell
summary: Interner Einstiegspunkt für zentralen Szenariozustand, Historie, Persistenz und Serverabstraktion.
status: Intern 0.6
last_updated: 2026-07-13
---

# Szenario- und Zustandsmodell

> Diese Seite ist eine interne Entwicklungsunterlage und durch `exclude_docs` von der öffentlichen Website ausgeschlossen.

Der zentrale `ScenarioDraft` ist die einzige veränderbare fachliche Quelle für Einkommensteuer-, Einnahmen- und Ausgabenparameter. UI-Seiten erhalten Zustand und Callbacks aus `App.tsx`; sie speichern nicht selbst in IndexedDB.

## Kernelemente

- `revenueChanges` enthält Parameter und materialisierte Ergebnisse der Einnahmenmodule.
- `expenseChanges` enthält Parameter und materialisierte Ergebnisse der Ausgabenmodule.
- `incomeTax` enthält den strukturierten Einkommensteuertarif.
- `modelLevel` steuert statische, verhaltensbasierte oder langfristige Wirkungen.
- `modelVersion` und `sourceIds` sichern Provenienz und Migration.
- der History-Reducer stellt Undo und Redo bereit.
- der lokale Worker kapselt Entwurf, Szenarien, Quellen und Metriken in IndexedDB.

## Persistenzfluss

```text
UI-Eingabe
  -> ScenarioDraft
  -> normalisierter History-Reducer
  -> materialisiertes Szenario
  -> LocalServerClient
  -> Web Worker
  -> IndexedDB
```

Der Clientvertrag bleibt bewusst serverähnlich. Ein späteres Backend soll dieselben Operationen anbieten, ohne dass Seiten oder Fachmodule direkten Datenbankzugriff erhalten.

## Verwandte Kapitel

- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Ausgabenmodule-Modellvertrag](ausgabenmodule-modellvertrag.md)
