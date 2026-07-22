---
title: Indirekte und langfristige Wirkungen
summary: Fachlicher Vertrag für zeitabhängige Wirkungsmodelle, Rückkopplungen, Unsicherheit und bewusste Nichtberechnung.
status: Implementiert 0.9
last_updated: 2026-07-21
---

# Indirekte und langfristige Wirkungen

Milestone 8 erweitert den HaushaltsKompass um eine eigenständige Wirkungs-Engine. Sie ergänzt unmittelbare Einnahmen- und Ausgabenänderungen um mögliche indirekte und zeitabhängige Entwicklungen. Die Ergebnisse sind **Szenariorechnungen unter Annahmen** und keine sicheren Prognosen.

## Modellstufen

Die zentrale Szenarioeinstellung steuert drei Stufen:

| Modellstufe | Enthalten |
|---|---|
| Statisch | unmittelbare finanzielle Erstwirkung ohne Verhaltensreaktion, Zeitverzug oder Rückkopplung |
| Verhalten | dokumentierte kurzfristige Verhaltensreaktionen und begrenzte indirekte Wirkungen |
| Langfristig | Zeitpfade, Demografie, Bildung, Produktivität, Erwerbsbeteiligung und fachlich begründete Rückkopplungen |

Ein Wechsel der Modellstufe verändert nicht die amtliche Ausgangsgröße, sondern nur die zusätzlich aktivierten Modellkomponenten.

## Ergebniszerlegung

Jedes berechnete Modul trennt mindestens:

- Baseline,
- direkte Erstwirkung,
- indirekte Wirkung,
- Beginn und Anlaufzeit,
- langfristige Wirkung,
- Rückkopplung,
- Untergrenze, Zentralwert und Obergrenze,
- betroffene Personen und Haushalte,
- monetäre und nicht monetäre Größen.

Zeitreihenpunkte enthalten Baseline, Szenariowert, direkte Wirkung, indirekte Wirkung, Rückkopplung sowie Unter- und Obergrenze. Werte verschiedener Jahre dürfen deshalb nicht als voneinander unabhängige Einzelschätzungen interpretiert werden.

## Evidenz- und Kausalitätsstatus

Jede Wirkung besitzt zwei getrennte Kennzeichnungen.

### Fachlicher Status

- amtlich beobachtete Ausgangsgröße,
- Modellrechnung,
- Szenarioannahme,
- externe Evidenz,
- nicht berechnet,
- nicht ausreichend belegt.

### Kausalitätseinordnung

- deskriptiv,
- korrelativ,
- kausal geschätzt,
- modelliert,
- hypothetisch.

Eine amtlich beobachtete Baseline ist nicht automatisch ein kausaler Effekt. Ebenso wird ein Literaturwert nicht ohne zusätzliche Begründung als auf Deutschland übertragbarer Kausaleffekt verwendet.

## Wirkungsbereiche

Das Register umfasst mindestens:

- Kita-Verfügbarkeit und Betreuungsausfälle,
- Erwerbsbeteiligung und Arbeitsvolumen,
- Krankheitstage und Gesundheit,
- Produktivität,
- Bildung und Qualifikation,
- Verwaltungskosten und Bürokratieaufwand,
- Migration und Integration,
- Geburtenentwicklung und Demografie,
- Altersstruktur sowie Renten-, Gesundheits- und Pflegeausgaben,
- Steuer- und Beitragseinnahmen über die Zeit,
- Infrastruktur- und Investitionswirkungen.

Module sind unabhängig kombinierbar. Abhängigkeiten und mögliche Rückkopplungen werden im Register explizit angegeben, damit dieselbe Wirkung nicht mehrfach vollständig addiert wird.

## Zwei Zugangswege auf dieselben Wirkungsdaten

Wirkungsdaten werden über zwei getrennte, aber konsistente Zugangswege sichtbar. Beide lesen denselben Wirkungslauf; keiner der beiden Wege verändert Werte, die der andere anzeigt.

### Kontextbezogene Folgewirkung

Innerhalb eines Einnahmen- oder Ausgabenmoduls erscheint unter **Mögliche Folgewirkungen** nur der Ausschnitt, der zur gerade bearbeiteten Maßnahme passt. Diese Ansicht ist bewusst schmal: Sie zeigt die direkte Wirkung weiterhin getrennt von der Verhaltens- und Folgekomponente und verweist erst bei Bedarf auf den vollständigen Berechnungsrahmen. Sie ersetzt keine Bevölkerungs- oder Wirkungsverwaltung und setzt keinen manuellen Modellstart voraus.

### Vollständiges Wirkungsregister

Über **Nachweise → Wirkungsregister** ist dieselbe Wirkungs-Engine zusätzlich als eigenständige, vollständige Fachansicht erreichbar. Dort lassen sich alle Wirkungsbereiche, Modellstufen, Zeithorizonte, Rückkopplungen und gespeicherten Läufe unabhängig von einem einzelnen Modul einsehen und vergleichen. Diese Ansicht richtet sich an Fachprüfung und Reproduzierbarkeit und ist keine gleichrangige Standardaufgabe.

Beide Wege führen zu denselben Zahlen: Ein im Modul sichtbarer Folgewirkungswert und der entsprechende Eintrag im Wirkungsregister widersprechen sich nicht, solange derselbe Wirkungslauf aktiv ist.

## Langfristige Demografie-, Arbeits- und Rentenpfade

Die implementierte Langfriststufe verbindet mehrere, weiterhin getrennte Rechenverträge:

- Kohortenfortschreibung mit Geburten, Sterbefällen, Zu- und Fortzügen und Altersgruppen,
- familienpolitische direkte Budgetwirkung getrennt von einem möglichen Geburtenpfad,
- Migration mit Schutzstatus, Erwerbsberechtigung und Beschäftigung als getrennten Übergängen,
- Erwerbsalter, Erwerbspotenzial, Erwerbspersonen, Beschäftigte, Vollzeitäquivalente und Beitragszahlende,
- Rentenbeziehende als Bezugsquote der Kohorten ab Rentenzugangsalter sowie Beiträge, Bundeszuschuss und Ausgaben.

Die gemeinsame Nutzeransicht zeigt höchstens vier Kernkennzahlen. Ursachen, Unsicherheitsband, Modellgrenzen und konkrete Zeitreihen werden erst in der progressiven Vertiefung geöffnet. Eine direkte Reformausgabe wird nicht mit späteren Beitragseinnahmen oder unsicheren Geburtenwirkungen verrechnet.

Weitere Rechenverträge stehen in den Kapiteln [Migration und Arbeitsmarktzugang](../05-module/migration-schutzstatus-und-arbeitsmarktzugang.md), [Erwerbspotenzial](../05-module/erwerbspotenzial-und-arbeitsvolumen.md) und [Alterssicherung](../05-module/alterssicherung-und-rentenindikatoren.md).

## Kita und Betreuung

Das implementierte Kita-Modul verwendet die aktive synthetische Bevölkerung und wertet Haushalte mit Kindern im relevanten Alter gewichtet aus. Es berücksichtigt insbesondere:

- verfügbare Betreuungsplätze,
- Ausfalltage,
- Öffnungsstunden,
- betreuungsbedingte Arbeitszeitreduktion,
- ausgefallene Arbeitsstunden,
- Rückkehr in Beschäftigung,
- Einkommenswirkung,
- Steuer- und Beitragswirkung,
- langfristige Erwerbsverläufe als Szenario.

Alleinerziehende, Haushalte mit zwei Erwerbspersonen, Teilzeitbeschäftigte und Einkommensgruppen werden als Zielgruppen getrennt ausgewiesen. Die Wirkungsparameter sind Annahmen mit dokumentierter Bandbreite; sie ersetzen keine individuelle Erwerbs- oder Betreuungsprognose.

## Zeitstruktur

Jedes quantifizierte Modul beschreibt:

- Wirkungsbeginn,
- Anlaufzeit,
- Zeitpunkt des Wirkungsmaximums,
- Abklingverhalten,
- temporären oder permanenten Charakter,
- maximalen Zeithorizont,
- mögliche Rückkopplung.

Die langfristige Stufe verwendet breitere Unsicherheitsintervalle als die kurzfristige Verhaltensstufe. Ein längerer Horizont erhöht nicht automatisch die Aussagekraft.

## Rückkopplungen

Rückkopplungen werden nur aktiviert, wenn sie fachlich begründet, transparent parametriert und numerisch stabil sind. Beispiele sind zusätzliche Steuer- und Beitragseinnahmen aus höherem Arbeitsvolumen oder Folgewirkungen von Infrastrukturinvestitionen.

Das Modell unterstellt nicht, dass zusätzliche Ausgaben sich selbst vollständig finanzieren. Direkte Kosten und fiskalische Rückflüsse bleiben getrennt sichtbar.

## Bewusste Nichtberechnung

Für Migration, Geburtenentwicklung, Demografie und altersabhängige Ausgaben kann die Engine relevante Zusammenhänge anzeigen, ohne einen monetären Punktwert zu liefern. Das geschieht insbesondere, wenn:

- keine belastbare deutsche Effektgröße vorliegt,
- nur Korrelationen bekannt sind,
- Übertragbarkeit oder Kausalität ungeklärt ist,
- mehrere gegenläufige Effekte nicht belastbar aggregiert werden können.

Die Oberfläche kennzeichnet solche Module als „nicht berechnet“ oder „nicht ausreichend belegt“. Diese Kennzeichnung ist ein fachliches Ergebnis und kein technischer Fehler.

## Unsicherheit und Darstellung

Langfristige Ergebnisse werden grundsätzlich als Bandbreite dargestellt. Eine Ausgabe wie „127.432 zusätzliche Beschäftigte“ ist unzulässig, wenn Daten- und Modelllage nur eine grobe Größenordnung tragen. Stattdessen werden gerundete Intervalle, relevante Zielgruppen, Annahmen und Grenzen gezeigt.

Nicht monetäre Wirkungen bleiben in ihrer natürlichen Einheit, etwa Arbeitsstunden, Krankheitstage, Betreuungsstunden oder Qualifikationsanteile. Eine monetäre Übersetzung darf nur zusätzlich und mit eigener Annahmenkennzeichnung erfolgen.

## Szenario- und Bevölkerungsbezug

Jeder Wirkungslauf referenziert:

- Szenario-ID,
- Bevölkerungslauf-ID,
- Modellversion,
- Daten- und Rechtsstand,
- Modellstufe,
- Zeithorizont,
- verwendete Parameter und Annahmen.

Personen- und Haushaltsdaten werden nicht in den zentralen React-Zustand oder den Szenarioexport kopiert. Das Szenario speichert lediglich die Referenz auf den aktiven Bevölkerungslauf und die gewählten Wirkungsparameter.

## Grenzen

- Die Engine ist keine amtliche Vorausberechnung.
- Verhaltens- und Langfristeffekte sind keine individuelle Beratung.
- Gemeinsame Effekte mehrerer Maßnahmen können trotz Überlappungsregeln verbleibende Modellunsicherheit enthalten.
- Nicht beobachtete gemeinsame Verteilungen der synthetischen Bevölkerung bleiben modelliert.
- Externe Evidenz ist nur innerhalb ihres dokumentierten Gültigkeitsbereichs verwendbar.

## Verwandte Kapitel

- [Wirkungsmodell](wirkungsmodell.md)
- [Indirekte und nicht monetäre Wirkungen](indirekte-und-nichtmonetaere-wirkungen.md)
- [Unsicherheit und Szenarien](unsicherheit-und-szenarien.md)
- [Synthetische Bevölkerung](../03-daten/synthetische-bevoelkerung.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
