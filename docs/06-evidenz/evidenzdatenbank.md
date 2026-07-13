---
title: Evidenzdatenbank und Quellenprovenienz
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.3
last_updated: 2026-07-13
---

# 14. Evidenzdatenbank und Quellenprovenienz

## 14.1 Ziel

Die Wirkungsdatenbank ist kein bloßes Literaturverzeichnis. Sie verbindet Quellen mit konkreten Aussagen, Modellparametern, Formeln und Rechenläufen.

## 14.2 Zentrale Objekte

| Objekt | Zweck |
|---|---|
| Source | Publikation, Gesetz, Statistik, Datensatz oder Expertenbeitrag. |
| DatasetVersion | Konkreter Datenstand mit Zeitraum, Geografie und Lizenz. |
| Claim | Aus einer Quelle abgeleitete Aussage. |
| Parameter | Numerischer oder qualitativer Modellwert. |
| EffectEdge | Zusammenhang zwischen zwei Knoten im Wirkungsgraph. |
| PolicyLever | Veränderbarer politischer Parameter. |
| OutcomeMetric | Sichtbare Ergebniskennzahl. |
| CalculationStep | Einzelner Rechenschritt mit Ein- und Ausgabe. |
| ModelRun | Vollständiger reproduzierbarer Lauf. |
| ReviewEvent | Fachliche Prüfung, Freigabe oder Beanstandung. |

## 14.3 Pflichtfelder einer Quelle

- eindeutige ID,
- Titel und Urheber,
- URL oder dauerhafter Identifikator,
- Publikationsdatum,
- Abrufdatum,
- Quellentyp,
- Population und Stichprobe,
- Geografie,
- Untersuchungszeitraum,
- Methode,
- zentrale Aussage,
- Einschränkungen,
- Lizenz und Nutzbarkeit,
- Archivkopie oder Prüfsumme, soweit rechtlich möglich.

## 14.4 Pflichtfelder eines Parameters

- Name und Definition,
- Einheit,
- zentraler Wert,
- Unter- und Obergrenze,
- Verteilung für Sensitivitätsanalysen,
- Gültigkeitszeitraum,
- Zielpopulation,
- Quelle und Claim,
- Transformation vom Originalwert,
- Reviewer,
- Status und Versionsnummer.

## 14.5 Mehrdimensionale Evidenzbewertung

Eine Quelle erhält nicht nur eine Gesamtnote. Bewertet werden getrennt:

1. **Quellenqualität:** amtliche Statistik, peer-reviewed, Working Paper, Bericht, Expertenannahme.
2. **Kausalität:** randomisiert, quasi-experimentell, modellbasiert, korrelativ, deskriptiv.
3. **Übertragbarkeit:** Deutschland direkt, teilweise übertragbar, Ausland oder historische Sondergruppe.
4. **Aktualität:** Datenalter und relevante Rechtsänderungen.
5. **Präzision:** Stichprobengröße, Konfidenzintervall und Messfehler.
6. **Konsistenz:** Übereinstimmung mit weiterer Literatur.

## 14.6 Statusklassen in der Oberfläche

- **Amtlicher Wert**
- **Berechneter Wert**
- **Verhaltensannahme**
- **Szenarioannahme**
- **Qualitativer Zusammenhang**
- **Nicht ausreichend bekannt**

## 14.7 Provenienzstandard

Die interne Struktur soll sich an W3C PROV-O orientieren: Daten und Ergebnisse sind Entitäten, Berechnungsschritte Aktivitäten und Autoren oder Systeme Agenten. Dadurch bleibt maschinell nachvollziehbar, welches Ergebnis aus welcher Quelle und Transformation entstanden ist.

## 14.8 FAIR-Prinzipien

Metadaten und öffentlich nutzbare Daten sollen auffindbar, zugänglich, interoperabel und wiederverwendbar sein. Zugangsbegrenzte Mikrodaten bleiben geschützt; ihre Metadaten und Transformationsregeln werden dennoch dokumentiert.

## Verwandte Kapitel

- [Berechnungstransparenz im Produkt](berechnungstransparenz.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Validierung, Governance und Ethik](../09-governance/validierung-governance-ethik.md)
