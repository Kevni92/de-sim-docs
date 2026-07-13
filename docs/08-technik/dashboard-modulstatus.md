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

## Unsicherheit

Niedrige Konfidenz wird weiterhin über den dreistufigen Konfidenzindikator dargestellt. Der gestreifte Hintergrund dient im Dashboard ausschließlich dem fehlenden Implementierungsstand, damit hypothetische, aber bereits umgesetzte Module wie die Vermögensteuer nicht fälschlich deaktiviert wirken.

## Regressionsschutz

Der Playwright-Test muss mindestens prüfen:

1. eine nicht implementierte Einnahmenposition ist deaktiviert, gestreift und ohne Hover-Effekt,
2. eine implementierte Position mit niedriger Konfidenz bleibt bedienbar und erhält keinen Deaktivierungshintergrund,
3. eine nicht implementierte Ausgabenposition verwendet denselben Zustand,
4. der Desktop-Zustand wird als Browser-Screenshot gesichert.
