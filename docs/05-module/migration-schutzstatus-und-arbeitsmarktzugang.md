---
title: Migration, Schutzstatus und Arbeitsmarktzugang
summary: Getrennte Modellierung von Zuzug, Schutzstatus, Erwerbsberechtigung und Beschäftigung.
status: Implementiert 1.0
last_updated: 2026-07-22
---

# Migration, Schutzstatus und Arbeitsmarktzugang

Die Langfristmodelle behandeln Migration als demografischen und rechtlichen Übergangspfad. Allgemeine Migration, Flucht- und asylbezogene Zuwanderung sowie tatsächliche Beschäftigung werden nicht zu einer Personenkennzahl zusammengezogen.

## Übergangskette

Für jede Projektion werden mindestens diese Stufen getrennt geführt:

1. Zuzüge nach Jahr und grobem Altersprofil,
2. Personen im Erwerbsalter,
3. rechtliche Erwerbsberechtigung,
4. Erwerbsbeteiligung,
5. Beschäftigung,
6. Arbeitszeit und Vollzeitäquivalente,
7. steuerpflichtige Lohnsumme und Sozialbeiträge.

Eine Erwerbsberechtigung ist daher weder eine Beschäftigung noch eine Einnahme. Beiträge entstehen erst aus beitragspflichtiger Beschäftigung und Arbeitsvolumen.

## Schutzstatus und Rechtsstand

Das Szenario speichert ein Datenjahr und ein Rechtsjahr. Als Rechtsquellen werden insbesondere [Asylgesetz § 61](https://www.gesetze-im-internet.de/asylvfg_1992/__61.html) und [Aufenthaltsgesetz § 4a](https://www.gesetze-im-internet.de/aufenthg_2004/__4a.html) geführt. Die konkrete Anwendung kann Warte- und Zugangszeiten als Szenarioannahme abbilden; ein früherer Zugang ist dabei ausdrücklich eine alternative Annahme und keine Aussage über das geltende Recht.

Die Rechtslage muss vor einer Veröffentlichung erneut geprüft werden. Ein Gesetzeslink ersetzt nicht die Speicherung des für den Lauf verwendeten Rechtsstands.

## Modellierung und Grenzen

- Allgemeine Migration und schutz-/asylbezogene Zuwanderung werden im Altersprofil getrennt behandelt.
- Zuzüge, Fortzüge und Wanderungssaldo bleiben als eigene Größen sichtbar.
- Schutzstatus, Verfahren, Erwerbsberechtigung und Qualifizierung werden nicht als Wertung einer Person interpretiert.
- Arbeitsnachfrage, Berufswechsel, Anerkennung einzelner Qualifikationen und regionale Verteilung werden nicht vollständig modelliert.
- Direkte Transfer- oder Verwaltungsausgaben stehen zeitlich getrennt neben später möglichen Steuern und Beiträgen.

Das Ergebnis ist ein Wenn-Dann-Szenario: „Unter diesen Zugang-, Beteiligungs- und Beschäftigungsannahmen entsteht dieser Pfad.“ Es ist keine individuelle Prognose und keine politische Empfehlung.

## Nutzeransicht

Die Standardansicht zeigt höchstens Erwerbspotenzial, Beschäftigte, Vollzeitäquivalente und Beitragswirkung. Detailansichten machen die Übergangsstufen, Unsicherheitsband, Datenjahr, Rechtsjahr und Quellen zugänglich. Sprache wie „Kosten eines Menschen“ oder pauschale Aussagen über Migration und Rentenfinanzierung wird nicht verwendet.

## Quellen und Übertragbarkeit

- [Bundesagentur für Arbeit: Migration und Arbeitsmarkt](https://statistik.arbeitsagentur.de/DE/Navigation/Statistiken/Interaktive-Statistiken/Migration-und-Arbeitsmarkt/Migration-und-Arbeitsmarkt-Nav.html) – Arbeitsmarktstatistik; nicht ohne Prüfung auf das gesamte Zuwanderungsprofil übertragbar.
- [Bundesagentur für Arbeit: Arbeitsmarktzulassung](https://www.arbeitsagentur.de/datei/das-beschaeftigungsrechtliche-anerkennungsverfahren_ba015000.pdf) – rechtliche und verfahrensbezogene Einordnung; Gültigkeit hängt vom Rechtsstand ab.
- [BAMF: Asylgeschäftsstatistik](https://www.bamf.de/SharedDocs/Anlagen/DE/Statistik/Asylgeschaeftsstatistik/asylgeschaeftsstatistik-gesamt-jahresbericht.html) – Verfahren und Schutzstatus; keine Beschäftigungsstatistik.
- [Destatis: Bevölkerungsvorausberechnungen](https://www.destatis.de/DE/Themen/Gesellschaft-Umwelt/Bevoelkerung/Bevoelkerungsvorausberechnung/_inhalt.html) – Referenz für Bevölkerung, Wanderungen und Altersstruktur.

## Verwandte Kapitel

- [Demografie und Alterspyramide](demografie-und-alterspyramide.md)
- [Erwerbspotenzial und Arbeitsvolumen](erwerbspotenzial-und-arbeitsvolumen.md)
- [Alterssicherung und vereinfachte Rentenindikatoren](alterssicherung-und-rentenindikatoren.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
