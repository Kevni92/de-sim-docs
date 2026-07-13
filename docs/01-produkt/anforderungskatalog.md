---
title: Anforderungskatalog
summary: Modulares Kapitel des Pflichtenhefts und Research Briefings.
status: Arbeitsstand 0.3
last_updated: 2026-07-13
---

# 3. Anforderungskatalog

## 3.1 Funktionale Kernanforderungen

| ID | Anforderung | Abnahmekriterium |
|---|---|---|
| FR-BAS-001 | Das System verwaltet versionierte Baselines. | Jeder Lauf nennt Rechtsstand, Datenstand und Preisjahr. |
| FR-SCN-001 | Nutzer können mehrere Szenarien speichern und vergleichen. | Mindestens drei Szenarien sind parallel vergleichbar. |
| FR-EIN-001 | Einnahmeposten sind hierarchisch aufklappbar und veränderbar. | Änderungen aktualisieren Haushalt und Verteilung live. |
| FR-AUS-001 | Ausgabeposten sind hierarchisch aufklappbar und veränderbar. | Änderungen zeigen Kosten, Leistungsmenge und Zielgruppen. |
| FR-WIR-001 | Jede Maßnahme zeigt direkte, indirekte und langfristige Wirkungen. | Mindestens ein Wirkungsgraph und eine Zeitleiste sind vorhanden. |
| FR-WIR-002 | Nicht monetäre Wirkungen werden als eigene Dimensionen dargestellt. | Zeit, Gesundheit, Bildung und Demografie sind nicht auf Euro reduziert. |
| FR-EVD-001 | Jede quantifizierte Wirkung besitzt Quelle, Formel und Unsicherheit. | Detailansicht ist aus jeder Kennzahl erreichbar. |
| FR-EVD-002 | Unzureichend belegte Wirkungen dürfen nicht als exakte Zahl erscheinen. | System zeigt „gerichtet“ oder „ungeklärt“. |
| FR-DEM-001 | Eine dynamische Alterspyramide zeigt demografische Szenarien. | Geburten, Sterblichkeit und Wanderung sind getrennte Annahmen. |
| FR-PER-001 | Beispielhaushalte und synthetische Haushalte zeigen Verteilungswirkungen. | Ergebnisse sind nach Dezil, Haushaltstyp und Region filterbar. |
| FR-REG-001 | Regionale Wirkungen können nach Bundesland dargestellt werden. | Karte nennt Datenauflösung und regionale Unsicherheit. |
| FR-TRC-001 | Jeder Modelllauf ist reproduzierbar. | Export enthält Szenario-, Daten- und Modellversion. |

## 3.2 Transparenzanforderungen

| ID | Anforderung |
|---|---|
| TR-001 | Neben jeder Zahl erscheint ihr Typ: amtlicher Wert, berechneter Wert, Verhaltensannahme oder unbekannt. |
| TR-002 | Evidenzqualität und kausale Aussagekraft werden getrennt bewertet. |
| TR-003 | Jede Wirkungskette zeigt alle Zwischenschritte. |
| TR-004 | Der Nutzer kann Annahmen einzeln deaktivieren. |
| TR-005 | Sensitivitätsbereiche sind wichtiger als eine einzelne Punktzahl. |
| TR-006 | Änderungen an Quellen und Parametern erhalten ein öffentliches Änderungsprotokoll. |

## 3.3 Nichtfunktionale Anforderungen

- Barrierefreiheit nach WCAG 2.2 AA.
- Gute Nutzung ab 360 Pixel Breite.
- Tastaturbedienung aller Regler und Diagramme.
- Alternative tabellarische Darstellung für jede Grafik.
- Ergebnisaktualisierung für einfache statische Änderungen unter 500 Millisekunden.
- Komplexe Langfristsimulationen mit sichtbarem Fortschritt und Abbruchmöglichkeit.
- Keine personenbezogene Speicherung ohne ausdrückliche Einwilligung.
- Rechenläufe müssen deterministisch reproduzierbar sein, sofern keine Monte-Carlo-Simulation gewählt wurde.

## Verwandte Kapitel

- [Vision und Grundsätze](vision-und-grundsaetze.md)
- [UI und Interaktionsmodell](ui-und-interaktionsmodell.md)
- [MVP und Roadmap](../10-roadmap/mvp-und-roadmap.md)
