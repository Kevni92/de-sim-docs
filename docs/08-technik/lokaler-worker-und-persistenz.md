---
title: Lokaler Worker und Persistenz
summary: Übergangsarchitektur für Quellen sowie Speichern und Laden ohne externen Server.
status: Arbeitsstand 0.4
last_updated: 2026-07-13
---

# Lokaler Worker und Persistenz

## Ziel

Die erste Projektphase verwendet keinen externen Anwendungsserver. Quellen sowie gespeicherte Szenarien werden über eine serverähnliche Schnittstelle angesprochen, deren Implementierung vollständig im Browser läuft.

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

- stellt fachlich benannte Methoden für Quellen und Szenarien bereit,
- erzeugt Korrelations-IDs für parallele Anfragen,
- übersetzt Worker-Antworten in Promises,
- kapselt Transportfehler.

### Web Worker

- simuliert die spätere Servergrenze,
- validiert und verteilt Anfragen,
- führt Datenbankzugriffe außerhalb des UI-Threads aus,
- liefert typisierte Erfolgs- oder Fehlerantworten.

### IndexedDB

- speichert Quellenmetadaten,
- speichert Szenarien inklusive Modellstufe und Änderungszeitpunkt,
- wird versioniert migriert,
- enthält keine geheime oder personenbezogene Information.

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

### ScenarioState

Ein Szenario enthält mindestens:

- stabile ID und Name,
- Erstellungs- und Änderungszeitpunkt,
- Modellstufe,
- geänderte Einnahmenparameter,
- geänderte Ausgabenparameter.

## Austauschbarkeit

Der UI-Code hängt ausschließlich vom Client-Vertrag ab. Eine spätere Serverimplementierung ersetzt den Worker-Transport durch HTTP oder RPC, ohne dass Fachkomponenten IndexedDB-Details kennen müssen.

Für die Migration gelten folgende Regeln:

1. Methoden und Ergebnisobjekte bleiben möglichst kompatibel.
2. Fehler werden weiterhin strukturiert zurückgegeben.
3. lokale Szenarien können exportiert und auf den Server übertragen werden.
4. Quellen-IDs bleiben stabil, damit gespeicherte Szenarien reproduzierbar bleiben.

## Testanforderungen

- Quellen lassen sich über den Client laden.
- Szenarien lassen sich speichern, nach einem Reload wieder laden und löschen.
- parallele Anfragen werden über Korrelations-IDs korrekt zugeordnet.
- Worker-Fehler blockieren die Oberfläche nicht dauerhaft.
- Playwright prüft die sichtbaren Speichern- und Laden-Abläufe.

## Grenzen der ersten Fassung

- keine Benutzerkonten,
- keine Synchronisierung zwischen Geräten,
- keine Konfliktauflösung,
- keine serverseitige Versionshistorie,
- keine vertraulichen Daten,
- Demoquellen sind noch keine fachlich freigegebene Produktionsdatenbank.

## Verwandte Kapitel

- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Evidenzdatenbank](../06-evidenz/evidenzdatenbank.md)
- [Berechnungstransparenz](../06-evidenz/berechnungstransparenz.md)
