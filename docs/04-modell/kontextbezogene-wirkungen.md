---
title: Kontextbezogene Wirkungen in Reformmodulen
summary: Fachlicher Vertrag für die Zuordnung von Reformen zu möglichen Wirkungen, Überlappungsschutz und getrennten Szenariovergleich.
status: Arbeitsstand 0.1
last_updated: 2026-07-14
---

# Kontextbezogene Wirkungen in Reformmodulen

Mögliche Wirkungen werden dort gezeigt, wo eine konkrete Reform verändert wird. Die vertiefende Wirkungsansicht bleibt für Prüfung und Parameterzugriff erreichbar, bildet aber keine zweite unabhängige Simulation.

## Feste Trennung

Jede Reformansicht unterscheidet:

1. **direkte staatliche Wirkung** aus dem Steuer-, Einnahmen-, Ausgaben- oder Leistungsmodell,
2. **kurzfristige mögliche Reaktion** als getrennten Modellpfad,
3. **langfristigen Szenariopfad** mit Zeitraum und breiterer Unsicherheit,
4. **nicht monetäre Wirkung** in natürlicher Einheit,
5. **nicht ausreichend belegte Wirkung** ohne Punktwert.

Diese Ebenen werden nicht zu einer scheinpräzisen Gesamtwirkung addiert.

## Explizite Zuordnung

Die Verbindung erfolgt über stabile Modulkennungen und dokumentierte Wirkungsketten. Sichtbare Namen oder freie Textähnlichkeit entscheiden nicht über die Zuordnung.

Beispiele:

| Reformkontext | Gezeigter Pfad | Einordnung |
| --- | --- | --- |
| Umsatzsteuer | Steuersatz → Preise → reale Nachfrage → steuerpflichtiger Umsatz | gerichtete Wirkung ohne Punktwert |
| Kitas und Familienleistungen | Plätze und Qualität → Betreuung → Arbeitszeit und Einkommen | quantifizierter Modellpfad mit Bandbreite |
| Infrastruktur | Investitionsausgabe → Kapitalstock → Wertschöpfung und fiskalische Rückflüsse | langfristiger Szenariopfad |
| Gesundheit | Prävention und Versorgung → mögliche vermiedene Ausfalltage | natürliche Einheit und Modellpfad |
| Migration, Geburten und Altersausgaben | relevante Wirkungskette | bewusst nicht berechnet, wenn Kausalität oder Datenbasis fehlen |

## Doppelzählung

Jede Verbindung besitzt einen Überlappungsschlüssel. Ein übergeordneter Pfad wird als primär markiert. Abhängige Vertiefungen bleiben sichtbar, werden im Szenariovergleich aber nicht zusätzlich summiert. Der Arbeitsvolumenpfad innerhalb einer Kita-Wirkung ist beispielsweise keine zweite unabhängige Wirkung.

## Aktualität

Ein Ergebnis ist nur aktuell, wenn Modellbasis, Modellstufe, Zeithorizont und reformbezogene Eingaben übereinstimmen. Bei Änderungen erscheinen die Zustände:

- **Aktuell**,
- **Aktualisierung läuft**,
- **Verwendet ältere Einstellung**.

Alte Ergebnisse dürfen während der Aktualisierung sichtbar bleiben, werden aber nicht als neuer Stand ausgegeben.

## Szenariovergleich

Der Vergleich zeigt getrennte Zeilen für:

- direkte fiskalische Wirkung,
- kurzfristige mögliche Reaktionen,
- fiskalische Rückkopplungen,
- langfristige Szenariopfade,
- nicht monetäre Wirkungen,
- nur gerichtete Wirkungen,
- nicht ausreichend belegte Pfade.

Fehlt für ein Vergleichsszenario eine passende Wirkungsrechnung, steht dort **nicht berechnet** statt eines erfundenen Wertes.

## Persistenz und Nachweis

Der Szenarioexport enthält neben Wirkungsparametern eine Referenz auf den verwendeten Wirkungslauf: Modellversion, Bevölkerungslauf, Modellstufe, Zeitraum, Eingabesignatur und Berechnungszeitpunkt. Quellen, Annahmen, Kausalität, Unsicherheit und bekannte Grenzen bleiben über **Berechnung, Annahmen und Quellen** sowie die vertiefende Fachansicht erreichbar.

## Verwandte Kapitel

- [Modellstufe und Zeithorizont](modellstufe-und-zeithorizont.md)
- [Indirekte und langfristige Wirkungen](indirekte-und-langfristige-wirkungen.md)
- [Weitere Einnahmemodule](../02-fiskal/weitere-einnahmemodule.md)
- [Ausgabenmodule 2026](../02-fiskal/ausgabenmodule.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
