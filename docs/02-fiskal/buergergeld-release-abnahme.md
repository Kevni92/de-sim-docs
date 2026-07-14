# Bürgergeld: Release-Abnahme 0.1

## Zweck

Die Release-Abnahme prüft die vollständige Rechenkette von der synthetischen Bevölkerung über Anspruch und Wohnkosten bis zur jährlichen Ausgabenanzeige. Sie bestätigt Reproduzierbarkeit, sichtbare Abweichungen und dokumentierte Modellgrenzen; sie behauptet keine Identität zwischen Modell- und Haushaltswerten.

## Referenzlauf und Jahresrate

Ein Lauf wird durch Seed, Stichprobengröße, Modell- und Policy-Versionen, Parameter, regionale Wohnkostenregeln und Bezugsmonate bestimmt. Daraus entsteht ein stabiler Fingerabdruck. Die Rechtsbaseline beginnt im Juli 2026; die Oberfläche zeigt deshalb ausdrücklich die Hochrechnung `Juli bis Dezember × 12 / 6`.

## Komponenten und Vergleich

Regelbedarf, Mehrbedarfe, Unterkunft und Heizung werden getrennt ausgewiesen. Für Vergleichsrahmen erscheinen Modellwert, Referenzwert, absolute und relative Abweichung, Vergleichbarkeit sowie bekannte Ursachen. Die verwendeten Haushaltsrahmen von 46,9 Mrd. Euro für Lebensunterhalt und 6,9 Mrd. Euro für Unterkunft und Heizung sind nur eingeschränkt vergleichbar. Bestands-/Stichtagsbezug, föderale Finanzierung, nicht enthaltene Leistungen, synthetische Verteilungen, regionale Fallbacks und nicht modellierte Nichtinanspruchnahme bleiben sichtbar. Eine freie Kalibriergröße bleibt null.

## Unsicherheit

Die Komponenten erhalten dokumentierte Sensitivitätsbänder: Regelbedarf ±8 Prozent, Mehrbedarfe ±30 Prozent, Unterkunft ±18 Prozent und Heizung ±25 Prozent. Diese Bänder sind keine statistischen Konfidenzintervalle.

## Qualitäts- und Performanceprüfung

Der Bericht prüft Fingerabdruck, Komponentenzerlegung, Referenzabgleich, Null-Kalibrierung, Unsicherheit und Laufzeit. Die Budgets betragen 6 Sekunden für 2.000, 20 Sekunden für 10.000 und 75 Sekunden für 50.000 Personen. Die Vorschau aggregiert fortlaufend, damit Monatsresultate großer Läufe nicht vollständig gleichzeitig im Speicher liegen.

## Technische Abnahme

Vor der Freigabe werden Typecheck, Produktions-Bundle, Unit- und Invariantentests, Performance mit 2.000 und 50.000 Personen, Desktop und Mobil, Barrierefreiheit, Szenarioexport/-import, Wiederherstellung sowie aktuelle Screenshots geprüft. Draft-PRs führen die schnelle Qualitätsprüfung aus; Performance und Playwright starten bei Review-Freigabe und auf `main`. Eine Concurrency-Gruppe beendet veraltete Läufe.

## Praktischer Test

1. Bevölkerung mit Seed `sgb2-release-e2e` und 2.000 Personen erzeugen.
2. Bürgergeld öffnen und Fingerabdruck, Status, Laufzeit und Hochrechnungsfaktor prüfen.
3. Vergleichsursachen und Sensitivitätsbänder öffnen.
4. Regelbedarfe auf 105 Prozent ändern und den neuen Fingerabdruck prüfen.
5. Szenario exportieren, Baseline herstellen, importieren und die Wiederherstellung prüfen.
6. Desktop, Mobil und Quellenzugang kontrollieren.

## Grenzen

Verwaltungskosten, Eingliederungsleistungen sowie indirekte Arbeitsmarkt-, Verhaltens- und Demografieeffekte gehören nicht zu dieser ersten Ausbaustufe. Vermögens- und medizinisch beziehungsweise verwaltungsrechtlich geprägte Einzelfälle sind nur innerhalb der dokumentierten Modellabdeckung belastbar.
