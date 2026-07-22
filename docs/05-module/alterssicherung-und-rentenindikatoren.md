---
title: Alterssicherung und vereinfachte Rentenindikatoren
summary: Aggregierte Beitrags-, Leistungs- und Finanzierungsindikatoren der gesetzlichen Rentenversicherung.
status: Implementiert 1.0
last_updated: 2026-07-22
---

# Alterssicherung und vereinfachte Rentenindikatoren

Die erste Ausbaustufe beschreibt die allgemeine gesetzliche Rentenversicherung aggregiert. Sie ist ein transparentes Langfristszenario und keine individuelle Rentenauskunft oder vollständige Versicherungsmathematik.

## Beitragsseite

Aus dem Erwerbspfad werden übernommen:

- Beitragszahlende,
- Vollzeitäquivalente,
- beitragspflichtige Lohnsumme.

Die vereinfachten Erwerbstätigenbeiträge berechnen sich als:

```text
beitragspflichtige Lohnsumme × effektiver Beitragssatz
```

Weitere Beitragseinnahmen, der allgemeine beziehungsweise zusätzliche Bundeszuschuss und sonstige Einnahmen werden separat ausgewiesen. Der Bundeszuschuss ist weder eine automatisch ausgeglichene Restgröße noch eine verdeckte Gegenfinanzierung.

## Leistungsseite

Der Rentenbestand wird aus den Alterskohorten ab dem gewählten Rentenzugangsalter und einer ausdrücklich gespeicherten Bezugsquote abgeleitet:

```text
Bevölkerung ab Rentenzugangsalter × Bezugsquote = geschätzte Rentenbeziehende
```

Damit werden Rentenbeziehende nicht pauschal mit allen älteren Personen gleichgesetzt. Sterblichkeit und Kohortenfortschreibung wirken über den Bevölkerungsbestand. Die durchschnittliche jährliche Rentenausgabe wird aus einer Basislohn- und Leistungsannahme mit dokumentierter Indexierung fortgeschrieben:

```text
Rentenbeziehende × durchschnittliche jährliche Ausgabe je Beziehendem
```

## Ergebnisindikatoren

| Indikator | Rechenweg und Einordnung |
|---|---|
| Beitragszahlende je 100 Rentenbeziehende | Strukturindikator; ersetzt keine Finanzrechnung. |
| Beitragseinnahmen | Lohnsumme multipliziert mit effektivem Beitragssatz. |
| Rentenausgaben | Geschätzte Rentenbeziehende multipliziert mit durchschnittlicher Jahresausgabe. |
| Finanzierungssaldo | Beiträge + weitere Einnahmen + Bundeszuschuss − Renten- und Verwaltungsausgaben. |
| Erforderlicher zusätzlicher Beitragssatz | Alternative Rechengröße, die eine Finanzierungslücke bei unverändertem Zuschuss ausgleichen würde. |
| Erforderlicher zusätzlicher Bundeszuschuss | Alternative Rechengröße; sie wird nicht zusätzlich zum Beitragssatz addiert. |

Ein negativer Finanzierungssaldo ist ein Szenarioergebnis. Er ist keine Aussage über einen Zahlungsausfall und keine politische Empfehlung.

## Rückkopplungen und Modellgrenzen

- Zusätzliche Migration erzeugt Beiträge nur über beitragspflichtige Beschäftigung und Arbeitsvolumen.
- Zusätzliche Geburten finanzieren keine heutigen Renten; sie erreichen Erwerbsalter erst nach dem modellierten Zeitverzug.
- Ein höheres Rentenalter schafft nicht automatisch Beschäftigung.
- Höhere Löhne erhöhen Beiträge und können über die Leistungsindexierung zugleich Ausgaben erhöhen.

Nicht individuell modelliert werden vollständige Entgeltpunktbiografien, sämtliche Rentenarten, Erwerbsminderungs- und Hinterbliebenenrenten, Zugangsfaktoren, Abschläge, Zuschläge, Kindererziehungs- und Pflegezeiten sowie Knappschaft und berufsständische Systeme im Detail.

## Quellen und Gültigkeitsbereich

- [Deutsche Rentenversicherung: Rentenversicherung in Zahlen](https://www.deutsche-rentenversicherung.de/SharedDocs/Downloads/DE/Statistiken-und-Berichte/statistikpublikationen/rv_in_zahlen.html) – Kennzahlen und Finanzgrößen; Kalenderjahr und Ausgabe sind zu speichern.
- [Deutsche Rentenversicherung: Aktuelle Daten](https://www.deutsche-rentenversicherung.de/SharedDocs/Downloads/DE/Statistiken-und-Berichte/statistikpublikationen/aktuelle_daten.html) – aktuelle Referenzdaten; nicht automatisch eine Langfristannahme.
- [Deutsche Rentenversicherung: Kennzahlen zur Finanzentwicklung](https://www.deutsche-rentenversicherung.de/DRV/DE/Experten/Zahlen-und-Fakten/Kennzahlen-zur-Finanzentwicklung/kennzahlen-zur-finanzentwicklung_node) – Einnahmen, Ausgaben und Zuschüsse.
- [Deutsche Rentenversicherung: Statistiken und Berichte](https://www.deutsche-rentenversicherung.de/DRV/DE/Experten/Zahlen-und-Fakten/Statistiken-und-Berichte/statistiken_und_berichte.html) – Quellenregister und methodische Einordnung.

## Verwandte Kapitel

- [Erwerbspotenzial und Arbeitsvolumen](erwerbspotenzial-und-arbeitsvolumen.md)
- [Migration, Schutzstatus und Arbeitsmarktzugang](migration-schutzstatus-und-arbeitsmarktzugang.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
