---
title: Branding und Darstellungsmodus
summary: Verbindliche Benennung, Logo-Verwendung und heller beziehungsweise dunkler Darstellungsmodus.
status: Arbeitsstand 1.0
last_updated: 2026-07-13
---

# Branding und Darstellungsmodus

## Produktname

Die sichtbare Produktbezeichnung der Anwendung lautet **HaushaltsKompass**.

Der Name erscheint mindestens:

- links oben in der globalen Kopfleiste,
- als Titel des Browser-Tabs,
- in zugänglichen Beschriftungen des Markenlinks.

Die fachliche Einordnung als Deutschland- und Staatshaushaltssimulator bleibt davon unberührt.

## Logos und Favicon

Für die Kopfleiste bestehen zwei aufeinander abgestimmte Logo-Varianten:

- eine helle Variante für die helle Darstellung,
- eine dunkle Variante für den Darkmode.

Die Logos werden proportional und kreisförmig skaliert. Auf kleinen Bildschirmen wird die Darstellung verkleinert, ohne die Kopfleiste zu verbreitern. Das Favicon wird aus der dunklen Logo-Variante abgeleitet und als kompaktes PNG eingebunden.

Die Logoauswahl folgt dem aktiven Darstellungsmodus. Das Logo ist dekorativ; der zugängliche Name wird über den Markenlink bereitgestellt.

## Heller und dunkler Darstellungsmodus

Die Anwendung unterstützt die Modi `light` und `dark`.

Beim ersten Aufruf gilt:

1. Eine bereits gespeicherte Wahl hat Vorrang.
2. Ohne gespeicherte Wahl wird `prefers-color-scheme` des Betriebssystems ausgewertet.
3. Wenn beides nicht verfügbar ist, wird die helle Darstellung verwendet.

Der Nutzer kann den Modus jederzeit über einen Mond- beziehungsweise Sonnen-Schalter in der Kopfleiste wechseln. Die Wahl wird im lokalen Browserspeicher unter `haushaltskompass-theme` gesichert und nach einem Neuladen wiederhergestellt.

Die Umschaltung aktualisiert zugleich:

- das globale Farbschema,
- Flächen, Linien, Texte und Eingabefelder,
- Status- und Diagrammfarben,
- die transparente Kopfleiste und die fixierten Kennzahlen,
- das Logo,
- die Browser-Theme-Farbe.

## Semantik und Barrierefreiheit

Der Darkmode verändert ausschließlich die Darstellung. Fachliche Bedeutung, Bewertung und Rechenlogik bleiben identisch.

Der Umschalter besitzt:

- eine eindeutige Aktionsbeschriftung,
- einen über `aria-pressed` erkennbaren Zustand,
- ein zusätzliches Symbol,
- einen sichtbaren Tastaturfokus.

Status, Konfidenz und Wirkungsrichtung dürfen weiterhin nicht ausschließlich über Farbe vermittelt werden. Die kontrastierenden Darkmode-Farben müssen Text, Rahmen, Diagramme und interaktive Zustände ausreichend unterscheidbar halten.

## Testanforderungen

Playwright prüft mindestens:

- Browser-Titel `HaushaltsKompass`,
- sichtbaren Produktnamen und sichtbares Logo,
- vorhandenes PNG-Favicon,
- Wechsel von heller zu dunkler Darstellung,
- aktualisierte zugängliche Beschriftung des Umschalters,
- Persistenz nach einem Neuladen,
- Desktop- und Mobilprojekt.

Der Test hängt einen echten Darkmode-Screenshot an den Playwright-Bericht an.

## Zusammenhang

Begleitende Dokumentation zu:

- https://github.com/Kevni92/de-sim/pull/11

## Verwandte Kapitel

- [UI-Referenz und Nutzerflüsse](ui-referenz-und-nutzerfluesse.md)
- [Dashboard-Modulstatus](dashboard-modulstatus.md)
