---
title: Gesundheit, Krankheitstage und Bürokratie
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.3
last_updated: 2026-07-13
---

# 11. Gesundheit, Krankheitstage und Bürokratie

## 11.1 Krankheitstage als Ergebnisgröße

Der Simulator führt mindestens:

- Arbeitsunfähigkeitstage je Beschäftigten,
- Produktionsausfall,
- Ausfall an Bruttowertschöpfung,
- Lohnfortzahlung,
- Krankengeld,
- Ausfall nach Diagnose- und Altersgruppen,
- Unsicherheit durch Erfassungsänderungen.

Die BAuA schätzt für 2024 bei durchschnittlich 20,8 Arbeitsunfähigkeitstagen je arbeitnehmender Person 881,5 Millionen AU-Tage, Produktionsausfälle von 134 Milliarden Euro und einen Ausfall an Bruttowertschöpfung von 227 Milliarden Euro. Diese Werte sind ein Baseline-Anker, keine universelle Umrechnungsformel für jede Reform.

## 11.2 Gesundheitspolitische Wirkungsketten

Beispiele:

`Prävention → Teilnahme → Risikofaktoren → Erkrankungswahrscheinlichkeit → Krankheitstage → Gesundheitskosten und Arbeitsausfall`

`mehr Pflegepersonal → Belastung und Versorgungsqualität → Komplikationen und Wiederaufnahmen → Kosten und Gesundheit`

Jeder Übergang benötigt eine eigene Evidenzbewertung.

## 11.3 Elektronische Arbeitsunfähigkeitsbescheinigung

Bei einer Abschaffung oder Änderung der eAU werden getrennt betrachtet:

- Papier-, Porto- und Übermittlungsaufwand,
- Zeitaufwand in Praxen, Krankenkassen und Unternehmen,
- Fehler- und Medienbruchrisiken,
- Vollständigkeit der Statistik,
- technische Betriebskosten,
- mögliche Übergangskosten.

Die eAU verbessert nach Angaben des GKV-Spitzenverbands Übermittlung, Dokumentation und Medienbruchfreiheit. Gleichzeitig hat die vollständigere Erfassung den beobachteten Krankenstand statistisch verändert. Das Modell darf eine höhere Zahl gemeldeter Fälle daher nicht automatisch als reale Verschlechterung der Gesundheit interpretieren.

## 11.4 Bürokratiekosten

Bürokratie wird in natürlichen Einheiten modelliert:

- Minuten je Vorgang,
- Anzahl Vorgänge,
- Personalkosten,
- Sachkosten,
- Warte- und Durchlaufzeit,
- Fehlerquote,
- einmaliger Umstellungsaufwand.

Erst danach erfolgt eine monetäre Zusammenfassung.

## 11.5 Grenzen

Eine Regeländerung wie die Pflicht zur Bescheinigung ab dem ersten Krankheitstag kann Verhalten, Arztkontakte, Erfassung und tatsächliche Abwesenheit unterschiedlich beeinflussen. Diese Effekte werden nicht zu einer scheinbar sicheren Zahl zusammengezogen.

## Verwandte Kapitel

- [Indirekte und nicht monetäre Wirkungen](../04-modell/indirekte-und-nichtmonetaere-wirkungen.md)
- [Evidenzdatenbank und Quellenprovenienz](../06-evidenz/evidenzdatenbank.md)
- [Technische Architektur](../08-technik/technische-architektur.md)
