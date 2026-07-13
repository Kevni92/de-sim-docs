---
title: UI-Referenz und Nutzerflüsse
summary: Verbindliche Übernahme der Staat-sKlarheit-Oberfläche als Anwendungsbasis.
status: Arbeitsstand 0.6
last_updated: 2026-07-13
---

# UI-Referenz und Nutzerflüsse

## Ziel

Die Anwendung `Kevni92/de-sim` verwendet die ausgearbeitete Oberfläche aus `Kevni92/staat-sklarheit` als verbindliche visuelle und interaktive Grundlage. Milestone 1 ist bewusst kein Redesign. Bestehende Interaktionsmuster werden übernommen und nur dort angepasst, wo Persistenz, Barrierefreiheit, Responsive Design oder die spätere fachliche Modellierung dies erfordern.

## Verbindliche Gestaltung

Beibehalten werden insbesondere:

- neutrales Türkis als Primärfarbe,
- helle, flache Karten mit kleinen Radien,
- tabellarische und zahlenorientierte Darstellung,
- kompakte Typografie mit tabellarischen Ziffern,
- getrennte Farben für positive, negative und unsichere Wirkungen,
- Konfidenzanzeige zusätzlich zur Farbe,
- Quellen- und Methodikansicht als seitlicher Drawer,
- Drei-Spalten-Dashboard auf großen Bildschirmen,
- Tab-Navigation auf kleinen Bildschirmen.

## Hauptseiten

### Onboarding

Das Onboarding erklärt Zweck und Grenzen des Simulators. Nutzer wählen:

- Rechtsstand,
- Modellstufe,
- Einstieg in die Simulation.

Die Modellstufen `statisch`, `mit Verhaltenseffekt` und `Langfristszenario` werden bereits sichtbar getrennt, auch wenn die Werte in Milestone 1 noch Demonstrationswerte sind.

### Dashboard

Das Desktop-Dashboard ist dreigeteilt:

1. Einnahmen und Steuern links,
2. Wirkungsdarstellung und Diagramme in der Mitte,
3. Staatsausgaben rechts.

Oberhalb bleiben Einnahmen, Ausgaben, Saldo und Schuldenstand sichtbar. Die mittlere Ansicht bietet die Reiter:

- Budget,
- Haushalte,
- Verteilung,
- Regionen,
- Zeitverlauf.

Auf mobilen Geräten werden Einnahmen, Ergebnis, Ausgaben und Szenario als vier Hauptreiter dargestellt.

### Einkommensteuer

Die erste Detailansicht enthält veränderbare Demonstrationsparameter für:

- Grundfreibetrag,
- Eingangssteuersatz,
- Spitzensteuersatz,
- Schwelle des Spitzensteuersatzes,
- Reichensteuersatz,
- Kinderfreibetrag,
- Ehegattensplitting.

Die Oberfläche zeigt unmittelbar aktualisierte Kennzahlen, Tarifkurve, Einkommensdezile und Beispielhaushalte. Die dahinterliegende vereinfachte Demoformel ist noch kein fachlich freigegebenes Steuermodell.

### Szenariovergleich

Der Vergleich stellt Status quo, aktuelles Szenario und ein alternatives Demonstrationsszenario nebeneinander. Unterschiede werden hervorgehoben, aber nicht politisch bewertet.

### Quellen-Drawer

Jede zentrale Kennzahl kann einen Drawer öffnen. Dieser zeigt mindestens:

- Institution,
- Datenjahr,
- Rechtsstand,
- Quellenstatus,
- Konfidenz,
- Zusammenfassung,
- Rechenlogik,
- bekannte Grenzen,
- Link zur Originalquelle.

### Szenarioverwaltung

Milestone 2 ergänzt einen zweiten Drawer für den vollständigen Szenariozustand. Er enthält:

- Name und Beschreibung,
- Rechtsstand und Datenstand,
- Zeithorizont,
- Modellstufe,
- explizite Annahmen,
- Modellversion,
- referenzierte Quellen-IDs,
- Aktionen für Neu, Duplizieren, Import, Export und Kopieren.

Die Szenarioverwaltung verwendet dieselbe Drawer-Struktur, Typografie, Farbgebung und Mobile-Logik wie die Quellenansicht.

## Lokale Persistenz

Szenarien und der aktive Entwurf werden ausschließlich über die definierte lokale Servergrenze gespeichert:

```text
React-Oberfläche
  → LocalServerClient
    → Web Worker
      → IndexedDB
```

Die UI greift nicht direkt auf IndexedDB zu. Rückgängig, Wiederholen und die automatische Wiederherstellung arbeiten auf dem zentralen Szenariozustand.

## Abgrenzung von Milestone 1 und 2

Milestone 1 liefert die vollständige visuelle und navigierbare Anwendungsbasis. Milestone 2 ergänzt das zentrale Zustands- und Lebenszyklusmodell.

Noch nicht Bestandteil sind:

- amtlich kalibrierte Steuerberechnungen,
- synthetische Bevölkerung,
- belastbare Verhaltensmodelle,
- echte Regionalberechnungen,
- langfristige Demografiemodelle,
- produktionsreife Quellen- und Evidenzdatenbank.

Sämtliche noch nicht validierten Werte müssen sichtbar als Demonstrationswerte gekennzeichnet bleiben.

## Testanforderungen

Playwright prüft mindestens:

- Onboarding und Einstieg ins Dashboard,
- Desktop-Dashboard,
- mobile Hauptreiter,
- Navigation zur Einkommensteuer,
- Live-Änderung eines Parameters,
- Quellen-Drawer,
- Szenarioverwaltung,
- Rückgängig und Wiederholen,
- Autosave und Reload,
- Speichern, Laden und Duplizieren,
- JSON-Import und JSON-Export,
- Szenariovergleich.

## Verwandte Kapitel

- [Zentrales Szenario- und Zustandsmodell](zentrales-szenario-und-zustandsmodell.md)
- [Lokaler Worker und Persistenz](lokaler-worker-und-persistenz.md)
- [Technische Architektur](technische-architektur.md)
- [Berechnungstransparenz](../06-evidenz/berechnungstransparenz.md)
- [Unsicherheit und Szenarien](../06-evidenz/unsicherheit-szenarien.md)
