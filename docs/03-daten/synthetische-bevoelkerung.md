---
title: Synthetische Bevölkerung und Modellbasis
summary: Fachliche Beschreibung der automatisch verwendeten synthetischen Modellbasis, ihrer Erzeugung, Kalibrierung, Verwaltung und Grenzen.
status: Implementiert 0.8
last_updated: 2026-07-14
---

# Synthetische Bevölkerung und Modellbasis

## Ziel und Abgrenzung

Der Deutschland-Simulator verwendet eine gemeinsame, gewichtete und vollständig synthetische Bevölkerung als Modellbasis für Verteilungs-, Steuer- und Leistungsberechnungen. Die Datensätze bilden statistische Randverteilungen und fachlich plausible Zusammenhänge ab, enthalten aber **keine echten Personen und keine kopierten amtlichen Mikrodaten**.

Für normale Reformabläufe wird diese Modellbasis automatisch bereitgestellt. Nutzende müssen weder einen Seed auswählen noch eine Stichprobe erzeugen oder einen Lauf aktivieren. Die vollständige Verwaltung bleibt in der erweiterten Prüfebene **Modellbasis und Bevölkerung** erhalten.

Ein synthetischer Datensatz repräsentiert über sein Gewicht viele vergleichbare Personen oder Haushalte. Die Standardbasis umfasst 10.000 synthetische Personen. Sie ist groß genug für Gruppen- und Dezilauswertungen und bleibt im Browser-Worker handhabbar.

Nicht Bestandteil sind:

- eine dynamische Demografie mit Geburten und Sterbefällen,
- kausale Verhaltens- oder Langfristprognosen,
- eine vollständige Regionalisierung unterhalb der Bundesländer,
- individuelle Steuer-, Beitrags- oder Leistungsberatung,
- eine perfekte multivariate Repräsentation aller Merkmalskombinationen.

## Standardbasis und erweiterte Verwaltung

### Automatische Standardbasis

Wenn eine Einkommensteuer- oder Bürgergeldberechnung erstmals eine Bevölkerung benötigt und das Szenario noch keine Referenz besitzt, stellt der Worker automatisch eine versionierte Standardbasis bereit.

Die Standardparameter sind fest definiert:

- Seed: `de-sim-2025`,
- Stichprobengröße: 10.000 Personen,
- Baseline: `de-2024-2025-v1`,
- Modellversion: `synthetic-population-0.7.0`.

Seed, Stichprobengröße, Baseline und Modellversion bilden gemeinsam eine deterministische Lauf-ID. Ein lokal bereits vorhandener passender Lauf wird wiederverwendet und nicht dupliziert. Fehlt er, wird er im Worker erzeugt und in IndexedDB gespeichert.

Normale Reformansichten zeigen nur einen verständlichen Zustand:

- **Modellbasis wird vorbereitet**,
- **Modellbasis bereit**,
- **bereit mit Qualitätswarnung**,
- **ursprüngliche Referenz fehlt**,
- **Modellbasis konnte nicht geladen werden**.

Technische Lauf-ID, Seed, Stichprobengröße und interne Modellversion erscheinen dort nicht.

### Erweiterte Prüfebene

Unter **Modellbasis und Bevölkerung** bleiben vollständig erreichbar:

- aktive Lauf-ID und Qualitätsstatus,
- Seed, Stichprobengröße, Baseline und Modellversion,
- manuelle Neugenerierung,
- gespeicherte Läufe,
- gewichtete Verteilungen,
- Kalibrierungsbericht,
- Quellen, Datenschutz und Modellgrenzen.

Eine manuell erzeugte oder aktivierte Modellbasis ist eine weitreichende Szenarioänderung. Die neue Referenz wird im Szenario gespeichert, weil sich Steuer-, Verteilungs- oder Leistungswerte verändern können.

## Fehlende Szenarioreferenz

Ein gespeichertes oder importiertes Szenario kann auf einen Lauf verweisen, der auf dem aktuellen Gerät nicht vorhanden ist. Die Anwendung ersetzt diese Referenz niemals stillschweigend.

### Identische Rekonstruktion

Eine identische Rekonstruktion wird nur angeboten, wenn folgende Angaben vollständig vorhanden und mit der aktuellen Modellversion vereinbar sind:

- ursprüngliche Lauf-ID,
- Modellversion,
- Seed,
- Stichprobengröße,
- Baseline-ID.

Die Anwendung berechnet aus diesen Angaben die erwartete deterministische Lauf-ID. Nur wenn sie mit der gespeicherten Referenz übereinstimmt, kann **Identische Modellbasis neu erzeugen** verwendet werden.

### Bewusster Wechsel auf die Standardbasis

Sind die Rekonstruktionsdaten unvollständig oder stammt das Szenario aus einer älteren Modellversion, bleibt die ursprüngliche Referenz erhalten. Nutzende können bewusst **Standard-Modellbasis verwenden** wählen. Vor der Übernahme wird erklärt, dass sich Ergebnisse dadurch verändern können. Erst nach dieser Entscheidung werden Bevölkerungs- und SGB-II-Referenz des Szenarios aktualisiert.

## Vollständige Synthetizität und Datenschutz

Erzeugt und gespeichert werden keine Namen, Adressen, vollständigen Geburtsdaten, Arbeitgeber, Kontodaten oder anderen identifizierenden Merkmale. Die IDs von Personen und Haushalten sind rein synthetisch und nur innerhalb eines Generationslaufs gültig.

Amtliche oder wissenschaftliche Quellen liefern ausschließlich Randziele, Definitionen und Plausibilitätsrahmen. Der Generator rekonstruiert daraus keine realen Einzelfälle. Auch bei identischem Seed entsteht keine reale Person, sondern dieselbe reproduzierbare Modellstichprobe.

## Datenmodell

### Synthetische Person

Eine Person enthält unter anderem Alter und Altersgruppe, Haushaltsrolle, Erwerbs- und Arbeitszeitstatus, modellierte Einkommensarten, Gewicht, Bundesland, Stadt-Land-Kategorie und Einkommensdezil.

### Synthetischer Haushalt

Ein Haushalt enthält unter anderem Haushaltstyp, Zahl der Erwachsenen und Kinder, Erwerbskonstellation, Einkommen, Transferkomponenten, Wohnstatus und Wohnkosten, Vermögen, Schulden, Region sowie Haushaltsgewicht.

Unterstützt werden alleinlebende Personen, Paare ohne Kinder, Paare mit Kindern, Alleinerziehende, Mehrpersonenhaushalte und Rentnerhaushalte.

### Generationslauf

Jeder Lauf dokumentiert:

- Lauf-ID, Schema- und Modellversion,
- expliziten Seed,
- Erstellungszeitpunkt,
- Daten- und Rechtsstand,
- Baseline- und Quellen-IDs,
- Stichprobengröße,
- gewichtete Bevölkerung und Haushaltszahl,
- Kalibrierungsverfahren,
- Qualitätsmetriken,
- bekannte Einschränkungen.

## Deterministische Erzeugung

Die Erzeugung nutzt einen eigenen deterministischen Pseudozufallszahlengenerator. `Math.random()` ist nicht Bestandteil des fachlichen Generators.

Gleicher Seed, gleiche Baseline, gleiche Stichprobengröße und gleiche Modellversion erzeugen dieselben synthetischen Personen, Haushalte, Bedarfsgemeinschaften und Zusammenfassungen. Ein anderer Seed verändert die Mikrodaten, während kalibrierte Randverteilungen innerhalb der dokumentierten Toleranzen bleiben sollen.

Die Generierung und Aggregation laufen im Web Worker und blockieren nicht den React-Hauptthread.

## Erzeugungsverfahren

Der Generator arbeitet in mehreren Schritten:

1. Seed, Baseline, Stichprobengröße und Modellversion werden zu einem stabilen Zufallszustand kombiniert.
2. Haushaltstyp, Region, Gemeindetyp und Wohnstatus werden gezogen.
3. Erwachsene und Kinder werden mit konsistenter Haushaltsstruktur erzeugt.
4. Alter, Erwerbsstatus, Arbeitszeit und Einkommen werden regelbasiert verknüpft.
5. Wohnkosten, Vermögen und Schulden werden aus begrenzten Modellverteilungen abgeleitet.
6. Personen werden Einkommensdezilen zugeordnet.
7. Personen- und Haushaltsgewichte werden kalibriert.
8. Konsistenzregeln, Zusammenfassungen und Qualitätsmetriken werden berechnet.

Die gemeinsame Verteilung ist eine Modellkonstruktion und keine Kopie einer Mehrzweck-Haushaltsbefragung.

## Kalibrierung und Gewichtung

Die Gewichte werden durch 40 Runden iterativen proportionalen Anpassens an Randverteilungen angepasst. Kalibriert werden mindestens Altersgruppen, Haushaltstypen, Haushaltsgrößen, Erwerbsstatus, Einkommensdezile, Kinderzahl, Bundesländer, Stadt-Land-Kategorie sowie Miete und Eigentum.

Jede Kategorie erhält Zielwert, synthetischen Istwert, Abweichung, Toleranz, Status und Quelle. Überschreitungen werden als Warnung sichtbar hervorgehoben. Eine Warnung blockiert die Berechnung nicht automatisch; strukturelle Validierungsfehler dürfen dagegen keine fachlich unbrauchbare Basis freigeben.

Raking trifft Randverteilungen, aber nicht automatisch alle mehrdimensionalen Abhängigkeiten. Aus einer guten Alters- und Einkommenskalibrierung folgt daher nicht, dass jede Kombination aus Alter, Haushaltstyp, Region und Einkommen repräsentativ ist.

## Verwendung in Einkommensteuer und Bürgergeld

Die gesetzliche Einkommensteuerformel bleibt unabhängig von der Bevölkerungskomponente. Die Modellbasis liefert gewichtete Steuerhaushalte für Aufkommen, Gewinner und Verlierer, Dezile, Medianwirkung und betroffene Steuerfälle.

Für Bürgergeld werden aus denselben synthetischen Haushalten versionierte Personenprofile, Bedarfsgemeinschaften, Wohnkosten, Bezugsmonate und Gewichte abgeleitet. Die automatische Basis wird vor der ersten Vorschau geladen oder erzeugt; ein manueller Besuch der Prüfebene ist nicht erforderlich.

## Lokale Speicherung und Szenarien

Personen, Haushalte, Laufmetadaten, Kalibrierungsbericht und Validierung liegen in getrennten versionierten IndexedDB-Stores. Ein Szenario speichert:

- Lauf-ID,
- Modellversion,
- Seed,
- Stichprobengröße,
- Baseline-ID,
- zugehörige SGB-II-Referenz.

Diese Metadaten ermöglichen die Prüfung und – sofern kompatibel – identische Rekonstruktion. Undo und Redo kopieren keine Personendatensätze, sondern nur Referenz und Konfiguration. JSON-Export und -Import erhalten die vollständige Modellbasisreferenz.

Sämtliche Daten verbleiben lokal im Browser; es werden keine synthetischen Einzeldaten an einen externen Dienst übertragen.

## Interpretation und bekannte Grenzen

Die synthetische Bevölkerung ist geeignet, Modellwirkungen konsistent nach Gruppen zu vergleichen. Sie ist nicht geeignet, Aussagen über konkrete Personen oder kleine Orte zu treffen, seltene Merkmalskombinationen exakt abzubilden, Vermögensspitzen präzise zu schätzen oder kausale Verhaltensänderungen vorherzusagen.

Ergebnisse sind deshalb zusammen mit Datenstand, Modellstatus, Kalibrierung, Unsicherheit und Einschränkungen zu lesen.

## Verwandte Kapitel

- [Informationsarchitektur und progressive Offenlegung](../01-produkt/informationsarchitektur-und-progressive-offenlegung.md)
- [Einkommensteuer-Modul 2026](../02-fiskal/einkommensteuer-modul.md)
- [Bürgergeld-Modul](../02-fiskal/buergergeld-modul.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
