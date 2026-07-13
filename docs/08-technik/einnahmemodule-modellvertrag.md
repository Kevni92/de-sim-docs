---
title: Modellvertrag weitere Einnahmen
summary: Interner technischer Vertrag für Parameter, Ergebnisobjekte, Worker-Referenzdaten und UI-Integration der Einnahmemodule.
status: Arbeitsstand 0.5
last_updated: 2026-07-13
---

# Modellvertrag weitere Einnahmen

Dieses Kapitel ist interne Implementierungsdokumentation und wird nicht auf der öffentlichen Dokumentationsseite gebaut.

## Modulidentität

Unterstützte Modul-IDs:

```text
ust, erb, verm, sozb, kst, kap, energie
```

Jede ID ist zugleich:

- Schlüssel im Dashboard,
- Präfix der Szenarioparameter,
- Teil der Metrik-ID `metric-revenue-<id>`,
- Referenz für Navigation und Berechnungsnachweis.

## Parameterablage

Modulparameter werden im bestehenden Feld `ScenarioDraft.revenueChanges` gespeichert. Fachliche Parameter verwenden das Schema:

```text
param.<moduleId>.<parameterKey>
```

Beispiele:

```text
param.ust.standardRate
param.verm.rate
param.sozb.healthCeiling
```

Berechnete Ergebnisänderungen dürfen dieselben Schlüssel nicht überschreiben. Für die materialisierte Szenarioansicht werden die aggregierten Deltas weiterhin unter den kurzen Einnahmen-IDs gespeichert.

## Definition

Jede `RevenueModuleDefinition` enthält mindestens:

- `id`, `label`, `shortLabel`,
- `baseline`,
- `confidence`,
- fachliche Beschreibung und Rechtsgrundlage,
- `sourceIds`,
- `behaviorSensitivity`,
- `uncertaintyPercent`,
- Inzidenzanteile,
- Parameterdefinitionen mit Baseline, Minimum, Maximum, Schrittweite, Einheit und Beschreibung.

## Ergebnisvertrag

`RevenueModuleResult` enthält:

- Baseline,
- statischen Szenariowert,
- finalen Szenariowert,
- statisches Delta,
- Verhaltensanpassung,
- finales Delta,
- Modellstufe,
- Unsicherheit,
- Konfidenz,
- Inzidenz,
- tatsächlich verwendete Parameter.

Es gilt:

```text
value = staticValue + behavioralAdjustment
value - baseline = delta
staticValue - baseline = staticDelta
behavioralAdjustment = delta - staticDelta
```

## Modellstufen

- `statisch`: Reaktionsfaktor 0,
- `verhalten`: modulspezifische Sensitivität,
- `langfrist`: verstärkte Sensitivität.

Die Reaktion darf niemals die statische Erstwirkung verdecken. Beide Größen müssen im UI und im Transparenzregister separat erscheinen.

## Worker und IndexedDB

Die lokale Worker-Schnittstelle bleibt gegenüber der UI stabil. Milestone 5 aktualisiert die Referenzdaten auf Version 5 und ergänzt Quellen und Metriken. Szenarien und aktive Entwürfe bleiben in den vorhandenen Stores gespeichert.

Der Worker ist weiterhin der einzige Zugriffspunkt auf IndexedDB. UI-Komponenten dürfen IndexedDB nicht direkt öffnen.

## Navigation

- `/einkommensteuer`: separates tarifbasiertes Einkommensteuer-Modul,
- `/einnahmen`: gemeinsame Seite der sieben Aggregatmodule.

Die ausgewählte Modul-ID ist UI-Zustand. Die Parameter liegen im zentralen Szenariozustand und werden über Undo, Redo, Autosave, JSON-Import und JSON-Export verwaltet.

## Tests

Verpflichtend sind:

- TypeScript-Prüfung,
- Produktions-Build,
- Baseline-Reproduktion aller Module,
- deterministische Referenzfälle für Umsatz- und Vermögensteuer,
- Navigation aus dem Dashboard,
- Live-Aktualisierung der Detailansicht,
- Konsistenz zwischen Detailseite, Dashboard und Transparenzregister,
- Quellen-Drawer aus Worker-Daten,
- Autosave und Wiederherstellung,
- JSON-Rundlauf,
- Desktop- und Mobile-Playwright-Test,
- echter Screenshot der sichtbaren UI-Änderung.

## Ablösung des lokalen Servers

Die spätere Serverimplementierung übernimmt dieselben fachlichen Objekte und Endpunkte. UI und Modellkern dürfen nicht von IndexedDB-spezifischen Typen abhängen. Quellen, Metriken und Szenarien sollen später über eine versionierte API bereitgestellt werden.

## Verwandte Kapitel

- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Szenario- und Zustandsmodell](szenario-und-zustandsmodell.md)
- [Transparenzregister und Metrikvertrag](transparenzregister-und-metrikvertrag.md)
- [Einkommensteuer-Modellvertrag](einkommensteuer-modellvertrag.md)
