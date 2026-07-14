---
title: Automatische Standard-Modellbasis
summary: Nutzerablauf, Wiederverwendung und Fehlerbehandlung der automatisch bereitgestellten synthetischen Bevölkerung.
status: Implementiert 0.8
last_updated: 2026-07-14
---

# Automatische Standard-Modellbasis

## Zweck

Einkommensteuer, Bürgergeld und weitere verteilungsbezogene Berechnungen benötigen eine synthetische Bevölkerung. Diese fachliche Voraussetzung wird im Standardablauf automatisch bereitgestellt. Nutzer müssen vor einer Reformberechnung weder einen Seed wählen noch eine Stichprobe erzeugen oder einen Lauf aktivieren.

Die vollständige Verwaltung der synthetischen Bevölkerung bleibt als erweiterte Modellbasis erhalten. Automatisierung bedeutet keine Entfernung von Reproduzierbarkeit oder Prüfbarkeit.

## Versionierter Standard

Die Standard-Modellbasis wird durch vier Werte eindeutig beschrieben:

- Baseline-ID,
- Seed,
- Stichprobengröße,
- Modellversion.

Gleiche Werte erzeugen dieselbe synthetische Stichprobe. Der Standardlauf ist damit deterministisch und fachlich rekonstruierbar.

## Automatische Auswahl

Bei der ersten Berechnung mit Modellbevölkerung gilt folgende Reihenfolge:

1. Ein bereits aktiver Lauf wird verwendet, wenn er exakt dem Standardvertrag entspricht.
2. Andernfalls wird unter den lokal gespeicherten Läufen nach derselben Baseline, demselben Seed, derselben Stichprobengröße und derselben Modellversion gesucht.
3. Ein passender Lauf wird aktiviert und wiederverwendet.
4. Nur wenn kein passender Lauf existiert, wird die Standard-Modellbasis im Worker neu erzeugt.

Dadurch entstehen keine unnötigen Duplikate. Ein benutzerdefinierter aktiver Lauf wird nicht fälschlich als Standardbasis behandelt.

## Standardansicht

Normale Reformansichten zeigen nur einen verständlichen Status, beispielsweise:

- Modellbasis wird vorbereitet,
- Modellbasis bereit,
- Qualitätswarnung,
- ursprüngliche Modellbasis fehlt.

Seed, interne Lauf-ID und technische Modellversion gehören in die Prüfebene und nicht in den primären Reformablauf.

## Fehlende Szenarioreferenz

Verweist ein gespeichertes oder importiertes Szenario auf einen lokal nicht vorhandenen Lauf, wird diese Referenz nicht automatisch ersetzt. Eine andere Modellbasis kann Ergebnisse verändern und muss deshalb bewusst gewählt werden.

Eine identische Rekonstruktion ist möglich, wenn Baseline-ID, Seed, Stichprobengröße und Modellversion erhalten sind. Ein Wechsel auf die aktuelle Standard-Modellbasis ist eine ausdrückliche Szenarioänderung und muss als solche erklärt werden.

## Qualität und Grenzen

Eine Kalibrierungswarnung bleibt sichtbar. Sie blockiert die Berechnung nur, wenn Validierungsfehler den Lauf fachlich unbrauchbar machen. Die automatische Bereitstellung ändert weder Generator, Gewichtung noch Unsicherheitsregeln.

Die Modellbasis bleibt vollständig synthetisch. Sie enthält keine realen Personen und keine kopierten amtlichen Mikrodaten.

## Verwandte Kapitel

- [Synthetische Bevölkerung und Haushalte](synthetische-bevoelkerung.md)
- [Informationsarchitektur und progressive Offenlegung](../01-produkt/informationsarchitektur-und-progressive-offenlegung.md)
- [Einkommensteuer-Modul 2026](../02-fiskal/einkommensteuer-modul.md)
- [Bürgergeld- und Grundsicherungsgeld-Modul](../02-fiskal/buergergeld-modul.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
