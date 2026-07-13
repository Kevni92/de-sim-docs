---
title: Berechnung und Quellen
summary: Fachliche Anforderungen an nachvollziehbare Rechenwege, Quellen und Unsicherheiten.
status: Arbeitsstand 0.4
last_updated: 2026-07-13
---

# Berechnung und Quellen

## Detailansicht

Bei jeder Ausgabe gibt es den Button **„Berechnung und Quellen“**. Er öffnet eine Ansicht mit:

1. Aussage in Alltagssprache,
2. Definition der Kennzahl,
3. Baseline-Wert,
4. geänderter Wert,
5. Differenz,
6. vollständiger Formel,
7. Eingangsparameter,
8. Wirkungskette,
9. Quellen,
10. Evidenzbewertung,
11. Sensitivität,
12. bekannte Auslassungen,
13. Modell- und Datenversion,
14. Änderungsverlauf.

## Rechenbaum

Der Rechenweg kann schrittweise aufgeklappt werden:

```text
Zusätzliche Kita-Ausgaben
  └─ Anteil für Personal
      └─ zusätzliche Fachkraftstunden
          └─ geschätzte Änderung der Ausfallstunden
              └─ Arbeitsstunden der Eltern
                  └─ Bruttowertschöpfung und Steuern
```

Jeder Knoten zeigt seine eigene Unsicherheit. Die Gesamtaussage darf nicht sicherer erscheinen als die schwächste wesentliche Verbindung.

## Quellenansicht

Jede Quelle zeigt:

- kurze Zusammenfassung,
- konkret verwendeten Abschnitt,
- warum sie passend ist,
- warum sie möglicherweise nicht vollständig übertragbar ist,
- alternative Quellen,
- Datum der letzten Prüfung.

## Szenarioexport

Ein Szenarioexport enthält:

- alle Nutzereinstellungen,
- Ergebniswerte,
- Quellenliste,
- Parameterliste,
- Modellversion,
- Datenstand,
- reproduzierbare Szenario-ID.

## Korrekturen

Fehler und Quellenänderungen werden öffentlich dokumentiert. Frühere Modellläufe bleiben mit ihrer damaligen Version abrufbar und werden nicht stillschweigend umgeschrieben.

## Verwandte Kapitel

- [Evidenzdatenbank und Quellenprovenienz](evidenzdatenbank.md)
- [Visualisierungen](../07-visualisierung/visualisierungen.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
