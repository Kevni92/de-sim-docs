---
title: Bürgergeld – Release-Validierung und Abnahme
summary: Reproduzierbarer Referenzlauf, amtlicher Haushaltsabgleich, Unsicherheitsband, Performancegrenzen und praktischer Abnahmeablauf.
status: Implementierungsdokumentation 0.1
last_updated: 2026-07-14
---

# Bürgergeld – Release-Validierung und Abnahme

## Zweck

Die Release-Validierung prüft das Bürgergeld-/Grundsicherungsgeld-Modul als vollständige Kette von der synthetischen Bevölkerung über Anspruch, Unterkunft und Heizung bis zur sichtbaren Ergebnisdarstellung. Sie ersetzt keine fachliche Evaluation, macht aber reproduzierbar sichtbar, welche Teile technisch stabil sind, welche amtlichen Vergleichsgrößen herangezogen werden und wo Abgrenzungsunterschiede verbleiben.

Die Abnahme verwendet keine freie Kalibriergröße. Abweichungen werden weder versteckt noch in den Modellwert zurückgeschrieben.

## Fester Referenzlauf

Der Referenzlauf wird durch folgende Angaben bestimmt:

- aktive Bevölkerungs-Lauf-ID und deren Seed,
- SGB-II-Policy `sgb2-policy-2026-07`,
- Modellversion,
- unveränderte Baseline-Parameter,
- Zeitraum Juli bis Dezember 2026,
- sortierte Bedarfsgemeinschaften und Personenprofile,
- deterministische Rundungs- und Restcent-Regeln.

Aus diesen Angaben und dem berechneten Baseline-Ergebnis entsteht ein kurzer Reproduzierbarkeitsschlüssel. Derselbe gespeicherte Bevölkerungslauf und derselbe Parametersatz müssen denselben Schlüssel und dieselben Centbeträge erzeugen. Ein anderer Seed oder ein geänderter Parameter führt bewusst zu einem anderen Schlüssel.

## Amtlicher Vergleich

Der sichtbare Abgleich nutzt die amtliche Haushaltsabgrenzung des Bundeshaushalts 2024 als externen Prüfanker:

| Vergleich | Amtlicher Wert | Modellsicht | Vergleichbarkeit |
|---|---:|---|---|
| Bürgergeld, Titel 1101 681 12 | 26,5 Mrd. € | Regelbedarf und Mehrbedarfe, auf zwölf Monate annualisiert | mittel |
| Beteiligung des Bundes an Unterkunft und Heizung, Titel 1101 632 11 | 11,1 Mrd. € | Bundesanteil von Unterkunft und Heizung, auf zwölf Monate annualisiert | mittel |

Die Werte sind keine Zielvorgabe und keine Kalibrierung. Der Rechtsstand des Modells ist Juli 2026, während die Referenz einen Ist-Haushaltswert 2024 abbildet. Außerdem enthält der Haushaltstitel Abgrenzungen, die nicht vollständig mit der personengenauen Modellkomponente übereinstimmen. Deshalb zeigt die Oberfläche für jeden Vergleich:

- amtlichen Referenzwert,
- annualisierten Modellwert,
- absolute und relative Abweichung,
- Vergleichbarkeitsklasse,
- Quelle,
- bekannte Zeit-, Rechts- und Systemgrenzen.

Regelbedarf und Mehrbedarfe sowie Unterkunft und Heizung bleiben im Modell weiterhin einzeln ausgewiesen. Wo die amtliche Quelle nur eine gemeinsame Titelabgrenzung liefert, wird diese Zusammenfassung ausdrücklich benannt und nicht künstlich auf Unterkomponenten verteilt.

## Qualitäts- und Unsicherheitsanzeige

Der Qualitätsstatus kombiniert technische und fachliche Signale:

- vollständige deterministische Berechnung,
- vorhandener amtlicher Vergleich,
- verwendete regionale KdU-Daten oder Modell-Fallbacks,
- Unsicherheitsklasse der Finanzierung und Wohnkosten,
- bekannte Modellgrenzen.

Für die sichtbare Ergebniszahl wird ein illustratives Unsicherheitsband ausgewiesen:

- mittlere Unsicherheit: ±10 Prozent,
- hohe Unsicherheit: ±20 Prozent.

Das Band ist kein statistisches Konfidenzintervall. Es ist eine transparente Sensitivitätskennzeichnung für die derzeitige Modellreife. Die Oberfläche nennt diese Einschränkung ausdrücklich.

## Performancegrenzen

Die lokale Vorschau misst die tatsächliche Berechnungsdauer sowie die Zahl der simulierten Bedarfsgemeinschaftsmonate. Für die Release-Abnahme gelten folgende Orientierungsgrenzen:

| Lauf | Umfang | Zielwert |
|---|---:|---:|
| Standardtest | 2.000 synthetische Personen | höchstens 15 Sekunden |
| große Stichprobe | 10.000 synthetische Personen | höchstens 60 Sekunden |

Die Grenzen sind Warnschwellen und keine fachlichen Parameter. Eine Überschreitung verändert das Ergebnis nicht, muss aber in der Abnahme dokumentiert werden.

## Persistenz und Wiederherstellung

Der kanonische SGB-II-Szenariozustand muss erhalten bleiben bei:

- automatischer Speicherung in IndexedDB,
- Neuladen der Anwendung,
- Rückgängig- und Wiederholen-Funktionen,
- Szenarioexport und -import,
- Migration älterer Sozialindex-Szenarien,
- Wiederherstellung der Baseline.

Die Reproduzierbarkeit bezieht sich auf einen gespeicherten Bevölkerungslauf. Wird der Lauf neu erzeugt, ist ein anderer Schlüssel erwartbar, selbst wenn dieselbe sichtbare Stichprobengröße gewählt wurde.

## Automatisierte Prüfungen

Die Release-Abnahme umfasst mindestens:

- TypeScript-Typecheck,
- Produktions-Build,
- Unit-Tests für Anspruch, Unterkunft, Aggregation, UI und Release-Validierung,
- Playwright-Tests auf Desktop und Mobil,
- sichtbaren amtlichen Abgleich,
- sichtbaren Reproduzierbarkeitsschlüssel,
- Persistenz eines geänderten Parameters,
- aktuellen Screenshot aus einem echten Browserlauf.

## Praktischer Abnahmeablauf

1. Anwendung öffnen und zu **Bevölkerung** wechseln.
2. Eine Stichprobe mit 2.000 Personen und festem Seed erzeugen oder den vorhandenen Referenzlauf aktivieren.
3. Zum Dashboard zurückkehren und **Bürgergeld bearbeiten** öffnen.
4. Prüfen, dass Baseline, Leistungsbestandteile, Kostenträger, Qualitätsstatus, Unsicherheitsband und Reproduzierbarkeitsschlüssel sichtbar sind.
5. Den Abschnitt **Amtlicher Abgleich** öffnen und Referenzwert, Modellwert, Abweichung, Vergleichbarkeit und Abgrenzungsgründe prüfen.
6. Im Einfachmodus die Regelbedarfe auf 105 Prozent setzen und die Änderung der Komponenten kontrollieren.
7. In den Expertenmodus wechseln und prüfen, dass der konkrete Wert für Alleinstehende denselben kanonischen Parametersatz zeigt.
8. Seite neu laden und kontrollieren, dass der Wert erhalten bleibt.
9. Baseline wiederherstellen und prüfen, dass die Abweichung zum unveränderten Referenzlauf zurückkehrt.
10. Desktop- und Mobilansicht prüfen; der Abgleich muss ohne Informationsverlust erreichbar bleiben.

## Bekannte Modelllücken

- Die amtlichen Haushaltswerte 2024 und der Rechtsstand Juli 2026 sind nur teilweise vergleichbar.
- Amtliche Titel trennen Regelbedarf und Mehrbedarfe beziehungsweise Unterkunft und Heizung nicht in derselben Granularität wie das Modell.
- Kommunale KdU-Werte liegen noch nicht flächendeckend vor; Fallbacks erhöhen die Unsicherheit.
- Nichtinanspruchnahme, Verwaltungskosten, Eingliederungsleistungen, Kranken- und Pflegeversicherungsbeiträge sowie langfristige Verhaltenswirkungen sind nicht Bestandteil des direkten Zahlungsanspruchs.
- Das Unsicherheitsband ist eine dokumentierte Sensitivitätskennzeichnung und kein empirisch geschätztes Konfidenzintervall.

## Quellen

- [Bundeshaushalt digital](https://www.bundeshaushalt.de/)
- [Statistik der Bundesagentur für Arbeit: Leistungen, Einkommen, Bedarfe und Wohnkosten](https://statistik.arbeitsagentur.de/DE/Navigation/Statistiken/Fachstatistiken/Grundsicherung-fuer-Arbeitsuchende-SGBII/Leistungen-Einkommen-Bedarfe-Wohnkosten/Leistungen-Einkommen-Bedarfe-Wohnkosten-Nav.html)
- [Bürgergeld- und Grundsicherungsgeld-Modul](buergergeld-modul.md)
- [Bürgergeld – Bedienoberfläche und Szenarien](buergergeld-bedienoberflaeche.md)
