---
title: Informationsarchitektur und progressive Offenlegung
summary: Verbindlicher UI-Vertrag für verständliche Reformparameter, direkte Ergebnisse, Betroffenheit, Folgewirkungen, Modellbasis und Nachweise.
status: Arbeitsstand 0.2
last_updated: 2026-07-14
---

# Informationsarchitektur und progressive Offenlegung

Die fachliche Tiefe des Deutschland-Simulators bleibt vollständig erhalten. Sie wird jedoch nicht als Voraussetzung für die normale Bedienung dargestellt. Die Oberfläche folgt deshalb drei aufeinander aufbauenden Ebenen.

## Drei Bedienebenen

### 1. Entscheiden

Nutzende wählen eine Maßnahme und verändern die wichtigste politische oder finanzielle Stellschraube. Die direkte staatliche Wirkung wird ohne manuellen Start einer technischen Rechenebene aktualisiert.

### 2. Ergebnis verstehen

Die Standardansicht beantwortet in fester Reihenfolge:

1. Was wird geändert?
2. Was ist die direkte staatliche Wirkung?
3. Wer ist hauptsächlich betroffen?
4. Wie belastbar ist das Ergebnis?

Mögliche Verhaltensreaktionen, indirekte Wirkungen und langfristige Pfade werden nicht mit der direkten Wirkung zu einer scheinexakten Gesamtsumme vermischt.

### 3. Nachvollziehen und prüfen

Bei Bedarf bleiben vollständig erreichbar:

- weitere Parameter und Annahmen,
- Betroffenheits- und Inzidenzannahmen,
- mögliche Folgewirkungen und der zentrale Berechnungsrahmen,
- Finanzierung und Teilkomponenten,
- Quellen, Formeln, Daten- und Rechtsstand,
- Unsicherheitsannahmen und bekannte Grenzen,
- synthetische Modellbasis, Kalibrierung und technische Laufreferenzen.

## Gemeinsamer Reform- und Ergebnisvertrag

Einnahmen- und Ausgabenmodule verwenden denselben fachlichen Aufbau. Der erste Ergebnisbereich enthält höchstens vier Kerninformationen:

- Ausgangswert oder Baseline,
- direkte staatliche Mehr- oder Minderwirkung,
- hauptsächlich betroffene Personen, Haushalte oder wirtschaftliche Wirkungsträger,
- Belastbarkeit mit verständlichem Unsicherheitshinweis.

Technische Kennungen, Seeds, Modellversionen und interne Quellen-IDs gehören nicht in diese Standardansicht.

Unterhalb der Kerninformationen folgen getrennte Vertiefungen:

- **Wer ist betroffen?**
- **Mögliche Folgewirkungen**
- **Finanzierung und Teilkomponenten**
- **Berechnung und Quellen**
- **Erweiterte Parameter**

Die Reihenfolge ist auf Desktop und Mobil identisch. Vertiefungen sind per Tastatur erreichbar und dürfen keine horizontale Pflichtnavigation voraussetzen.

## Modellbasis als Infrastruktur

Die synthetische Bevölkerung ist notwendige Recheninfrastruktur, aber keine verpflichtende Standardaufgabe. Einkommensteuer- und Leistungsberechnungen fordern deshalb automatisch eine stabile, versionierte Standardbasis an.

In normalen Reformansichten erscheint nur ein kompakter fachlicher Status:

- wird vorbereitet,
- bereit,
- bereit mit Qualitätswarnung,
- ursprüngliche Referenz fehlt,
- konnte nicht geladen werden.

Seed, Stichprobengröße, Lauf-ID und Modellversion liegen in der erweiterten Prüfebene **Modellbasis und Bevölkerung**. Dort können Fachnutzende Verteilungen, Kalibrierung, Quellen und gespeicherte Läufe prüfen oder bewusst eine andere Modellbasis erzeugen und aktivieren.

Ein Szenario mit fehlender Laufreferenz wird nicht still auf einen verfügbaren Lauf umgestellt. Die Oberfläche unterscheidet:

1. **Identische Rekonstruktion:** nur bei vollständigen, kompatiblen Generationsparametern.
2. **Bewusster Wechsel zur Standardbasis:** mit vorherigem Hinweis, dass sich Ergebnisse verändern können.

Damit bleibt Reproduzierbarkeit erhalten, ohne Seed- und Laufverwaltung in den normalen Reformablauf zu verlagern.

## Zustände

Der gemeinsame Vertrag gilt auch dann, wenn kein reguläres Ergebnis vorliegt:

- **Laden:** stabile Platzhalter ohne irreführenden Zwischenwert,
- **Leer:** verständliche Erklärung der fehlenden Berechnungsgrundlage,
- **Fehler:** Ursache und mögliche Wiederholung in Alltagssprache,
- **Nicht berechenbar:** fachlicher Status statt erfundener Zahl,
- **Bereit:** Stellschraube und höchstens vier Kerninformationen.

„Nicht seriös quantifizierbar“ ist ein gültiges Ergebnis. Es darf nicht still durch einen Schätzwert ersetzt werden.

## Direkte und mögliche Folgewirkung

Die direkte Wirkung beschreibt zunächst den rechnerischen Effekt bei unveränderter Bemessungsgrundlage beziehungsweise ohne zusätzliche Folgeannahme. Verhaltensreaktionen werden separat ausgewiesen. Ein ausgewählter Modellpfad verändert daher nicht rückwirkend die Darstellung der direkten Wirkung.

## Referenz: Umsatzsteuer

Die Umsatzsteuer dient als erste Referenzimplementierung des Reform- und Ergebnisvertrags:

- Der Regelsteuersatz ist die primäre Stellschraube.
- Ausgangswert, direkte Aufkommenswirkung, hauptsächlich betroffene Wirkungsträger und Belastbarkeit bilden den ersten Ergebnisbereich.
- Ermäßigter Satz, Anteil ermäßigter Umsätze und Preisweitergabe liegen unter **Erweiterte Parameter**.
- Die Inzidenzannahme liegt unter **Wer ist betroffen?**.
- Die Verhaltenskomponente liegt unter **Mögliche Folgewirkungen**; Modellstufe und Zeithorizont werden dort nur angezeigt und zentral im Szenario geändert.
- Vollständige Quellen und Rechenwege bleiben über **Berechnung und Quellen** erreichbar.

## Verwandte Kapitel

- [Zielbild und Grundsätze](vision-und-grundsaetze.md)
- [Synthetische Bevölkerung und Modellbasis](../03-daten/synthetische-bevoelkerung.md)
- [Weitere Einnahmemodule](../02-fiskal/weitere-einnahmemodule.md)
- [Modellstufe und Zeithorizont](../04-modell/modellstufe-und-zeithorizont.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
