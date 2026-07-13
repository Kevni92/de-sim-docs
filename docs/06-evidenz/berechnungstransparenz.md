---
title: Berechnungstransparenz im Produkt
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.3
last_updated: 2026-07-13
---

# 15. Berechnungstransparenz im Produkt

## 15.1 Detailbutton

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

## 15.2 Rechenbaum

Der Nutzer kann den Rechenweg aufklappen:

```text
Zusätzliche Kita-Ausgaben
  └─ Anteil für Personal
      └─ zusätzliche Fachkraftstunden
          └─ geschätzte Änderung der Ausfallstunden
              └─ Arbeitsstunden der Eltern
                  └─ Bruttowertschöpfung und Steuern
```

Jeder Knoten zeigt seine eigene Unsicherheit. Die Gesamtaussage darf nicht sicherer erscheinen als die schwächste wesentliche Verbindung.

## 15.3 Quellenansicht

Jede Quelle zeigt:

- kurze Zusammenfassung,
- konkreten verwendeten Abschnitt,
- warum sie passend ist,
- warum sie möglicherweise nicht vollständig übertragbar ist,
- alternative Quellen,
- Datum der letzten Prüfung.

## 15.4 Export

Ein Szenarioexport enthält:

- alle Nutzereinstellungen,
- Ergebniswerte,
- Quellenliste,
- Parameterliste,
- Softwareversion,
- Datenvintage,
- reproduzierbare Szenario-ID.

## 15.5 Korrekturen

Fehler und Quellenänderungen werden öffentlich dokumentiert. Frühere Modellläufe bleiben mit ihrer damaligen Version abrufbar und werden nicht stillschweigend umgeschrieben.

## Verwandte Kapitel

- [Evidenzdatenbank und Quellenprovenienz](evidenzdatenbank.md)
- [Visualisierungen](../07-visualisierung/visualisierungen.md)
- [Technische Architektur](../08-technik/technische-architektur.md)
