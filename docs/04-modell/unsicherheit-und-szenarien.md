---
title: Unsicherheit und Szenarien
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.5
last_updated: 2026-10-23
---

# 16. Unsicherheit und Szenarien

## 16.1 Drei Ergebnisebenen

Die Anwendung verwendet in der Szenarioverwaltung verständliche Bezeichnungen. Die internen Werte bleiben für Persistenz und Reproduzierbarkeit erhalten:

- **Nur direkte Wirkung** (`statisch`): hohe Nachvollziehbarkeit, keine Verhaltensänderung.
- **Mit kurzfristigen Reaktionen** (`verhalten`): dokumentierte Reaktionen von Haushalten und Unternehmen sowie begrenzte Folgewirkungen.
- **Langfristiges Szenario** (`langfrist`): Demografie, Humankapital, Wachstum und Rückkopplungen mit höherer Unsicherheit.

Modellstufe und Zeithorizont gelten zentral für das gesamte Szenario. Fachseiten zeigen sie schreibgeschützt an und führen keine unabhängigen lokalen Varianten. Langfristige Ergebnisse sind Szenariopfade und keine sichere Prognose.

## 16.2 Bandbreiten

Ergebnisse werden als zentrale Schätzung und Bandbreite dargestellt. Die Bandbreite kann aus Konfidenzintervallen, alternativen Studien oder bewusst gewählten Szenarien stammen. Die Herkunft der Bandbreite wird genannt.

## 16.3 Sensitivitätsanalyse

Der Nutzer kann sehen, welche Annahmen das Ergebnis treiben. Für wichtige Parameter zeigt ein Tornado-Diagramm die Ergebnisänderung bei niedriger und hoher Annahme.

## 16.4 Monte-Carlo-Simulation

Später können unsichere Parameter aus dokumentierten Verteilungen gezogen werden. Ergebnisse werden als Quantile dargestellt. Korrelationen zwischen Parametern müssen berücksichtigt werden, damit Unsicherheit nicht künstlich über- oder unterschätzt wird.

## 16.5 Vorsicht bei Multiplikationsketten

Bei langen Wirkungsketten kann sich Unsicherheit stark vergrößern. Solche Ergebnisse erhalten eine auffällige Kennzeichnung und dürfen nicht als einzelne präzise Eurozahl in der Hauptansicht stehen.

## 16.6 Konfligierende Studien

Widersprechen sich seriöse Quellen, werden mehrere Modellvarianten angeboten. Die Dokumentation erklärt, warum die Ergebnisse auseinandergehen.

## 16.7 Werte außerhalb des validierten Modellbereichs

Eine Berechnung außerhalb des validierten Modellbereichs ist eine **Extrapolation** und ein eigener sichtbarer Grund für zusätzliche Unsicherheit. Sie wird direkt am Szenariowert und im Nachweis benannt. Ein Wert außerhalb des üblichen Sliderbereichs ist dagegen allein kein Unsicherheitsbeleg: Der Bedienbereich und der fachlich validierte Bereich beantworten unterschiedliche Fragen.

Die allgemeine Belastbarkeit eines Moduls bleibt von der zusätzlichen Unsicherheit eines konkreten Extremwerts unterscheidbar. Ein Modul kann schon für seine Baseline nur eine niedrige Belastbarkeit haben; ein weit außerhalb des validierten Bereichs liegender Szenariowert bringt zusätzlich die Unsicherheit der Extrapolation mit sich. Die Anwendung muss beide Hinweise verständlich einordnen und darf einen Wert nicht allein wegen seiner Größe als ungültig behandeln.

Außerhalb des validierten Bereichs werden Ergebnisse nicht als scheinexakte Prognose dargestellt. Eine Szenariozahl darf mit klarer Kennzeichnung und den bekannten Grenzen gezeigt werden, sofern die Berechnung sinnvoll bleibt. Wenn die Modellannahmen keine belastbare Quantifizierung mehr erlauben, wird ein fachlicher Status wie **„nicht seriös quantifizierbar“** ausgegeben statt einer erfundenen Punktzahl. Eine fehlende Bandbreite oder ein solcher Status wird begründet.

## Verwandte Kapitel

- [Modellstufe und Zeithorizont](modellstufe-und-zeithorizont.md)
- [Wirkungsmodell](wirkungsmodell.md)
- [Evidenzdatenbank und Quellenprovenienz](../06-evidenz/evidenzdatenbank.md)
- [Berechnungstransparenz im Produkt](../06-evidenz/berechnungstransparenz.md)
