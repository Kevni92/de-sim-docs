---
title: UI-Referenz und Nutzerflüsse
summary: Verbindliche Staat-sKlarheit-Oberfläche mit Szenario- und Transparenzfunktionen.
status: Arbeitsstand 0.7
last_updated: 2026-07-13
---

# UI-Referenz und Nutzerflüsse

## Ziel

Die Anwendung `Kevni92/de-sim` verwendet die ausgearbeitete Oberfläche aus `Kevni92/staat-sklarheit` als verbindliche visuelle und interaktive Grundlage. Die Anwendung wird funktional erweitert, ohne das bestehende Erscheinungsbild neu zu entwerfen.

Anpassungen sind zulässig, wenn sie Persistenz, Nachvollziehbarkeit, Barrierefreiheit, Responsive Design oder die fachliche Modellierung unterstützen.

## Verbindliche Gestaltung

Beibehalten werden insbesondere:

- neutrales Türkis als Primärfarbe,
- helle, flache Karten mit kleinen Radien,
- tabellarische und zahlenorientierte Darstellung,
- kompakte Typografie mit tabellarischen Ziffern,
- getrennte Farben für positive, negative und unsichere Wirkungen,
- Status und Konfidenz zusätzlich zur Farbe,
- Nachweis- und Szenarioansichten als seitliche Drawer,
- Drei-Spalten-Dashboard auf großen Bildschirmen,
- Tab-Navigation auf kleinen Bildschirmen.

## Hauptseiten

### Onboarding

Das Onboarding erklärt Zweck und Grenzen des Simulators. Nutzer wählen:

- Rechtsstand,
- Modellstufe,
- Einstieg in die Simulation.

Die Modellstufen `statisch`, `mit Verhaltenseffekt` und `Langfristszenario` werden sichtbar getrennt. Nicht fachlich kalibrierte Werte bleiben als Demonstrationswerte gekennzeichnet.

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

Zentrale KPIs und fachliche Darstellungen besitzen einen Quellen- beziehungsweise Nachweisbutton. Dieser öffnet die konkret zugehörige Metrik und nicht nur eine allgemeine Startseite der Institution.

### Einkommensteuer

Die erste Detailansicht enthält veränderbare Demonstrationsparameter für:

- Grundfreibetrag,
- Eingangssteuersatz,
- Spitzensteuersatz,
- Schwelle des Spitzensteuersatzes,
- Reichensteuersatz,
- Kinderfreibetrag,
- Ehegattensplitting.

Die Oberfläche zeigt unmittelbar aktualisierte Kennzahlen, Tarifkurve, Einkommensdezile und Beispielhaushalte. Steueraufkommen, Gewinner, Verlierer, Medianwirkung, Tarifkurve, Verteilung und Beispielhaushalte sind jeweils mit einem Nachweis verknüpft.

Die vereinfachte Demoformel ist noch kein fachlich freigegebenes Steuermodell und wird im Nachweis als Modellrechnung oder Annahme gekennzeichnet.

### Szenariovergleich

Der Vergleich stellt Status quo, aktuelles Szenario und ein alternatives Demonstrationsszenario nebeneinander. Unterschiede werden hervorgehoben, aber nicht politisch bewertet.

### Transparenzregister

Milestone 3 ergänzt **Transparenz** als eigene Hauptseite. Sie enthält:

- Anzahl amtlicher Grundlagen,
- Anzahl von Modellrechnungen,
- Anzahl expliziter Annahmen,
- Anzahl verknüpfter Originalquellen,
- Suchfeld für Name, Kategorie, Beschreibung und Formel,
- Statusfilter,
- Karten für registrierte Kennzahlen,
- aktuellen Szenariowert,
- Datenjahr, Rechtsstand und Quellenanzahl,
- Einstieg in den vollständigen Nachweis.

Die Seite ist kein separates Designsystem. Sie verwendet dieselben Karten, Abstände, Farben, Typografie und Buttons wie Dashboard und Detailseiten.

### Nachweis-Drawer

Der frühere Quellen-Drawer wird zu einem vollständigen Nachweis-Drawer erweitert. Er zeigt:

1. Name der Kennzahl,
2. Evidenzstatus und Konfidenz,
3. aktuell angezeigten Szenariowert,
4. Kategorie, Datenjahr und Rechtsstand,
5. aktive Modellversion und Zeithorizont,
6. fachliche Definition,
7. Gesamtformel,
8. nummerierte Rechenschritte,
9. verwendete Parameter und Provenienz,
10. Unsicherheit oder begründete Nichtanwendbarkeit,
11. Originalquellen mit Institution und Link,
12. bekannte Grenzen,
13. Änderungsverlauf.

Der Drawer schließt über:

- den sichtbaren Schließen-Button,
- Klick auf den Hintergrund,
- Escape-Taste.

Auf kleinen Bildschirmen nutzt er die vollständige verfügbare Breite.

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

Die Szenarioverwaltung verwendet dieselbe Drawer-Struktur, Typografie, Farbgebung und Mobile-Logik wie die Nachweisansicht.

## Lokale Persistenz

Szenarien, aktiver Entwurf, Quellen und Metriknachweise werden ausschließlich über die definierte lokale Servergrenze angesprochen:

```text
React-Oberfläche
  → LocalServerClient
    → Web Worker
      → IndexedDB
```

Die UI greift nicht direkt auf IndexedDB zu. Rückgängig, Wiederholen und die automatische Wiederherstellung arbeiten auf dem zentralen Szenariozustand.

## Abgrenzung der Milestones

- Milestone 1 liefert die visuelle und navigierbare Anwendungsbasis.
- Milestone 2 ergänzt das zentrale Zustands- und Lebenszyklusmodell.
- Milestone 3 ergänzt strukturierte Nachweise und das Transparenzregister.

Noch nicht Bestandteil sind:

- amtlich kalibrierte vollständige Steuerberechnungen,
- synthetische Bevölkerung,
- belastbare Verhaltensmodelle,
- echte Regionalberechnungen,
- langfristige Demografiemodelle,
- serverseitige unveränderliche Modellhistorie.

Sämtliche noch nicht validierten Werte müssen sichtbar als Demonstrationswerte, Modellrechnung oder Annahme gekennzeichnet bleiben.

## Testanforderungen

Playwright prüft mindestens:

- Onboarding und Einstieg ins Dashboard,
- Desktop-Dashboard,
- mobile Hauptreiter,
- Navigation zur Einkommensteuer,
- Live-Änderung eines Parameters,
- Öffnen eines Nachweises aus dem Dashboard,
- Navigation zum Transparenzregister,
- Suche und Statusfilter,
- Formel, Rechenschritte und Parameter,
- Unsicherheitsdarstellung,
- Originalquellen und Grenzen,
- Änderungsverlauf,
- Szenarioverwaltung,
- Rückgängig und Wiederholen,
- Autosave und Reload,
- Speichern, Laden und Duplizieren,
- JSON-Import und JSON-Export,
- Szenariovergleich.

Sichtbare Änderungen am Transparenzregister werden in CI durch einen echten Playwright-Screenshot dokumentiert.

## Verwandte Kapitel

- [Transparenzregister und Metrikvertrag](transparenzregister-und-metrikvertrag.md)
- [Zentrales Szenario- und Zustandsmodell](zentrales-szenario-und-zustandsmodell.md)
- [Lokaler Worker und Persistenz](lokaler-worker-und-persistenz.md)
- [Technische Architektur](technische-architektur.md)
- [Berechnungstransparenz](../06-evidenz/berechnungstransparenz.md)
- [Unsicherheit und Szenarien](../06-evidenz/unsicherheit-szenarien.md)
