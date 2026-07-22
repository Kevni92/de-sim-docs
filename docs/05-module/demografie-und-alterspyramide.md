---
title: Demografie und Alterspyramide
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.3
last_updated: 2026-07-13
---

# 12. Demografie und Alterspyramide

## 12.1 Kohorten-Komponenten-Modell

Die Bevölkerung wird nach Alter, Geschlecht und Region fortgeschrieben. Grundkomponenten sind:

- Geburten,
- Sterbefälle,
- Zuzüge,
- Fortzüge,
- Übergang jedes Jahrgangs in das nächste Alter.

## 12.2 Baseline

Die amtliche Bevölkerungsvorausberechnung dient als Referenz. Destatis arbeitet bewusst mit Varianten und bezeichnet diese als Wenn-Dann-Szenarien, nicht als Vorhersagen. Dieses Prinzip wird übernommen.

## 12.3 Alterspyramide

Die interaktive Grafik zeigt:

- Baseline und Reformszenario,
- Jahr 2026 bis mindestens 2070,
- Kinder und Jugendliche,
- Erwerbsalter,
- Rentenalter,
- Alten- und Jugendquotient,
- Bundesländer,
- Unsicherheitsband.

## 12.4 Implementierter Rechenvertrag

Die Anwendung speichert für jeden Lauf Datenjahr, Rechtsjahr, Modellversion, Baseline, Szenario und ein Unsicherheitsband. Intern werden Einzelalter bis zur Gruppe `100+` fortgeschrieben; die Standardansicht bündelt sie in verständliche Altersgruppen. Für jedes Jahr bleiben Geburten, Sterbefälle, Zuzüge, Fortzüge und Wanderungssaldo getrennt prüfbar.

Die Projektion ist eine aggregierte Kohortenfortschreibung. Sie schreibt keine individuellen Lebensläufe fort und kalibriert keine politische Wirkung automatisch aus einer beobachteten Korrelation.

## 12.5 Politische Einflüsse

Maßnahmen können über folgende Wege in das Demografiemodul gelangen:

- Familiengründung und gewünschte Kinderzahl,
- Lebenserwartung und Mortalität,
- Zu- und Abwanderung,
- regionale Binnenwanderung.

Direkte Eingriffe in diese Parameter werden nur als explizite Szenarioannahme zugelassen. Beispielsweise führt „mehr Kita-Geld“ nicht automatisch zu einer fest definierten zusätzlichen Geburtenzahl.

## 12.6 Zeitverzögerung

Demografische Effekte auf Arbeitsmarkt, Schulen, Rente und Pflege treten zu unterschiedlichen Zeitpunkten auf. Die Oberfläche zeigt deshalb, wann ein Effekt erstmals sichtbar wird und wann er sein größtes Gewicht erreicht.

## Verwandte Langfristkapitel

- [Migration, Schutzstatus und Arbeitsmarktzugang](migration-schutzstatus-und-arbeitsmarktzugang.md)
- [Erwerbspotenzial und Arbeitsvolumen](erwerbspotenzial-und-arbeitsvolumen.md)
- [Alterssicherung und vereinfachte Rentenindikatoren](alterssicherung-und-rentenindikatoren.md)

## Verwandte Kapitel

- [Synthetische Bevölkerung und Haushalte](../03-daten/synthetische-bevoelkerung.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
- [Kita, Familie und Bildung](kita-familie-und-bildung.md)
