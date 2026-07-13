---
title: Implementierungsprinzipien
summary: Architekturentscheidungen, die spätere indirekte Wirkungen vorbereiten.
status: Entwurf
last_updated: 2026-07-13
---

# Implementierungsprinzipien

Nicht alle langfristigen Wirkungen werden im MVP berechnet. Die erste Implementierung muss sie strukturell vorbereiten.

## Von Beginn an erforderlich

- stabile IDs für Maßnahmen, Quellen, Claims, Parameter und Ergebnisse,
- getrennte Speicherung direkter, indirekter und langfristiger Wirkungen,
- Rechenbaum und Provenienzreferenz für jede Kennzahl,
- Zeitdimension und staatliche Ebene in jedem Ergebnisobjekt,
- Bandbreiten und qualitative Statuswerte,
- versionierte Baselines und austauschbare Module,
- keine hart codierten Erklärtexte ohne Modellreferenz.

## Später ergänzbar

Komplexe Verhaltensmodelle, Monte-Carlo-Simulationen, dynamische Demografie, regionale Mikrosimulation und monetäre Bewertungen einzelner nicht monetärer Effekte.

## Entscheidungsregel

Wenn nur eine unprüfbare Zahl möglich ist, wird eine Wirkung zunächst qualitativ mit Forschungsstatus dargestellt.

## Verwandte Kapitel

- [MVP und Roadmap](mvp-und-roadmap.md)
- [Wirkungsmodell](../04-modell/wirkungsmodell.md)
- [Technische Architektur](../08-technik/technische-architektur.md)
