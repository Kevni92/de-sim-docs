---
title: Zentrales Szenario- und Zustandsmodell
summary: Einheitliches Modell für Entwurf, Historie, Persistenz und Austausch von Szenarien.
status: Arbeitsstand 0.6
last_updated: 2026-07-13
---

# Zentrales Szenario- und Zustandsmodell

## Ziel

Milestone 2 führt einen einzigen verbindlichen Szenariozustand für die Anwendung `Kevni92/de-sim` ein. Dashboard, Einkommensteuer-Detailseite, Vergleich und Szenarioverwaltung lesen und verändern denselben Zustand.

Damit werden voneinander abweichende lokale Komponentenwerte vermieden. Eine Änderung des Grundfreibetrags, der Modellstufe oder des Zeithorizonts ist unmittelbar Teil desselben Entwurfs und wird bei Speichern, Export und Reload konsistent berücksichtigt.

## Abgrenzung

Das Szenariomodell beschreibt den Zustand und seinen Lebenszyklus. Es macht noch keine fachliche Aussage darüber, ob eine Steuerformel oder Wirkungsschätzung korrekt kalibriert ist.

Die sichtbaren Zahlen bleiben bis zur fachlichen Umsetzung der jeweiligen Modelle als Demonstrationswerte gekennzeichnet.

## Kernobjekte

### ScenarioDraft

Der aktive Arbeitsstand enthält:

- Name,
- Beschreibung,
- Rechtsstand,
- Datenstand,
- Zeithorizont,
- Modellstufe,
- Einnahmenänderungen,
- Ausgabenänderungen,
- Einkommensteuerparameter,
- explizite Annahmen,
- Modellversion,
- referenzierte Quellen-IDs.

Der Entwurf besitzt bewusst keinen zwingenden dauerhaften Datensatzschlüssel. Ein neuer oder importierter Entwurf kann bearbeitet werden, bevor er als gespeichertes Szenario abgelegt wird.

### ScenarioState

Ein gespeichertes Szenario erweitert den Entwurf um:

- stabile Szenario-ID,
- Erstellungszeitpunkt,
- letzten Änderungszeitpunkt.

Das Objekt ist die derzeitige lokale Entsprechung eines späteren serverseitigen Szenariodatensatzes.

### ActiveScenarioDraft

Für die automatische Wiederherstellung wird zusätzlich gespeichert:

- ID des aktuell geladenen gespeicherten Szenarios oder `null`,
- vollständiger aktiver Entwurf.

Dadurch kann die Anwendung nach einem Reload nicht nur Werte wiederherstellen, sondern auch erkennen, ob ein erneutes Speichern einen bestehenden Datensatz aktualisieren oder einen neuen Datensatz anlegen soll.

## Feldstruktur

| Feld | Bedeutung | Beispiel |
|---|---|---|
| `name` | nutzerdefinierte Bezeichnung | `Reformentwurf A` |
| `description` | kurze Einordnung des Szenarios | Arbeitsstand für eine Reformsimulation |
| `legalYear` | zugrunde gelegter Rechtsstand | `2026` |
| `dataYear` | primärer Datenstand | `2025` |
| `horizonYears` | Betrachtungszeitraum | `1`, `5`, `10` oder `20` Jahre |
| `modelLevel` | statisch, Verhalten oder langfristig | `verhalten` |
| `revenueChanges` | Änderungen nach Einnahmenmodul | Einkommensteuer, Kreditaufnahme |
| `expenseChanges` | Änderungen nach Ausgabenmodul | Bildung, Gesundheit oder Rente |
| `incomeTax` | Parameter der Einkommensteueransicht | Freibetrag, Sätze und Schwellen |
| `assumptions` | explizite Annahmen | eine Annahme pro Eintrag |
| `modelVersion` | reproduzierbare Modellkennung | `ui-demo-0.2.0` |
| `sourceIds` | stabile Verweise auf Quellenobjekte | `source-budget`, `source-est` |

## Zentrale Zustandsverwaltung

Der React-Einstieg hält eine Historie mit drei Bereichen:

```text
past → present → future
```

- `present` ist der aktuell sichtbare Entwurf.
- `past` enthält bis zu 50 vorherige Zustände.
- `future` enthält nach einem Rückgängig-Vorgang erneut anwendbare Zustände.
- Eine neue Änderung leert `future`.

Die Historie arbeitet auf vollständigen Szenarioentwürfen. Dadurch werden auch zusammengehörige Metadaten und Parameter gemeinsam rückgängig gemacht.

## Rückgängig und Wiederholen

Die Kopfzeile bietet funktionale Aktionen für:

- Rückgängig,
- Wiederholen.

Die Schaltflächen sind deaktiviert, wenn keine passende Historie vorhanden ist. Eine Änderung an einem Parameter oder Metadatenfeld erzeugt einen neuen Historieneintrag, sofern sich der Zustand tatsächlich geändert hat.

## Materialisierter Zustand

Einige Werte werden aus Eingaben abgeleitet. Dazu gehören beispielsweise:

- berechnete Änderung des Einkommensteueraufkommens,
- korrespondierende Änderung der Nettokreditaufnahme.

Vor Autosave, dauerhaftem Speichern und Export wird der Entwurf materialisiert. Das bedeutet, dass abgeleitete Werte in das zu speichernde Szenario übernommen werden, ohne die Benutzereingabe-Historie durch rein technische Aktualisierungen zu verunreinigen.

## Automatische lokale Sicherung

Nach einer Änderung wartet die Anwendung kurz und sendet anschließend den aktiven Entwurf an die lokale Servergrenze:

```text
React-Zustand
  → LocalServerClient.saveActiveDraft
    → Web Worker
      → IndexedDB / Store drafts
```

Die Verzögerung verhindert unnötige Schreibvorgänge bei unmittelbar aufeinanderfolgenden Eingaben.

Beim Start werden parallel geladen:

- Quellen,
- gespeicherte Szenarien,
- aktiver Entwurf.

Erst danach wird der Zustand als initialisiert behandelt. So überschreibt der Standardzustand keinen bereits gespeicherten Entwurf.

## IndexedDB-Schema

Milestone 2 erhöht die Datenbankversion auf `2`.

Verwendete Stores:

| Store | Inhalt |
|---|---|
| `sources` | Quellen- und Methodikobjekte |
| `scenarios` | dauerhaft gespeicherte Szenarien |
| `drafts` | automatisch gesicherter aktiver Entwurf |

Der aktive Entwurf wird unter dem stabilen Schlüssel `active` abgelegt.

Die Migration legt den zusätzlichen Store nur an, wenn er noch nicht existiert. Bereits gespeicherte Quellen und Szenarien bleiben erhalten.

## Speichern und Laden

### Speichern

Beim Speichern wird:

1. der aktuelle Entwurf materialisiert,
2. eine bestehende aktive Szenario-ID wiederverwendet oder eine neue ID erzeugt,
3. der Erstellungszeitpunkt beibehalten,
4. der Änderungszeitpunkt aktualisiert,
5. das vollständige Objekt über Worker und IndexedDB gespeichert.

### Laden

Beim Laden wird ein gespeichertes Szenario normalisiert und als neuer aktiver Zustand eingesetzt. Die aktive Szenario-ID wird mitgeführt.

Ältere lokale Szenarien können noch Felder aus einer früheren Fassung vermissen. Fehlende Werte werden durch definierte Standardwerte ergänzt.

### Löschen

Das Löschen entfernt nur den gespeicherten Datensatz. Ist das gelöschte Szenario aktiv, wird die aktive ID entfernt; der sichtbare Entwurf bleibt als ungespeicherter Arbeitsstand erhalten.

### Duplizieren

Duplizieren erzeugt:

- eine neue ID,
- einen neuen Erstellungszeitpunkt,
- den Namenszusatz `(Kopie)`,
- ansonsten denselben materialisierten Zustand.

Die Kopie wird sofort gespeichert und als aktives Szenario geladen.

## Neues Szenario

Die Aktion `Neu` ersetzt den aktuellen Entwurf durch einen definierten Standardzustand und entfernt die aktive Szenario-ID.

Der neue Entwurf wird anschließend automatisch lokal gesichert, aber erst durch die explizite Speichern-Aktion zu einem dauerhaft gelisteten Szenario.

## JSON-Austauschformat

Der Export verwendet einen kleinen Umschlag:

```json
{
  "schemaVersion": 1,
  "scenario": {
    "name": "Reformentwurf A",
    "legalYear": 2026,
    "dataYear": 2025
  }
}
```

Die Versionsnummer erlaubt spätere Migrationen des Austauschformats.

### Export

Exportiert wird der materialisierte Zustand als formatierte JSON-Datei. Der Dateiname wird aus dem Szenarionamen abgeleitet und bereinigt.

### Import

Beim Import werden geprüft:

- unterstützte `schemaVersion`,
- vorhandenes Szenarioobjekt,
- bekannte Feldtypen.

Fehlende Felder werden normalisiert. Das importierte Szenario wird zunächst als ungespeicherter Entwurf geladen.

### Kopieren

Die gleiche JSON-Repräsentation kann in die Zwischenablage kopiert werden. Diese Funktion ersetzt noch keinen reproduzierbaren öffentlichen Szenario-Link, da kein externer Server vorhanden ist.

## Szenarioverwaltung in der Oberfläche

Der Drawer `Szenario verwalten` zeigt:

- Status als gespeichertes Szenario oder lokaler Entwurf,
- Anzahl lokal gespeicherter Szenarien,
- Modellversion,
- Name und Beschreibung,
- Rechts- und Datenstand,
- Zeithorizont,
- Modellstufe,
- Annahmen,
- referenzierte Quellen-IDs,
- Aktionen für Neu, Duplizieren, Import, Export und Kopieren.

Die Darstellung verwendet weiterhin Farben, Typografie, Abstände und Drawer-Verhalten aus der verbindlichen UI-Referenz.

## Fehlerverhalten

- Nicht unterstützte Importdateien erzeugen eine sichtbare Fehlermeldung.
- Ein blockierter Zwischenablagezugriff wird verständlich gemeldet.
- Worker- oder IndexedDB-Fehler werden als abgelehnte Client-Promises weitergegeben.
- Die Anwendung greift nicht direkt aus UI-Komponenten auf IndexedDB zu.

## Datenschutz und Sicherheit

In der lokalen Fassung werden keine Benutzerkonten und keine personenbezogenen Daten gespeichert. JSON-Dateien können jedoch nutzerdefinierte Beschreibungen und Annahmen enthalten. Sie sind daher wie normale lokale Dateien zu behandeln.

## Testanforderungen

Playwright prüft mindestens:

- gemeinsame Aktualisierung des zentralen Zustands,
- funktionales Rückgängig und Wiederholen,
- Autosave und Wiederherstellung nach Reload,
- dauerhaftes Speichern und Laden,
- Duplizieren,
- JSON-Export,
- JSON-Import,
- Bedienbarkeit des Drawers auf Desktop und Mobilgeräten,
- Erstellung eines aktuellen UI-Screenshots.

TypeScript und Produktions-Build müssen zusätzlich erfolgreich sein.

## Spätere Serverauslagerung

Die spätere Serverimplementierung soll den bestehenden Client-Vertrag möglichst erhalten. Ersetzt werden primär:

```text
Web Worker + IndexedDB
```

durch:

```text
HTTP oder RPC + serverseitige Datenbank
```

Die UI soll weiterhin nur fachlich benannte Client-Methoden verwenden. Für eine echte Mehrgeräte-Nutzung werden später zusätzlich benötigt:

- Benutzer- oder anonyme Besitzmodelle,
- serverseitige Versionshistorie,
- Konfliktauflösung,
- Freigabelinks,
- Zugriffsrechte,
- serverseitige Validierung und Migration.

## Verwandte Kapitel

- [UI-Referenz und Nutzerflüsse](ui-referenz-und-nutzerfluesse.md)
- [Lokaler Worker und Persistenz](lokaler-worker-und-persistenz.md)
- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Berechnungstransparenz](../06-evidenz/berechnungstransparenz.md)
- [Unsicherheit und Szenarien](../06-evidenz/unsicherheit-szenarien.md)
