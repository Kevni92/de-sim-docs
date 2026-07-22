---
title: Erwerbspotenzial und Arbeitsvolumen
summary: Verbindliche Stufen von Erwerbsalter bis beitragspflichtiger Lohnsumme.
status: Implementiert 1.0
last_updated: 2026-07-22
---

# Erwerbspotenzial und Arbeitsvolumen

Die Projektion unterscheidet Personen im Erwerbsalter, Erwerbspotenzial, Erwerbspersonen, Beschäftigte, Vollzeitäquivalente und Beitragszahlende. Diese Begriffe sind nicht austauschbar.

## Verbindliche Begriffe

| Größe | Definition im vereinfachten Modell |
|---|---|
| Bevölkerung im Erwerbsalter | Personen zwischen unterer Altersgrenze und Rentenaltersgrenze. |
| Demografisches Erwerbspotenzial | Erwerbsalter nach einer altersbezogenen Beteiligungsstruktur, bevor Beschäftigung angenommen wird. |
| Erwerbspersonen | Personen, die unter der Beteiligungsannahme dem Arbeitsmarkt zur Verfügung stehen. |
| Beschäftigte | Erwerbspersonen nach Anwendung der Beschäftigungsquote; bei Migration nur Personen mit Erwerbsberechtigung. |
| Vollzeitäquivalente | Beschäftigte, gewichtet mit dem angenommenen Arbeitszeitfaktor. |
| Beitragszahlende | Im Basismodell Beschäftigte mit beitragspflichtigem Arbeitsvolumen; die Zahl ist keine reine Altersgruppen- oder Personenquote. |
| Beitragspflichtige Lohnsumme | Vollzeitäquivalente multipliziert mit dem versionierten durchschnittlichen Jahreslohn. |

## Rechenschritte

Für ein Jahr `t` gilt als fachliche Reihenfolge:

```text
Erwerbsalter → demografisches Potenzial → Erwerbspersonen
→ Beschäftigte → Vollzeitäquivalente → Beitragszahlende
→ beitragspflichtige Lohnsumme
```

Migration wird, sofern sie nicht schon im Bevölkerungsbestand enthalten ist, über den eigenen Zugangspfad ergänzt. Damit werden Personen nicht doppelt gezählt. Eine rechtliche Berechtigung wird nicht als Beschäftigung eingesetzt; ohne Beschäftigung entstehen weder Lohnsumme noch Erwerbstätigenbeiträge.

## Rentenalter

Das Rentenalter ist im Modell zugleich eine demografische Grenze und ein Szenarioparameter. Ein höheres Rentenalter erweitert den rechnerischen Erwerbsaltersbereich und verschiebt den Rentenzugang. Es garantiert aber keine Beteiligung, Beschäftigung oder zusätzliche Arbeitszeit. Die Beteiligungs- und Beschäftigungsannahmen für ältere Jahrgänge bleiben deshalb separat sichtbar.

## Modellgrenzen

Das Modell enthält keine Arbeitsnachfrage-, Berufs-, Qualifikations- oder individuellen Erwerbsbiografien. Ausbildung, Teilzeit, Betreuung, Krankheit, regionale Verteilung und Übergänge zwischen Beschäftigungen werden über aggregierte Quoten angenähert. Die Lohnsumme ist eine Szenarioannahme und keine individuelle Einkommensprognose.

## Unsicherheit und Ausgaben

Unter-, Zentral- und Oberpfad verändern Beteiligungs- und Beschäftigungsannahmen gemeinsam als Bandbreite. Sie sind keine drei unabhängigen politischen Empfehlungen. Erwerbspotenzial und Arbeitsvolumen werden außerdem getrennt von direkten Familien-, Migrations- oder Transferausgaben dargestellt.

## Quellen

- [Destatis: Erwerbstätigkeit](https://www.destatis.de/DE/Themen/Arbeit/Arbeitsmarkt/Erwerbstaetigkeit/_inhalt.html) – amtliche Erwerbs- und Arbeitsmarktstatistik.
- [Destatis: Mikrozensus](https://www.destatis.de/DE/Themen/Gesellschaft-Umwelt/Bevoelkerung/Mikrozensus.html) – Erwerbsbeteiligung und Arbeitszeit nach Erhebung; Modellübertragung bleibt eine Annäherung.
- [Bundesagentur für Arbeit: Arbeitsmarktberichte](https://statistik.arbeitsagentur.de/DE/Navigation/Statistiken/Arbeitsmarktberichte/Arbeitsmarktberichte-Nav.html) – Beschäftigung und Arbeitsmarkt; keine vollständige Langfristvorausberechnung.

## Verwandte Kapitel

- [Migration, Schutzstatus und Arbeitsmarktzugang](migration-schutzstatus-und-arbeitsmarktzugang.md)
- [Alterssicherung und vereinfachte Rentenindikatoren](alterssicherung-und-rentenindikatoren.md)
- [Demografie und Alterspyramide](demografie-und-alterspyramide.md)
