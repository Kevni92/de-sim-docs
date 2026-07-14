---
title: Modellstufe und Zeithorizont
summary: Zentrale Szenarioentscheidung für direkte Wirkung, kurzfristige Reaktionen und langfristige Pfade.
status: Arbeitsstand 0.1
last_updated: 2026-07-14
---

# Modellstufe und Zeithorizont

Modellstufe und Zeithorizont gelten für das gesamte Szenario. Sie werden genau einmal in der Szenarioverwaltung gewählt. Einnahmen-, Ausgaben-, Leistungs- und Wirkungsansichten zeigen die Einstellung anschließend nur noch an und führen keine unabhängigen lokalen Varianten.

## Sichtbare Begriffe

Die internen Werte bleiben für bestehende Szenarien und Exporte erhalten. In der Oberfläche werden verständliche Begriffe verwendet:

| Interner Wert | Sichtbare Bezeichnung | Bedeutung |
| --- | --- | --- |
| `statisch` | **Nur direkte Wirkung** | unmittelbare finanzielle Erstwirkung ohne Verhaltensreaktion |
| `verhalten` | **Mit kurzfristigen Reaktionen** | dokumentierte kurzfristige Verhaltensanpassung und begrenzte Folgewirkungen |
| `langfrist` | **Langfristiges Szenario** | zusätzliche Zeitpfade und langfristige Modellannahmen mit höherer Unsicherheit |

Ein langfristiges Szenario ist keine sichere Prognose. Es beschreibt einen möglichen Pfad unter den gewählten Annahmen und muss zusammen mit Unsicherheit und Modellgrenzen gelesen werden.

## Zeithorizont

Der Zeithorizont wird zentral als 1, 5, 10 oder 20 Jahre gewählt. Er ordnet Ergebnisse zeitlich ein. Die Auswahl eines längeren Zeitraums erzeugt nicht automatisch eine langfristige Wirkung, wenn die gewählte Modellstufe oder die fachliche Evidenz diese Wirkung nicht unterstützt.

## Bedienung

1. Nutzende öffnen **Szenario verwalten**.
2. Im Abschnitt **Berechnungsrahmen** wählen sie Modellstufe und Zeithorizont.
3. Fachseiten zeigen anschließend beispielsweise **Berechnet: Nur direkte Wirkung** und **Zeitraum: 10 Jahre**.
4. Die Aktion **Im Szenario ändern** führt direkt zurück zur zentralen Einstellung.

Die Fachseite besitzt keine zweite Modellstufen- oder Zeitraumsteuerung. Dadurch bleibt eindeutig, welche Einstellung für das gesamte Szenario gilt.

## Aktualität von Ergebnissen

Abhängige Ergebnisse verwenden drei verständliche Zustände:

- **Aktuell:** Ergebnis entspricht Modellstufe und Zeitraum des Szenarios.
- **Aktualisierung läuft:** Eine neue Rechnung wird erstellt. Direkte oder ältere Ergebnisse dürfen zur Orientierung sichtbar bleiben, werden aber nicht als neuer Stand ausgegeben.
- **Verwendet ältere Einstellung:** Das sichtbare Ergebnis stammt noch aus einem anderen Berechnungsrahmen und ist entsprechend gekennzeichnet.

Die Wirkungsrechnung wird nach einer Änderung automatisch aktualisiert. Eine separate Aktion **Neu berechnen** ist im normalen Ablauf nicht erforderlich. Bei einem technischen Fehler bleibt eine gezielte Wiederholung möglich.

## Trennung der Wirkungsebenen

Die Modellstufe verändert nicht rückwirkend die Bedeutung der direkten Wirkung:

- direkte finanzielle Erstwirkung bleibt separat sichtbar,
- kurzfristige Reaktionen werden als eigener Modellpfad ausgewiesen,
- langfristige Pfade erhalten einen eigenen Zeitraum, Unsicherheitsstatus und Prognosehinweis,
- nicht ausreichend belegte Wirkungen bleiben ohne scheinpräzisen Punktwert.

## Szenarien und Kompatibilität

Modellstufe und Zeithorizont sind Bestandteil von Speicherung, Import, Export, Duplizieren, Undo und Redo. Bestehende Szenarien behalten ihre internen Werte; die neue Oberfläche übersetzt sie lediglich in die verbindlichen Nutzerbegriffe.

## Verwandte Kapitel

- [Informationsarchitektur und progressive Offenlegung](../01-produkt/informationsarchitektur-und-progressive-offenlegung.md)
- [Indirekte und langfristige Wirkungen](indirekte-und-langfristige-wirkungen.md)
- [Unsicherheit und Szenarien](unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
