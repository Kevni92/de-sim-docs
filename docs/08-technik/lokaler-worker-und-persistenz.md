---
title: Lokaler Worker und Persistenz
summary: Übergangsarchitektur für Quellen, Metriken sowie Speichern und Laden ohne externen Server.
status: Arbeitsstand 0.7
last_updated: 2026-07-13
---

# Lokaler Worker und Persistenz

## Ziel

Die erste Projektphase verwendet keinen externen Anwendungsserver. Quellen, Kennzahlennachweise, gespeicherte Szenarien und der aktive Arbeitsentwurf werden über eine serverähnliche Schnittstelle angesprochen, deren Implementierung vollständig im Browser läuft.

Dadurch kann die Fachlogik bereits gegen einen klaren Serververtrag entwickelt werden, ohne die spätere Auslagerung an eine HTTP-API zu blockieren.

## Architektur

```text
React-Oberfläche
  → LocalServerClient
    → Web Worker
      → IndexedDB
```

Die Oberfläche darf IndexedDB nicht direkt verwenden. Sämtliche Zugriffe laufen über den `LocalServerClient` und ein typisiertes Nachrichtenprotokoll.

## Verantwortlichkeiten

### LocalServerClient

- stellt fachlich benannte Methoden für Quellen, Metriken, Szenarien und den aktiven Entwurf bereit,
- erzeugt Korrelations-IDs für parallele Anfragen,
- übersetzt Worker-Antworten in Promises,
- kapselt Transportfehler.

### Web Worker

- simuliert die spätere Servergrenze,
- validiert und verteilt Anfragen,
- stellt versionierte Referenzdaten für Quellen und Metriken bereit,
- führt Datenbankzugriffe außerhalb des UI-Threads aus,
- liefert typisierte Erfolgs- oder Fehlerantworten.

### IndexedDB

- speichert Quellenmetadaten,
- speichert strukturierte Kennzahlennachweise,
- speichert vollständige Szenarien inklusive Modellstufe und Änderungszeitpunkt,
- speichert den aktiven Arbeitsentwurf für die Wiederherstellung nach einem Reload,
- wird versioniert migriert,
- enthält keine geheime oder personenbezogene Information.

## Datenbankversion 3

Milestone 3 verwendet vier Object Stores:

| Store | Zweck |
|---|---|
| `sources` | Quellen- und Methodikdaten |
| `metrics` | Definitionen, Rechenwege, Parameter, Unsicherheit und Historie von Kennzahlen |
| `scenarios` | dauerhaft gespeicherte Szenarien |
| `drafts` | automatisch gesicherter aktiver Entwurf |

Der aktive Entwurf liegt im Store `drafts` unter dem stabilen Schlüssel `active`.

Die Migration von Version 2 auf Version 3 ergänzt ausschließlich `metrics`. Bestehende Quellen, Szenarien und Entwürfe bleiben erhalten.

Referenzdaten für `sources` und `metrics` werden über stabile IDs aktualisiert. Diese Aktualisierung überschreibt keine Nutzerobjekte in `scenarios` oder `drafts`.

## Fachliche Objekte

### SourceRecord

Ein Quellenobjekt enthält mindestens:

- stabile ID,
- Titel und Institution,
- Original-URL,
- Datenjahr und Rechtsstand,
- Evidenzstatus und Konfidenz,
- kurze Zusammenfassung,
- verwendete Methode,
- bekannte Grenzen,
- Datum der letzten fachlichen Prüfung.

### MetricRecord

Ein Kennzahlennachweis enthält mindestens:

- stabile Metrik-ID,
- Name, Kategorie, Definition und Einheit,
- Evidenzstatus und Konfidenz,
- Datenjahr und Rechtsstand,
- referenzierte Quellen-IDs,
- Gesamtformel,
- verwendete Parameter,
- geordnete Rechenschritte,
- Unsicherheitsdefinition,
- bekannte Grenzen,
- Änderungsverlauf.

Der aktuell angezeigte Wert wird aus dem Szenariozustand berechnet und nicht als statischer Bestandteil des Metrikregisters behandelt.

### ScenarioDraft

Der aktive Entwurf enthält den vollständigen bearbeitbaren Zustand, unter anderem:

- Name und Beschreibung,
- Rechtsstand und Datenstand,
- Modellstufe und Zeithorizont,
- Einnahmen- und Ausgabenänderungen,
- Einkommensteuerparameter,
- Annahmen,
- Modellversion und Quellen-IDs.

### ScenarioState

Ein dauerhaft gespeichertes Szenario erweitert den Entwurf um:

- stabile ID,
- Erstellungszeitpunkt,
- Änderungszeitpunkt.

### ActiveScenarioDraft

Der automatisch gesicherte Arbeitsstand enthält:

- die ID des aktuell geladenen Szenarios oder `null`,
- den vollständigen Entwurf.

## Nachrichtenprotokoll

Der Worker unterstützt mindestens:

```text
sources:list
metrics:list
scenarios:list
scenarios:save
scenarios:delete
draft:get
draft:save
```

Jede Anfrage und Antwort trägt eine Korrelations-ID. Fehler werden als strukturierte Fehlerantworten an den Client zurückgegeben.

## Automatische Sicherung

Änderungen des zentralen Szenariozustands werden kurz verzögert über `draft:save` gespeichert. Die Verzögerung reduziert Schreibvorgänge bei schnellen Eingabefolgen.

Beim Start lädt die Anwendung den Entwurf mit `draft:get`. Der geladene Zustand wird normalisiert, damit ältere lokale Daten weiterhin verwendet werden können.

Quellen und Metriken werden beim Start parallel mit Szenarien und Entwurf geladen. Die UI zeigt einen Nachweis nur, wenn die referenzierte Metrik im Register vorhanden ist.

## Austauschbarkeit

Der UI-Code hängt ausschließlich vom Client-Vertrag ab. Eine spätere Serverimplementierung ersetzt den Worker-Transport durch HTTP oder RPC, ohne dass Fachkomponenten IndexedDB-Details kennen müssen.

Für die Migration gelten folgende Regeln:

1. Methoden und Ergebnisobjekte bleiben möglichst kompatibel.
2. Fehler werden weiterhin strukturiert zurückgegeben.
3. lokale Szenarien können als versioniertes JSON exportiert und auf den Server übertragen werden.
4. Quellen- und Metrik-IDs bleiben stabil, damit gespeicherte Szenarien reproduzierbar bleiben.
5. die aktive Entwurfssemantik wird serverseitig entweder als Draft-Ressource oder als lokale Cache-Schicht fortgeführt.
6. historische Modellversionen dürfen nicht stillschweigend durch neue Rechenwege ersetzt werden.

## Testanforderungen

- Quellen lassen sich über den Client laden.
- Metriken lassen sich über `metrics:list` laden.
- jede registrierte Metrik verweist nur auf vorhandene Quellen-IDs.
- Szenarien lassen sich speichern, nach einem Reload wieder laden und löschen.
- der aktive Entwurf wird nach einem Reload vollständig wiederhergestellt.
- die aktive Szenario-ID bleibt erhalten.
- parallele Anfragen werden über Korrelations-IDs korrekt zugeordnet.
- Worker-Fehler blockieren die Oberfläche nicht dauerhaft.
- Playwright prüft Speichern, Laden, Autosave, Import, Export, Duplizieren und sichtbare Nachweise.

## Grenzen der lokalen Fassung

- keine Benutzerkonten,
- keine Synchronisierung zwischen Geräten,
- keine Konfliktauflösung,
- keine serverseitige unveränderliche Versionshistorie,
- keine vertraulichen Daten,
- keine öffentlichen Freigabelinks,
- Referenzdaten werden noch mit der Anwendung ausgeliefert,
- Demoquellen und Demonstrationsmetriken sind noch keine vollständig fachlich freigegebene Produktionsdatenbank.

## Verwandte Kapitel

- [Transparenzregister und Metrikvertrag](transparenzregister-und-metrikvertrag.md)
- [Zentrales Szenario- und Zustandsmodell](zentrales-szenario-und-zustandsmodell.md)
- [UI-Referenz und Nutzerflüsse](ui-referenz-und-nutzerfluesse.md)
- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Evidenzdatenbank](../06-evidenz/evidenzdatenbank.md)
- [Berechnungstransparenz](../06-evidenz/berechnungstransparenz.md)
