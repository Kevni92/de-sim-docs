---
title: Figma-Prompt
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.3
last_updated: 2026-07-13
---

# 23. Figma-Prompt

Erstelle ein vollständiges, responsives UI-Konzept für einen deutschsprachigen Web-Simulator mit dem Arbeitstitel **„Deutschland-Simulator“**. Das Produkt erklärt Auswirkungen von Steuer-, Ausgaben- und Gesetzesänderungen auf Staatshaushalt, Haushalte, öffentliche Leistungen und langfristige gesellschaftliche Entwicklungen.

## Designziel

Das Interface soll sachlich, vertrauenswürdig, modern und datenorientiert wirken. Es ist kein Parteitool und darf keine politischen Lagerfarben verwenden. Keine verspielte Gamification. Komplexität wird durch klare Hierarchie, progressive Offenlegung und verständliche Erklärungen reduziert.

## Desktop-Layout bei 1440 Pixel

### Linke Spalte, 300 bis 340 Pixel

- Überschrift „Einnahmen“ mit Gesamtsumme und Veränderung zur Baseline.
- Suchfeld und Filter nach Bund, Ländern, Kommunen und Sozialversicherung.
- Hierarchische Tabelle mit Einkommensteuer, Umsatzsteuer, Unternehmenssteuern, Vermögen, Erbschaft, Verbrauchsteuern, Sozialbeiträgen und sonstigen Einnahmen.
- Jede Zeile zeigt Baseline, Szenario, Differenz und Evidenzbadge.
- Aufklappen öffnet Regler, Zahlenfelder und Tarifkurven.

### Mittlere Arbeitsfläche

Sticky Topbar mit:

- Szenarioname,
- Baseline-Jahr,
- Zeithorizont „Heute / 5 Jahre / 20 Jahre / 2070“,
- Rücksetzen, Vergleichen und Exportieren.

Darunter eine Haushaltsbilanz mit Einnahmen, Ausgaben, Saldo und Schuldenpfad.

Tabs:

1. Überblick,
2. Menschen,
3. Wirkungsketten,
4. Regionen,
5. Demografie,
6. Berechnung und Quellen.

Visualisierungen:

- Sankey-Diagramm der Geldflüsse,
- Wasserfall der Änderungen,
- Balken nach Einkommensdezilen,
- Deutschlandkarte,
- Alterspyramide mit Zeitregler,
- Wirkungsketten-Graph mit direkten und indirekten Folgen,
- Karten für Krankheitstage, Betreuungsstunden, Wartezeiten und Bildungsindikatoren.

### Rechte Spalte, 300 bis 340 Pixel

- Überschrift „Ausgaben“ mit Gesamtsumme und Veränderung.
- Hierarchische Tabelle mit Soziales, Rente, Gesundheit, Kita, Schule, Hochschule, Infrastruktur, Verteidigung, Verwaltung, Migration und Asyl, Subventionen und Zinsen.
- Jede Zeile zeigt Geld, Leistungsmenge und Wirkungsindikator.

## Zentrale neue Funktion: Wirkungsdimensionen

Beim Anklicken einer Maßnahme erscheint eine Detailseite mit Karten für:

- Staatshaushalt,
- persönliches Einkommen,
- Zeit und Planbarkeit,
- Leistungszuverlässigkeit,
- Arbeit und Produktivität,
- Gesundheit und Krankheitstage,
- Bildung und Humankapital,
- Demografie und Familiengründung,
- Verteilung,
- regionale Wirkung,
- Klima,
- Bürokratie und Vertrauen.

Jede Karte zeigt Richtung, Zeithorizont, betroffene Gruppen, Bandbreite und Evidenzstatus. Nicht quantifizierbare Wirkungen zeigen eine klare qualitative Aussage statt einer Fantasiezahl.

## Beispielscreen „Kita-Finanzierung“

Zeige links den Regler „öffentliche Kita-Ausgaben“. In der Mitte erscheint die Kette:

`Budget → Personalstunden → Ausfall- und Schließtage → Betreuungsstunden → Arbeitsstunden der Eltern → Einkommen und Staatseinnahmen → langfristige Bildungschancen`

Jeder Knoten ist anklickbar. Eine Seitenleiste erklärt Formel, Quelle und Unsicherheit.

## Beispielscreen „eAU abschaffen“

Zeige getrennt:

- Papier- und Verwaltungsaufwand,
- technische Betriebskosten,
- Fehlerquote,
- Vollständigkeit der Krankheitsstatistik,
- keine automatische Annahme, dass mehr registrierte Krankmeldungen mehr reale Krankheit bedeuten.

## Berechnungs- und Quellenansicht

Erstelle eine gut lesbare Provenienzansicht mit:

- Aussage in Alltagssprache,
- Baseline und Szenario,
- Formel,
- aufklappbarem Rechenbaum,
- Quellenkarten,
- Evidenzprofil mit getrennten Achsen für Quellenqualität, Kausalität, Übertragbarkeit, Aktualität und Präzision,
- Annahmen-Schaltern,
- Sensitivitätsdiagramm,
- Modell- und Datenversion.

## Evidenzbadges

Verwende neutrale Badges:

- Amtlicher Wert,
- Berechneter Wert,
- Verhaltensannahme,
- Szenarioannahme,
- Qualitativer Zusammenhang,
- Nicht ausreichend bekannt.

Keine Ampelfarben als moralische Bewertung. Farben dienen nur der Orientierung und müssen barrierefrei sein.

## Mobile

Unter 768 Pixel:

- Tabs „Einnahmen / Wirkung / Ausgaben“ als Bottom Navigation,
- kompakte Sticky-Bilanz,
- Diagramme untereinander,
- Detailansichten vollflächig,
- keine schmalen Modalfenster,
- mindestens 44 Pixel große Touch-Ziele.

## Designsystem

- helle und dunkle Variante,
- niedrige bis mittlere Border-Radien von 6 bis 10 Pixel,
- klare Kontraste,
- tabellarische Zahlen mit Tabular Nums,
- seriöse Sans-Serif-Schrift,
- zurückhaltende Schatten,
- 8-Pixel-Abstandssystem,
- sichtbare Fokuszustände,
- WCAG 2.2 AA.

Erstelle folgende Figma-Seiten:

1. Foundations und Tokens,
2. Komponentenbibliothek,
3. Desktop Überblick,
4. Steuereditor Einkommensteuer,
5. Ausgabendetail Kita,
6. Wirkungsketten und Quellen,
7. Alterspyramide und Deutschlandkarte,
8. Szenariovergleich,
9. Mobile Screens,
10. klickbarer Prototyp für den Weg von einer Änderung bis zur vollständigen Berechnungsquelle.

## Verwandte Kapitel

- [UI und Interaktionsmodell](../01-produkt/ui-und-interaktionsmodell.md)
- [Berechnungstransparenz im Produkt](../06-evidenz/berechnungstransparenz.md)
- [Visualisierungen](../07-visualisierung/visualisierungen.md)
