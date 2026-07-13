---
title: Evidenzschema und Bewertungslogik
summary: Datenmodell für Quellen, Claims, Parameter und Wirkungskanten.
status: Entwurf
last_updated: 2026-07-13
---

# Evidenzschema und Bewertungslogik

## Source

Pflichtfelder sind stabile ID, Titel, Urheber, URL oder DOI, Publikations- und Abrufdatum, Quellentyp, Population, Geografie, Zeitraum, Methode, Einschränkungen und Lizenz.

## Claim

Ein Claim ist eine einzelne prüfbare Aussage aus einer Quelle. Er speichert Originalfundstelle, Paraphrase, Richtung, Zielpopulation, Kontext und Reviewstatus. Mehrere Claims können dieselbe Quelle verwenden.

## Parameter

Ein Parameter enthält Einheit, zentralen Wert, Bandbreite oder Verteilung, Gültigkeitszeitraum, Zielpopulation, Transformation und Quellen-Claim. Jede Transformation muss in der Berechnungsansicht erklärbar sein.

## Effect Edge

Eine Wirkungskante verbindet Ursache und Ergebnis. Sie enthält Richtung, funktionale Form, Zeitverzug, Gültigkeitsbereich, Evidenzstatus, Parameterreferenzen und Regeln gegen Doppelzählung.

## Bewertung

Quellenqualität, Kausalität, Übertragbarkeit, Aktualität, Präzision und Konsistenz werden getrennt bewertet. Die Oberfläche zeigt keine undurchsichtige Gesamtnote, sondern die entscheidenden Stärken und Schwächen.

## Verwandte Kapitel

- [Evidenzdatenbank](evidenzdatenbank.md)
- [Berechnungstransparenz](berechnungstransparenz.md)
- [Unsicherheit](../04-modell/unsicherheit-und-szenarien.md)
