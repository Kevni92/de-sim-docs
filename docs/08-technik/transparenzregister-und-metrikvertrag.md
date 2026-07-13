---
title: Transparenzregister und Metrikvertrag
summary: Technischer und fachlicher Vertrag für Kennzahlen, Rechenwege, Quellen, Unsicherheit und Änderungsverlauf.
status: Arbeitsstand 0.7
last_updated: 2026-07-13
---

# Transparenzregister und Metrikvertrag

## Ziel

Milestone 3 führt für `Kevni92/de-sim` ein zentrales Transparenzregister ein. Sichtbare Kennzahlen werden nicht nur mit einer URL verknüpft, sondern mit einem strukturierten Nachweis aus:

- fachlicher Definition,
- Einheit und Geltungsbereich,
- Evidenzstatus und Konfidenz,
- vollständiger Formel,
- verwendeten Parametern,
- nummerierten Rechenschritten,
- Originalquellen,
- Unsicherheitsangabe,
- bekannten Grenzen,
- versioniertem Änderungsverlauf.

Der Nachweis beschreibt, **wie** eine Zahl zustande kommt. Er ist kein Ersatz für die fachliche Validierung des zugrunde liegenden Modells.

## Statusmodell

Jede Kennzahl besitzt genau einen sichtbaren Status:

| Status | Bedeutung |
|---|---|
| `amtlich` | Der dargestellte Wert oder seine Baseline stammt unmittelbar aus einer amtlichen Quelle. |
| `modell` | Der Wert wird aus dokumentierten Eingaben und einer versionierten Modelllogik abgeleitet. |
| `annahme` | Der Wert dient als ausdrücklich gekennzeichnete Szenario- oder Demonstrationsannahme. |
| `unbekannt` | Der Status konnte nicht belastbar bestimmt werden; dieser Zustand darf nicht stillschweigend als amtlich erscheinen. |

Die Konfidenz `hoch`, `mittel` oder `niedrig` ist davon getrennt. Eine amtliche Baseline kann beispielsweise hohe Konfidenz haben, während eine daraus abgeleitete langfristige Wirkung niedrige Konfidenz besitzt.

## MetricRecord

Der Metrikvertrag enthält mindestens:

| Feld | Zweck |
|---|---|
| `id` | stabile technische Kennung |
| `label` | verständlicher Name der Kennzahl |
| `category` | fachliche Gruppierung |
| `description` | Definition und Abgrenzung |
| `unit` | Einheit und Zeitraum |
| `status` | amtlich, Modell, Annahme oder unbekannt |
| `confidence` | qualitative Konfidenz |
| `dataYear` | Jahr der Datenbasis |
| `legalYear` | berücksichtigter Rechtsstand |
| `sourceIds` | stabile Verweise auf Originalquellen |
| `formula` | kompakte Gesamtformel |
| `parameters` | verwendete Eingangsgrößen einschließlich Provenienz |
| `calculation` | geordnete Rechenschritte |
| `uncertainty` | Bandbreite, Wertebereich oder Nichtanwendbarkeit |
| `limitations` | bekannte Auslassungen und Grenzen |
| `changeLog` | Modellversion, Datum und Änderungsbeschreibung |

Der aktuelle Szenariowert ist nicht dauerhaft im Metrikregister gespeichert. Er wird aus dem zentralen Szenariozustand berechnet und beim Öffnen des Nachweises zusammen mit der Modellversion angezeigt.

## Parameter und Provenienz

Ein Parameter besteht aus:

- Name,
- im Rechenweg verwendeter Darstellung,
- optionaler `sourceId`.

Parameter ohne Quellen-ID sind als Szenarioeingabe oder interne Modellgröße erkennbar. Ein Parameter darf nicht allein deshalb als amtlich gelten, weil die Zielkennzahl eine amtliche Baseline verwendet.

## Rechenschritte

Die Gesamtformel wird in geordnete Schritte zerlegt. Jeder Schritt enthält:

- verständliche Bezeichnung,
- mathematischen oder logischen Ausdruck,
- optional eine erläuternde Notiz.

Beispiel:

```text
1. Baseline laden
   B = 358,2 Mrd. €

2. Tarifeffekt bestimmen
   T = f(Freibetrag, Sätze, Schwellen, Splitting)

3. Modellstufe anwenden
   Δ = T × Faktor(Modellstufe)

4. Ergebnis bilden
   Aufkommen = B + Δ
```

## Unsicherheit

Unterstützt werden drei Formen:

- `band`: relative untere und obere Abweichung,
- `range`: fachlich definierter Wertebereich,
- `not-applicable`: für deterministische Darstellungen wie eine aus Eingaben gezeichnete Tarifkurve.

Eine fehlende Unsicherheitsangabe ist nicht gleichbedeutend mit Sicherheit. Wo keine belastbare Quantifizierung möglich ist, muss dies textlich erklärt und die Konfidenz entsprechend niedrig gesetzt werden.

## Quellenbeziehung

`MetricRecord.sourceIds` verweist auf `SourceRecord`-Objekte. Eine Quelle enthält unter anderem:

- Institution und Titel,
- Original-URL,
- Datenjahr und Rechtsstand,
- Quellenstatus und Konfidenz,
- Zusammenfassung,
- verwendete Methode,
- bekannte Grenzen,
- Datum der letzten Prüfung.

Mehrere Kennzahlen können dieselbe Quelle verwenden. Eine Kennzahl kann amtliche Baselines und eine projektinterne Modellquelle kombinieren.

## Lokale Servergrenze

Das Register wird wie Szenarien und Quellen über die lokale Servergrenze geladen:

```text
React-Oberfläche
  → LocalServerClient.listMetrics()
    → Web Worker: metrics:list
      → IndexedDB: metrics
```

Milestone 3 erhöht die Datenbankversion auf 3 und ergänzt den Store `metrics`. Bestehende Stores und lokale Szenarien bleiben erhalten.

Referenzdaten werden versioniert in den Worker eingebracht und bei der Initialisierung über stabile IDs aktualisiert. Persistierte Nutzerentwürfe und Szenarien werden dadurch nicht überschrieben.

## UI-Nutzerfluss

### Aus einer Kennzahl

Ein Quellen- beziehungsweise Nachweis-Button öffnet den Drawer direkt für die zugehörige Metrik. Angezeigt werden:

1. aktueller Szenariowert,
2. Status und Konfidenz,
3. Daten- und Rechtsstand,
4. Modellversion und Zeithorizont,
5. Definition,
6. Formel und Rechenschritte,
7. Parameter und Provenienz,
8. Unsicherheit,
9. Originalquellen,
10. bekannte Grenzen,
11. Änderungsverlauf.

### Transparenzregister

Die Hauptnavigation enthält eine eigene Seite **Transparenz**. Dort können Nutzer:

- alle registrierten Kennzahlen sehen,
- nach Name, Kategorie, Beschreibung oder Formel suchen,
- nach Evidenzstatus filtern,
- aktuelle Szenariowerte sehen,
- einen vollständigen Nachweis öffnen.

## Abdeckung in Milestone 3

Verknüpft sind insbesondere:

- Gesamteinnahmen,
- Gesamtausgaben,
- Budgetsaldo,
- Schuldenstand,
- einzelne Haushaltspositionen,
- Einkommensteueraufkommen,
- Einkommensteuertarif,
- Verteilungswirkung,
- Beispielhaushalte,
- regionale Demonstrationswirkung,
- schematischer Zeitverlauf,
- getrennte Teilbereiche Migration und Asyl.

Die Abdeckung wird in späteren Milestones mit jedem neuen Fachmodul erweitert.

## Testanforderungen

Playwright prüft mindestens:

- Navigation zum Transparenzregister,
- Suche nach einer Kennzahl,
- Statusfilter,
- Öffnen eines Nachweises aus dem Register,
- Öffnen eines Nachweises direkt aus dem Dashboard,
- sichtbare Formel und Rechenschritte,
- Parameterliste,
- Unsicherheitsdarstellung,
- Originalquellen,
- bekannte Grenzen,
- Änderungsverlauf,
- Bedienbarkeit des Drawers auf Mobilgeräten.

Typecheck und Produktions-Build müssen den erweiterten Metrik- und Worker-Vertrag prüfen.

## Spätere Serverauslagerung

Ein externer Server übernimmt später die gleichen fachlichen Operationen:

```text
GET /sources
GET /metrics
GET /metrics/{id}
```

Stabile Metrik- und Quellen-IDs sind Voraussetzung dafür, dass gespeicherte Szenarien reproduzierbar bleiben. Der Server darf einen historischen Modelllauf nicht stillschweigend auf eine neue Formel umdeuten; Modellversion und Änderungsverlauf müssen erhalten bleiben.

## Grenzen von Milestone 3

- Die vorhandenen Demonstrationswerte werden nicht allein durch ihre Dokumentation fachlich valide.
- Mehrere Bereiche verwenden weiterhin Annahmen mit niedriger Konfidenz.
- Der Rechenweg ist strukturiert, aber noch kein allgemeiner ausführbarer Rechengraph.
- Historische Modellläufe werden lokal noch nicht als unveränderliche Snapshots archiviert.
- Quellenabschnitte und maschinenlesbare Zitate werden später verfeinert.

## Verwandte Kapitel

- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Evidenzdatenbank und Quellenprovenienz](../06-evidenz/evidenzdatenbank.md)
- [Lokaler Worker und Persistenz](lokaler-worker-und-persistenz.md)
- [Zentrales Szenario- und Zustandsmodell](zentrales-szenario-und-zustandsmodell.md)
- [UI-Referenz und Nutzerflüsse](ui-referenz-und-nutzerfluesse.md)
