---
title: Szenario- und Zustandsmodell
summary: Interner Einstiegspunkt für zentralen Szenariozustand, Historie, Persistenz und Serverabstraktion.
status: Intern 0.6
last_updated: 2026-10-21
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

## Gemeinsame Haushaltsübersicht

Übersicht und Szenariovergleich verwenden dieselbe Zusammenfassung der dargestellten Einnahme- und Ausgabenposten. Sie übernimmt die Ergebnisse des aktuellen Szenarios und weist Baseline, Veränderung und Saldo aus denselben Zeilen aus. Ein fehlendes Modul darf nicht durch seinen Baselinewert oder null ersetzt werden; in diesem Fall bleiben Gesamtergebnis und Vergleich sichtbar unvollständig.

Die Wirkungsebenen des Wirkungs-Workers bleiben davon getrennt. Nur ein Lauf mit aktueller Eingabesignatur darf als aktuelle modellierte Reaktion erscheinen. Direkte Modulergebnisse und zusätzliche Wirkungspfade werden nicht zu einer neuen Gesamtformel addiert.

Der Clientvertrag bleibt bewusst serverähnlich. Ein späteres Backend soll dieselben Operationen anbieten, ohne dass Seiten oder Fachmodule direkten Datenbankzugriff erhalten.

## Verwandte Kapitel

- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Ausgabenmodule-Modellvertrag](ausgabenmodule-modellvertrag.md)
