---
title: Bürgergeld – verständlicher Standardmodus
summary: Politische Stellschrauben, vier Kernergebnisse und Übergang zum Expertenmodus.
status: Implementiert 0.2
last_updated: 2026-07-14
---

# Bürgergeld – verständlicher Standardmodus

Der Standardmodus übersetzt politische Entscheidungen in den bestehenden SGB-II-Parametersatz. Er besitzt keinen vereinfachten zweiten Rechenkern. Standard- und Expertenmodus speichern dieselben konkreten Werte und verwenden dieselbe Mikrosimulation.

## Politische Stellschrauben

- **Regelbedarfe verändern:** Alle monatlichen Regelbedarfe für Erwachsene und Kinder werden gemeinsam verändert. Ein Beispiel zeigt den neuen Monatsbetrag für eine alleinstehende Person.
- **Mehr vom Hinzuverdienst behalten:** Der anrechnungsfreie Grundbetrag wird direkt in Euro pro Monat eingestellt. Weitere Einkommensgrenzen und Freibetragssätze bleiben im Expertenmodus getrennt.
- **Unterkunft und Heizung anerkennen:** Integrierte Miet- und Heizgrenzen sowie der regionale Fallback werden verändert. Karenzzeiten, Karenzdeckel und Kostensenkungszeiträume bleiben davon unberührt.
- **Weitere Regelungen:** Mehrbedarfe sind eingeklappt erreichbar. Karenzzeiten, Leistungsminderungen und Sonderfälle bleiben konkrete Expertenthemen.

Regionale Fallbacks werden als hohe Unsicherheit gekennzeichnet. Eine Berliner Beispielgrenze darf nicht als bundesweit gültiger Wert verstanden werden.

## Vier Kernergebnisse

Der erste Ergebnisbereich zeigt höchstens:

1. staatliche Mehr- oder Minderausgaben pro Jahr,
2. betroffene Personen und Bedarfsgemeinschaften,
3. die durchschnittliche Änderung je gewichtetem Bezugsmonat,
4. Belastbarkeit und Unsicherheit.

Eine **Bedarfsgemeinschaft** ist ein Haushalt oder Teilhaushalt, dessen Anspruch gemeinsam berechnet wird. Die Monatswirkung ist ein aggregierter Orientierungswert und kein individueller Bescheid.

## Vertiefungen und Expertenmodus

Baseline, Leistungsbestandteile, Finanzierung, amtlicher Abgleich, Reproduzierbarkeit und Rechenweg erscheinen erst nach gezieltem Öffnen. Der Expertenmodus erhält alle Euro-, Prozent-, Monats-, Regional- und Minderungsparameter mit Quelle, Rechtsstand, Datenstand, Evidenz und Unsicherheit.

Abweichende Einzelwerte werden im Standardmodus als gemischter Expertenstand gekennzeichnet. Der Moduswechsel verliert keine Werte. Ein vollständiger Reset entfernt die SGB-II-Parameter-, Unterkunfts- und Finanzierungsänderungen.

## Automatische Berechnung

Nach jeder Änderung berechnet der lokale Worker die unmittelbare Zahlungswirkung automatisch auf der aktiven Modellbasis. Standardnutzer müssen weder eine Bevölkerungsseite öffnen noch einen Rechenlauf manuell starten. Direkte Zahlungswirkung und mögliche langfristige Folgewirkungen bleiben getrennt.

## Grenzen

Die Oberfläche ist keine individuelle Leistungsberatung. Ergebnisse hängen von synthetischer Bevölkerung, Regionaldaten, Bezugsverläufen und dokumentierten Fallbacks ab. Fehlende kommunale Daten erhöhen die Unsicherheit; eine Durchschnittswirkung ersetzt keine Einzelfallprüfung.

## Verwandte Kapitel

- [Bürgergeld – Bedienoberfläche und Szenarien](buergergeld-bedienoberflaeche.md)
- [Bürgergeld- und Grundsicherungsgeld-Modul](buergergeld-modul.md)
- [Unterkunft und Heizung – Berlin 2026](kdu-berlin-2026.md)
- [Automatische Standard-Modellbasis](../03-daten/standard-modellbasis.md)
