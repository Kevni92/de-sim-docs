---
title: Berechnung und Quellen
summary: Fachliche Anforderungen an nachvollziehbare Rechenwege, Quellen, Status und Unsicherheiten.
status: Arbeitsstand 0.7
last_updated: 2026-10-21
---

# Berechnung und Quellen

## Grundsatz

Keine zentrale Zahl darf ohne erkennbare Herkunft und Einordnung erscheinen. Zu jeder Kennzahl müssen Nutzer unterscheiden können, ob sie:

- unmittelbar auf einer amtlichen Grundlage beruht,
- aus einer Modellrechnung abgeleitet wurde,
- eine explizite Annahme darstellt,
- oder noch keinen belastbar bestimmten Status besitzt.

Der Status ist unabhängig von der Konfidenz. Eine amtliche Baseline kann zuverlässig sein, während eine daraus abgeleitete langfristige Wirkung große Unsicherheit besitzt.

## Bedeutung der Statusangaben

Statusangaben beschreiben, wie ein konkretes Ergebnis zustande kommt:

- **Regelberechnung:** Eine ausgewiesene gesetzliche Regel und ihr Rechtsstand werden auf die Szenarioeinstellungen angewendet. Das Resultat einer geänderten Regel ist ein Szenario, keine amtliche Prognose ihrer tatsächlichen Wirkung.
- **Modellschätzung:** Das Ergebnis nutzt Modellannahmen, gewichtete Referenzpunkte oder vereinfachte Zusammenhänge. Konfidenz, Reichweite und bekannte Grenzen bleiben direkt am Ergebnis zugänglich.
- **Beispielwert / Annahme:** Ein fester oder angenommener Wert ohne nachgewiesenen Beobachtungsstand wird als solcher benannt. Ein fehlendes Datenjahr wird nicht durch ein plausibel wirkendes Jahr ersetzt.
- **Noch nicht berechnet:** Es wird kein Ergebniswert vorgetäuscht. Der fehlende Status ist bereits am Einstieg in die betroffene Ergebnisgruppe sichtbar.

Eine Quelle kann eine Eingangsgröße oder die gesetzliche Baseline belegen. Sie bestätigt nicht automatisch die Modellannahmen, die Rechenqualität oder das Ergebnis, das daraus abgeleitet wird. Diese Unterschiede gelten gleichermaßen für Übersicht, Vergleich und Langfristansicht.

## Detailansicht

Bei jeder zentralen Ausgabe gibt es einen Nachweis- beziehungsweise Quellenbutton. Er öffnet eine Ansicht mit:

1. Aussage in Alltagssprache,
2. Definition der Kennzahl,
3. aktuell angezeigtem Szenariowert,
4. Einheit und Zeitraum,
5. Datenjahr und Rechtsstand,
6. Evidenzstatus und Konfidenz,
7. vollständiger Formel,
8. geordneten Rechenschritten,
9. Eingangsparametern und ihrer Provenienz,
10. Originalquellen,
11. Unsicherheit oder Sensitivität,
12. bekannten Auslassungen,
13. Modell- und Datenversion,
14. Änderungsverlauf.

## Transparenzregister

Zusätzlich zu den Nachweisen an einzelnen Zahlen gibt es ein zentrales Register. Es ermöglicht:

- Suche nach Kennzahl, Themenfeld oder Formel,
- Filterung nach amtlicher Grundlage, Modellrechnung oder Annahme,
- Vergleich von Daten- und Rechtsständen,
- Öffnen des vollständigen Rechenwegs,
- Erkennen noch nicht fachlich kalibrierter Bereiche.

Beispiele und nicht kalibrierte Modellteile dürfen nicht durch Gestaltung oder Wortwahl den Eindruck amtlicher Präzision erwecken. Die übrigen Ergebnisse werden anhand ihres eigenen Status eingeordnet, nicht pauschal als Beispiele abgewertet.

## Nicht belegte Bestandswerte

Ein fester Schuldenbetrag ohne nachgewiesenen Stichtag und passende amtliche Reihe ist als Annahme mit niedriger Konfidenz und ohne Datenjahr zu kennzeichnen. Die Oberfläche kann ihn als Beispielwert zeigen, muss dies direkt am Wert nennen und darf keine daraus abgeleitete Szenarioänderung, BIP-Quote oder Bandbreite vortäuschen.

Ein jährlicher Saldo bleibt als Stromgröße mit Zeitraum und Umfang benannt. Eine Änderung des jährlichen Saldos darf nur dort erscheinen; sie wird nicht als Änderung eines historischen Schuldenbestands ausgegeben. Ein Belegbutton führt zum vollständigen Nachweis der Beispielannahme und benennt ausdrücklich, welcher Referenzstand fehlt.

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

Für einfache Kennzahlen kann statt eines verzweigten Baums eine geordnete Liste von Rechenschritten verwendet werden. Entscheidend ist, dass Zwischenannahmen und Transformationen sichtbar bleiben.

## Parameter und Provenienz

Jeder Eingangsparameter zeigt mindestens:

- verständlichen Namen,
- verwendeten Wert oder Szenariobezug,
- zugehörige Originalquelle oder Kennzeichnung als Nutzereingabe,
- Datenjahr,
- bekannte Einschränkungen.

Eine modellinterne Größe darf nicht allein deshalb als amtlich bezeichnet werden, weil ein anderer Teil der Berechnung aus amtlichen Daten stammt.

## Quellenansicht

Jede Quelle zeigt:

- Titel und Institution,
- Original-URL,
- kurze Zusammenfassung,
- konkret verwendeten Zweck,
- warum sie passend ist,
- warum sie möglicherweise nicht vollständig übertragbar ist,
- alternative Quellen, soweit relevant,
- Datum der letzten Prüfung.

Mehrere Quellen können gemeinsam eine Kennzahl stützen. Baseline, Modelllogik und Annahmen werden dabei getrennt ausgewiesen.

## Unsicherheit

Unsicherheit wird je nach Kennzahl dargestellt als:

- relative Bandbreite,
- absoluter Wertebereich,
- Sensitivität gegenüber einzelnen Parametern,
- oder begründete Nichtanwendbarkeit bei rein deterministischen Darstellungen.

Eine fehlende quantifizierte Bandbreite bedeutet nicht, dass keine Unsicherheit besteht. In diesem Fall werden die Gründe beschrieben und die Konfidenz entsprechend vorsichtig eingestuft.

## Szenarioexport

Ein Szenarioexport enthält:

- alle Nutzereinstellungen,
- Ergebniswerte,
- referenzierte Kennzahlen- und Quellen-IDs,
- Parameterliste,
- Modellversion,
- Datenstand und Rechtsstand,
- reproduzierbare Szenario-ID.

## Korrekturen

Fehler, geänderte Formeln und Quellenänderungen werden dokumentiert. Frühere Modellläufe dürfen nicht stillschweigend auf eine neue Modellversion umgedeutet werden.

Der Änderungsverlauf einer Kennzahl enthält mindestens:

- Datum,
- Modell- oder Registerversion,
- verständliche Beschreibung der Änderung.

## Verwandte Kapitel

- [Informationsarchitektur und progressive Offenlegung](../01-produkt/informationsarchitektur-und-progressive-offenlegung.md)
- [Zielbild und Grundsätze](../01-produkt/vision-und-grundsaetze.md)
- [Evidenzdatenbank und Quellenprovenienz](evidenzdatenbank.md)
- [Visualisierungen](../07-visualisierung/visualisierungen.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
- [Bürgergeld- und Grundsicherungsmodul](../02-fiskal/buergergeld-modul.md)
