---
title: Szenario- und Zustandsmodell
summary: Interner Einstiegspunkt für zentralen Szenariozustand, Historie, Persistenz und Serverabstraktion.
status: Intern 0.7
last_updated: 2026-10-21
---

# Szenario- und Zustandsmodell

> Diese Seite ist eine interne Entwicklungsunterlage und durch `exclude_docs` von der öffentlichen Website ausgeschlossen.

Der zentrale `ScenarioDraft` ist die einzige veränderbare fachliche Quelle für Einkommensteuer-, Einnahmen- und Ausgabenparameter. UI-Seiten erhalten Zustand und Callbacks aus `App.tsx`; sie speichern nicht selbst in IndexedDB.

## Kernelemente

- `revenueChanges` enthält Parameter und materialisierte Ergebnisse der Einnahmenmodule.
- `expenseChanges` enthält Parameter und materialisierte Ergebnisse der Ausgabenmodule.
- `incomeTax` enthält den strukturierten Einkommensteuertarif.
- `modelLevel` steuert statische, verhaltensbasierte oder langfristige Wirkungen.
- `modelVersion` und `sourceIds` sichern Provenienz und Migration.
- der History-Reducer stellt Undo und Redo bereit.
- der lokale Worker kapselt Entwurf, Szenarien, Quellen und Metriken in IndexedDB.

## Persistenzfluss

```text
UI-Eingabe
  -> ScenarioDraft
  -> normalisierter History-Reducer
  -> materialisiertes Szenario
  -> LocalServerClient
  -> Web Worker
  -> IndexedDB
```

## Gemeinsame Haushaltsübersicht

Übersicht und Szenariovergleich verwenden dieselbe Zusammenfassung der dargestellten Einnahme- und Ausgabenposten. Sie übernimmt die Ergebnisse des aktuellen Szenarios und weist Baseline, Veränderung und Saldo aus denselben Zeilen aus. Ein fehlendes Modul darf nicht durch seinen Baselinewert oder null ersetzt werden; in diesem Fall bleiben Gesamtergebnis und Vergleich sichtbar unvollständig.

Die Wirkungsebenen des Wirkungs-Workers bleiben davon getrennt. Nur ein Lauf mit aktueller Eingabesignatur darf als aktuelle modellierte Reaktion erscheinen. Direkte Modulergebnisse und zusätzliche Wirkungspfade werden nicht zu einer neuen Gesamtformel addiert.

Der Clientvertrag bleibt bewusst serverähnlich. Ein späteres Backend soll dieselben Operationen anbieten, ohne dass Seiten oder Fachmodule direkten Datenbankzugriff erhalten.

## Änderungsübersicht und Einzelreset

Die nutzerseitige Ansicht **Deine Änderungen** wird aus den jeweils aktiven Szenariowerten gegenüber den versionierten Ausgangswerten gebildet. Sie führt nur abweichende konkrete Werte auf und ordnet sie politischen Stellschrauben, Modell- und Wirkungsannahmen oder dem Berechnungsrahmen zu. Gruppierte Bedienelemente wie Regelbedarfe oder Mehrbedarfe erscheinen als einzelne geänderte Parameter; ein zweiter Gruppenwert würde dieselbe Maßnahme doppelt zählen.

Jeder Eintrag enthält den Ausgangswert, den aktuellen Wert, die Einheit, den passenden Modulzugang und einen Einzelreset. Der Reset setzt ausschließlich den ausgewählten Wert auf seine zugehörige Baseline zurück. Andere Parameter im selben Fachpaket bleiben erhalten. Umsatzsteuer-Sätze werden von Anteil ermäßigter Umsätze und Preisweitergabe getrennt ausgewiesen. Bevölkerungslauf und Profilmerkmale sind keine politischen Reformänderungen.

Die Ansicht ist keine zusätzlich gespeicherte Szenariofassung. Import, Undo, Redo und Wiederherstellung des Browserentwurfs müssen dieselbe Änderungsübersicht aus dem jeweils aktuellen Szenariozustand ergeben. Ergebnisse und Wirkungsannahmen werden nicht als unabhängige Einzelwirkungen zu einer neuen Gesamtsumme addiert.

## Gespeicherte Szenarien vergleichen

Der Szenariovergleich stellt die gesetzliche Ausgangslage, den aktuellen Arbeitsentwurf und eine ausdrücklich ausgewählte gespeicherte Fassung gegenüber. Die feste Beispielspalte ist kein Szenario und liefert daher keine Vergleichszahlen. Ist noch keine gespeicherte Fassung vorhanden, zeigt die Ansicht einen Leerzustand mit Zugang zur Szenarioverwaltung.

Jede Szenariospalte wird aus ihren eigenen gespeicherten Parametern berechnet. Auswahl und Berechnung ändern weder den Arbeitsentwurf noch eine gespeicherte Fassung. Eine Auswahl wird nicht als Änderung am Szenario persistiert. Fehlt eine für ein Ergebnis benötigte Referenz, wird dieses Ergebnis als nicht verfügbar erläutert; es wird kein ersatzweiser Bevölkerungslauf stillschweigend aktiviert.

Vor dem Vergleich werden Rechtsstand, Datenbezug, Modellstufe, Zeithorizont, Bevölkerungslauf sowie versionierte Fachmodelle geprüft. Abweichungen werden konkret benannt. Die jeweiligen Szenarioergebnisse dürfen einzeln sichtbar bleiben, aber ein Unterschied wird nicht als gleichgrundiger Vergleich ausgegeben. Unvollständige Summen bleiben unvollständig. Fehlende oder veraltete Wirkungsrechnungen werden getrennt vom direkten Budgeteffekt gekennzeichnet.

Die Maßnahmenübersicht führt die gegenüber ihrer Baseline geänderten konkreten Werte beider Szenarien zusammen. Sie kann optional auf Werte begrenzt werden, die sich zwischen Entwurf und gespeicherter Alternative unterscheiden. Gleiche Werte werden nicht doppelt gezählt und die Auswahl der gespeicherten Alternative verändert keine Parametereingabe.

## Arbeitsentwurf und gespeicherte Szenariofassung

Nutzer arbeiten zunächst an einem automatisch gesicherten Entwurf in diesem Browser. Eine gespeicherte Szenariofassung entsteht erst über die ausdrückliche Aktion „Szenario speichern“. Die Oberfläche unterscheidet beide Zustände: Sie zeigt den Zeitpunkt der letzten bestätigten Entwurfssicherung und meldet Änderungen gegenüber der zuletzt gespeicherten Fassung.

„Änderungen speichern“ aktualisiert die aktive gespeicherte Fassung. „Als neue Variante sichern“ legt eine separate Fassung an; die bisher gespeicherte Variante bleibt erhalten. Nach einem Reload stellt die Anwendung den Browser-Entwurf samt Bezug zur aktiven gespeicherten Fassung wieder her und zeigt, ob beide noch übereinstimmen. Ein Speicherfehler wird nicht als Erfolg dargestellt; der Entwurf bleibt im geöffneten Formular und kann erneut gesichert werden.

Der Entwurf liegt nur auf diesem Gerät in diesem Browser. Es gibt weder ein Konto noch eine Synchronisierung zwischen Geräten.

## Entwurf vor Verwerfen oder Laden absichern

Wenn ein Arbeitsentwurf gegenüber seiner gespeicherten Fassung geändert wurde, fragt die Anwendung vor „Neu“, dem Laden einer anderen Fassung oder einem gültigen Import, wie weiter verfahren werden soll. „Als Variante sichern und fortfahren“ legt zuerst eine eigenständige gespeicherte Fassung an; der bisherige gespeicherte Stand bleibt erhalten. „Entwurf verwerfen und fortfahren“ übernimmt den gewünschten Wechsel ohne die aktuellen Änderungen. „Abbrechen“ schließt die Auswahl und lässt den Entwurf unverändert. Ein unberührter neuer Entwurf kann ohne wiederholte Warnung gewechselt werden.

Ein Import wird erst nach erfolgreicher Prüfung der Datei als möglicher Wechsel angeboten. Eine ungültige Datei verändert weder den Entwurf noch die gespeicherte Auswahl. Schlägt das Sichern als Variante fehl, bleibt die Auswahl geöffnet, die Eingaben bleiben erhalten und der Wechsel wird nicht ausgeführt; ein erneuter Versuch ist möglich.

Vor dem Löschen einer gespeicherten Fassung nennt die Bestätigung deren Namen. Abbrechen erhält die Fassung. Wird die aktive gespeicherte Fassung gelöscht, bleibt der aktuelle Arbeitsentwurf im Browser erhalten und wird von dieser gelöschten Fassung getrennt.

## Verwandte Kapitel

- [Technische Architektur](technische-architektur.md)
- [Modulvertrag](modulvertrag.md)
- [Ausgabenmodule-Modellvertrag](ausgabenmodule-modellvertrag.md)
