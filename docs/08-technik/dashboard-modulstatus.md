# Statuskennzeichnung der Dashboardmodule

## Zweck

Die Listen **Einnahmen** und **Ausgaben** unterscheiden sichtbar zwischen geänderten Szenariowerten, belastbaren beziehungsweise unsicheren Berechnungen und noch nicht implementierten Detailmodulen.

## Geänderte Szenariowerte

Implementierte Haushaltsposten behalten unabhängig von einer Abweichung zur Baseline denselben neutralen Zeilenhintergrund. Eine Änderung wird ausschließlich über den angezeigten Differenzwert und dessen positive beziehungsweise negative Textfarbe kenntlich gemacht.

Dadurch entsteht in den Dashboardlisten kein scheinbarer Aktiv- oder Auswahlzustand. Eine farbige Flächenmarkierung bleibt tatsächlichen Auswahlzuständen in Navigation und Detailansichten vorbehalten.

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
3. eine geänderte implementierte Position verwendet denselben neutralen Hintergrund wie eine unveränderte Position,
4. eine nicht implementierte Ausgabenposition verwendet denselben deaktivierten Zustand,
5. der Desktop-Zustand wird als Browser-Screenshot gesichert.
