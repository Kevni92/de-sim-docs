# Statuskennzeichnung der Dashboardmodule

## Zweck

Die Listen **Einnahmen** und **Ausgaben** unterscheiden sichtbar zwischen geänderten Szenariowerten, belastbaren beziehungsweise unsicheren Berechnungen und noch nicht implementierten Detailmodulen.

## Geänderte Szenariowerte

Eine türkis hinterlegte Zeile kennzeichnet einen gegenüber der Baseline veränderten Wert. Maßgeblich ist eine von null abweichende Differenz des jeweiligen Einnahmen- oder Ausgabenpostens. Die Farbe ist kein Hinweis auf den Implementierungsstand.

## Nicht implementierte Detailmodule

Ein Haushaltsposten gilt im Dashboard als nicht implementiert, wenn für die Zeile keine Navigation zu einem Detailmodul vorhanden ist. Solche Zeilen verwenden:

- einen diagonal gestreiften Hintergrund,
- eine aufgehellte Schrift- und Iconfarbe,
- einen deaktivierten Hauptbutton ohne Hover-Zustand.

Die Quellenaktion bleibt separat verfügbar, sofern für den Haushaltsposten ein Nachweis hinterlegt ist.

## Unsicherheit und Punktindikator

Die drei Punkte zeigen die zusammengefasste Belastbarkeit einer Kennzahl:

- drei aktive Punkte: hohe Belastbarkeit,
- zwei aktive Punkte: mittlere Belastbarkeit,
- ein aktiver Punkt: niedrige Belastbarkeit.

Der Indikator fasst Datenbasis, Methode und bekannte Unsicherheit zusammen. Er bewertet weder die politische Qualität einer Maßnahme noch die gesellschaftliche Erwünschtheit eines Ergebnisses.

Niedrige Konfidenz wird ausschließlich über diesen Indikator dargestellt. Der gestreifte Hintergrund dient im Dashboard ausschließlich dem fehlenden Implementierungsstand, damit hypothetische, aber bereits umgesetzte Module wie die Vermögensteuer nicht fälschlich deaktiviert wirken.

## Tooltip-Vorschauen

Quellenbuttons mit Text und reine Icon-Buttons zeigen bei Hover sowie Tastaturfokus eine kompakte Evidenzvorschau. Sie enthält nur die zunächst entscheidungsrelevanten Angaben:

- Evidenzstatus der Kennzahl,
- Konfidenz,
- Daten- und Rechtsstand,
- institutionelle Grundlage,
- Unsicherheitsbeschreibung,
- wichtigste bekannte Grenze.

Ein Klick öffnet weiterhin den vollständigen Nachweis-Drawer. Die Punktindikatoren zeigen im Tooltip zusätzlich die Bedeutung der Skala und die konkrete Anzahl aktiver Punkte.

Tooltips werden außerhalb überlaufbegrenzter Karten gerendert, bleiben innerhalb des Browserfensters und sind über `aria-describedby` mit dem fokussierten Auslöser verbunden. Escape schließt eine geöffnete Vorschau.

## Regressionsschutz

Der Playwright-Test muss mindestens prüfen:

1. eine nicht implementierte Einnahmenposition ist deaktiviert, gestreift und ohne Hover-Effekt,
2. eine implementierte Position mit niedriger Konfidenz bleibt bedienbar und erhält keinen Deaktivierungshintergrund,
3. eine nicht implementierte Ausgabenposition verwendet denselben Zustand,
4. Quellenbuttons zeigen bei Fokus die Evidenzvorschau mit Grundlage, Stand und Unsicherheit,
5. der Punktindikator erklärt die Skala von einem bis drei Punkten,
6. Desktop- und Mobilansicht bleiben tastaturbedienbar,
7. der Desktop-Zustand wird als Browser-Screenshot gesichert.
