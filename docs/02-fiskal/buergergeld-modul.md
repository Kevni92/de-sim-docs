---
title: Bürgergeld- und Grundsicherungsgeld-Modul
summary: Fachspezifikation für die monatliche Anspruchsberechnung, Unterkunft und Heizung, Jahreshochrechnung, Kalibrierung und transparente Szenarien.
status: Fachspezifikation 0.1
last_updated: 2026-07-13
---

# Bürgergeld- und Grundsicherungsgeld-Modul

## Ziel

Das Modul berechnet Leistungen der Grundsicherung für Arbeitsuchende nicht aus einem pauschalen Kostenindex, sondern aus konkreten gesetzlichen Parametern und einer gewichteten synthetischen Bevölkerung. Die primäre Recheneinheit ist die Bedarfsgemeinschaft im einzelnen Bezugsmonat.

Der sichtbare Arbeitsname **Bürgergeld** bleibt für bestehende Szenarien und die Verständlichkeit zunächst erhalten. Für den Rechtsstand ab 1. Juli 2026 verwendet das Sozialgesetzbuch den Begriff **Grundsicherungsgeld**. Begriff, Rechtsstand und Gültigkeitszeitraum werden deshalb in jedem Parametersatz ausdrücklich gespeichert.

Das Modul soll beantworten:

- welcher monatliche Bedarf für jede Person und Bedarfsgemeinschaft entsteht,
- welcher Teil durch Einkommen oder vorrangige Leistungen gedeckt wird,
- welche Unterkunfts- und Heizkosten anerkannt werden,
- welcher Zahlungsanspruch verbleibt,
- wie viele Personen und Bedarfsgemeinschaften betroffen sind,
- welche jährlichen Ausgaben nach Leistungsbestandteil und Kostenträger entstehen,
- wie stark das Modellergebnis von amtlichen Referenzwerten abweicht.

Es handelt sich um eine transparente Mikrosimulation auf vollständig synthetischen Datensätzen. Das Ergebnis ist keine individuelle Leistungsberatung und kein Ersatz für einen Bescheid des Jobcenters.

## Baseline und Zeitbezug

Das Modul trennt zwei Baselines:

| Baseline | Zweck | Standard |
|---|---|---|
| Rechtsbaseline | bestimmt Anspruchsregeln und Parameter | Rechtsstand 1. Juli 2026 |
| statistische Vergleichsbaseline | prüft Bestände, Zahlungsansprüche und Wohnkosten | jüngster fachlich vollständiger BA-Berichtszeitraum |
| Haushaltsbaseline | prüft staatliche Ausgabenabgrenzung | Bundeshaushalt 2026 sowie verfügbare Ist-Werte |

Eine aktuelle Rechtsbaseline darf nicht stillschweigend mit einem älteren Statistikjahr gleichgesetzt werden. Das Modell weist deshalb Rechtsstand, Datenstand und Haushaltsjahr getrennt aus.

Berechnet wird grundsätzlich monatlich. Jahreswerte entstehen erst danach aus Bezugsmonaten und Gewichten. Eine Stichtagszahl wird nicht pauschal mit zwölf multipliziert.

## Systemgrenze

### Bestandteil der ersten vollständigen Fassung

- Regelbedarf je Person und Regelbedarfsstufe,
- gesetzlich parametrierbare Mehrbedarfe,
- tatsächliche und anerkannte Unterkunftskosten,
- tatsächliche und anerkannte Heizkosten,
- Erwerbs- und sonstige Einkommen,
- Absetzbeträge und Freibeträge,
- vorrangige Leistungen,
- explizite Leistungsminderungen,
- monatlicher Anspruch je Person und Bedarfsgemeinschaft,
- gewichtete Jahreshochrechnung,
- Aufteilung nach Leistungsbestandteil und Kostenträger,
- Vergleich mit amtlichen Statistik- und Haushaltswerten.

### Zunächst getrennt oder nur als Referenz ausgewiesen

- Verwaltungskosten der Jobcenter,
- Leistungen zur Eingliederung in Arbeit,
- Bildung und Teilhabe,
- Beiträge zur Kranken- und Pflegeversicherung,
- Darlehen und Rückzahlungen,
- einmalige Leistungen mit geringer Fallzahl,
- Erstattungen zwischen Leistungsträgern,
- nicht realisierte Ansprüche und Nichtinanspruchnahme,
- Verhaltens-, Arbeitsmarkt- und Konjunkturfolgen.

Diese Positionen dürfen in einer Gesamtdarstellung ergänzt werden, werden aber nicht in den individuellen Regelbedarfsanspruch hineingerechnet.

## Fachliche Entitäten

### Person

Eine synthetische Person benötigt mindestens:

- Personen-ID und Haushalts-ID,
- Alter und Geburtsmonat beziehungsweise Altersstufe,
- Rolle im Haushalt,
- Erwerbsfähigkeit und gewöhnlichen Aufenthalt,
- Partnerschafts- und Eltern-Kind-Beziehung,
- Schwangerschaftsstatus, Alleinerziehungsstatus und weitere Mehrbedarfsmerkmale,
- monatliche Einkommensarten,
- Pflichtbeiträge, notwendige Ausgaben und weitere Absetzungen,
- vorrangige Leistungen,
- Vermögensmerkmale für die grundsätzliche Anspruchsprüfung,
- statistisches Personengewicht.

### Haushalt

Ein Haushalt ist eine Wohn- und Wirtschaftseinheit. Er kann mehrere Bedarfsgemeinschaften enthalten. Haushalt und Bedarfsgemeinschaft dürfen deshalb nicht synonym verwendet werden.

Benötigte Haushaltsmerkmale sind mindestens:

- Haushalts-ID,
- Mitglieder und Beziehungen,
- Region beziehungsweise zuständiger kommunaler Träger,
- Wohnstatus,
- Wohnfläche,
- tatsächliche Grundmiete,
- kalte Betriebskosten,
- Heizkosten,
- zentral oder dezentral erzeugtes Warmwasser,
- Einzugs- und Bezugsbeginn,
- statistisches Haushaltsgewicht.

### Bedarfsgemeinschaft

Eine Bedarfsgemeinschaft wird aus den gesetzlichen Zugehörigkeitsregeln und den Personenbeziehungen abgeleitet. Mindestens ein Mitglied muss die maßgeblichen Voraussetzungen des SGB II erfüllen. In einem Haushalt können mehrere Bedarfsgemeinschaften bestehen.

Der Datensatz enthält:

- stabile Bedarfsgemeinschafts-ID,
- zugehörige Personen,
- Referenzmonat,
- Bedarfsgemeinschaftstyp,
- Zahl der Erwachsenen und Kinder,
- leistungsberechtigte und nicht leistungsberechtigte Mitglieder,
- zu berücksichtigendes Einkommen und Vermögen,
- anteilige Wohnkosten,
- Bezugsstatus und Bezugsmonat,
- Hochrechnungsgewicht.

## Versionierter Parametervertrag

Jede Eingangsgröße besitzt:

| Feld | Bedeutung |
|---|---|
| `parameterId` | stabile fachliche Kennung |
| `value` | Wert ohne implizite Umrechnung |
| `unit` | Euro pro Monat, Prozent, Person, Quadratmeter oder andere eindeutige Einheit |
| `validFrom` / `validTo` | gesetzlicher oder statistischer Gültigkeitszeitraum |
| `legalStatusDate` | Rechtsstand |
| `dataStatusDate` | Datenstand, falls statistisch |
| `sourceId` | Verweis auf Quellenregister |
| `evidenceClass` | Gesetz, amtliche Statistik, Modell oder Annahme |
| `uncertaintyClass` | niedrig, mittel oder hoch |
| `roundingRule` | anzuwendende Rundungsregel |
| `notes` | Abgrenzung und bekannte Einschränkungen |

Ein Szenario ändert Werte in einem vollständigen Parametersatz. Es verändert keine einzelnen UI-Indizes, die außerhalb des Parametersatzes interpretiert werden müssten.

## Regelbedarfe 2026

Für die Rechtsbaseline 2026 gelten folgende monatliche Regelbedarfe:

| Regelbedarfsgruppe | Betrag |
|---|---:|
| Alleinstehende, Alleinerziehende und Volljährige mit minderjährigem Partner | 563 € |
| volljährige Partner, jeweils | 506 € |
| Volljährige unter 25 Jahren ohne eigenen Haushalt beziehungsweise bestimmter nicht zugesicherter Umzug | 451 € |
| Kinder von 14 bis 17 Jahren | 471 € |
| Kinder von 6 bis 13 Jahren | 390 € |
| Kinder von 0 bis 5 Jahren | 357 € |

Die Zuordnung erfolgt personengenau im jeweiligen Monat. Alterswechsel innerhalb eines Jahres wirken ab dem fachlich festgelegten Monat und werden nicht als Jahresdurchschnitt behandelt.

Quelle ist die amtliche Darstellung des BMAS zu den Leistungen und Bedarfen der Grundsicherung für Arbeitsuchende sowie die Regelbedarfsfortschreibung 2026.

## Bedarfsrechnung

Für eine Bedarfsgemeinschaft `b` im Monat `m` gilt zunächst:

```text
Bruttobedarf(b,m)
  = Summe Regelbedarf der Mitglieder
  + Summe anerkannte Mehrbedarfe
  + anerkannte Unterkunftskosten
  + anerkannte Heizkosten
  + modellierte einmalige oder sonstige Bedarfe
```

Der monatliche Anspruch lautet:

```text
Anspruch_vor_Minderung(b,m)
  = max(0,
      Bruttobedarf(b,m)
      - anrechenbares Einkommen(b,m)
      - anzurechnende vorrangige Leistungen(b,m))

Zahlungsanspruch(b,m)
  = max(0,
      Anspruch_vor_Minderung(b,m)
      - Leistungsminderung(b,m))
```

Jeder Summand bleibt im Ergebnis separat erhalten. Der Gesamtbetrag ist immer vollständig bis auf Personen- und Komponentenebene zerlegbar.

## Mehrbedarfe

Mehrbedarfe werden als eigene, versionierte Regeln modelliert. Eine Regel besitzt Voraussetzungen, Bemessungsgrundlage, Prozentsatz oder Eurobetrag, zeitliche Gültigkeit und eventuelle gemeinsame Obergrenzen.

Die erste Fassung berücksichtigt mindestens:

- Schwangerschaft ab der maßgeblichen Schwangerschaftswoche,
- Alleinerziehung abhängig von Zahl und Alter der Kinder,
- bestimmte Behinderungs- und Teilhabekonstellationen,
- kostenaufwändige Ernährung als gesondert parametrierte Fallgruppe,
- dezentrale Warmwassererzeugung,
- unabweisbare laufende besondere Bedarfe, soweit als Modellfall abbildbar.

Für 2026 sind unter anderem 17 Prozent für Schwangerschaft, gestaffelte Alleinerziehenden-Mehrbedarfe und 35 Prozent für bestimmte Teilhabeleistungen dokumentiert. Gemeinsame gesetzliche Obergrenzen werden nach der Reihenfolge des Rechenvertrags angewendet.

Nicht beobachtbare medizinische oder verwaltungsrechtliche Einzelfallentscheidungen werden nicht zufällig als sichere Tatsachen erzeugt. Sie benötigen eine dokumentierte Prävalenzannahme und eine erhöhte Unsicherheitsklasse.

## Einkommen, Absetzungen und Freibeträge

Einkommen wird zuerst nach Art und Person erfasst. Mindestens getrennt werden:

- Bruttoerwerbseinkommen,
- Nettoerwerbseinkommen,
- selbstständige Einkünfte,
- Arbeitslosengeld und andere Entgeltersatzleistungen,
- Renten und Versorgungsbezüge,
- Kindergeld,
- Unterhalt und Unterhaltsvorschuss,
- sonstige laufende Einnahmen,
- gesetzlich privilegierte oder nicht anzurechnende Einnahmen.

Die Berechnung erfolgt in dieser Reihenfolge:

```text
bereinigtes Einkommen
  = Brutto- oder Ausgangseinkommen
  - gesetzliche Pflichtbeiträge
  - Steuern
  - notwendige Versicherungen und Ausgaben
  - Grundabsetzbetrag
  - weitere personenbezogene Absetzungen

Erwerbstätigenfreibetrag
  = Summe der für die gültige Rechtsbaseline definierten Tarifsegmente

anrechenbares Einkommen
  = max(0, bereinigtes Einkommen - Erwerbstätigenfreibetrag)
```

Die Tarifsegmente werden nicht in der Formel hart codiert. Für jeden Abschnitt werden Untergrenze, Obergrenze, Prozentsatz, Zielgruppe und Gültigkeitszeitraum gespeichert. Der Parametersatz bildet insbesondere den Grundfreibetrag auf die ersten 100 Euro Erwerbseinkommen und die weiteren gesetzlichen Staffelungen ab.

Einkommen eines Kindes wird nicht ohne Rechtsgrundlage auf andere Mitglieder verteilt. Die Verteilung auf Personen und Bedarfsarten wird als eigener, testbarer Schritt dokumentiert.

## Vermögen und grundsätzliche Anspruchsprüfung

Vermögen beeinflusst zunächst, ob ein Leistungsanspruch dem Grunde nach besteht. Es wird nicht als negativer Monatsbetrag in die Leistungsformel eingesetzt.

Der Modellvertrag benötigt:

- verwertbares Vermögen je Person,
- Alters- und personenbezogene Freibeträge,
- geschützte Vermögensarten,
- besondere Härtefallregeln,
- Rechtsstand und Übergangsregeln.

Nicht ausreichend beobachtbare Vermögensarten werden als Modellannahme gekennzeichnet. Die Anspruchsprüfung gibt einen erklärbaren Status aus: anspruchsberechtigt, wegen Vermögen ausgeschlossen oder mangels Daten nicht sicher bestimmbar.

## Unterkunft und Heizung

Unterkunft und Heizung werden nicht durch einen bundesweiten Durchschnittsbetrag berechnet.

### Tatsächliche Kosten

```text
tatsächliche Unterkunftskosten
  = Grundmiete + kalte Betriebskosten

tatsächliche Heizkosten
  = laufende Heizkosten + zulässige einmalige Heizkostenanteile
```

### Regionale Anerkennungsregeln

Jeder regionale Datensatz enthält mindestens:

- Region beziehungsweise kommunalen Träger,
- Haushalts- oder Bedarfsgemeinschaftsgröße,
- angemessene Wohnfläche,
- Bruttokaltmietgrenze oder getrennte Miet- und Nebenkostengrenzen,
- optional Quadratmeterhöchstmiete,
- Heizkostengrenze oder verwendeten Heizspiegel,
- Gültigkeitszeitraum,
- Quelle und Veröffentlichungsdatum,
- Status als Satzung, Richtlinie, Statistik oder Modellannahme.

Für den Rechtsstand ab Juli 2026 wird die Begrenzung während der Unterkunfts-Karenzzeit auf das Eineinhalbfache der abstrakten örtlichen Angemessenheitsgrenze als versionierbare Regel abgebildet. Härtefälle und Bedarfsgemeinschaften mit Kindern werden nicht durch eine allgemeine mathematische Kürzung überschrieben, sondern erhalten eine explizite Entscheidungsregel.

### Berechnung

```text
anerkannte Unterkunftskosten
  = Anerkennungsregel(
      tatsächliche Unterkunftskosten,
      regionale Grenze,
      Haushaltsgröße,
      Bezugsdauer,
      Karenz- und Übergangsstatus,
      Härtefallstatus)

anerkannte Heizkosten
  = Anerkennungsregel(
      tatsächliche Heizkosten,
      regionaler oder bundesweiter Heizspiegel,
      Wohnfläche,
      Energieträger,
      Abrechnungszeitraum)
```

Tatsächliche und anerkannte Kosten bleiben beide sichtbar. Eine Differenz wird als nicht anerkannter Wohn- beziehungsweise Heizkostenanteil ausgewiesen.

Fehlen regionale Werte, gilt eine dokumentierte Fallback-Hierarchie. Ein Fallback darf niemals still einen Nullwert oder einen bundesweiten Durchschnitt als örtliches Recht ausgeben. Jede Fallback-Nutzung erhöht die Unsicherheitsklasse.

## Verteilung des Anspruchs

Die Bedarfsgemeinschaft ist die primäre Recheneinheit. Für Transparenz und Verteilungsanalysen wird das Ergebnis anschließend auf Personen und Komponenten aufgeteilt.

Die Zuordnung dokumentiert mindestens:

- persönlichen Regelbedarf,
- persönlichen Mehrbedarf,
- persönlichen Einkommensanteil,
- anteilige Unterkunft und Heizung,
- zugeordnete vorrangige Leistung,
- zugeordnete Minderung,
- persönlichen Zahlungsanspruch.

Die Summe der Personenwerte muss exakt dem Ergebnis der Bedarfsgemeinschaft entsprechen. Etwaige Rundungsdifferenzen werden nach einer versionierten Restcent-Regel verteilt.

## Monats- und Jahreshochrechnung

Für jede Bedarfsgemeinschaft und jeden simulierten Monat gilt:

```text
gewichteter Monatsbetrag
  = Zahlungsanspruch × Bedarfsgemeinschaftsgewicht
```

Der Jahreswert einer Komponente `k` lautet:

```text
Jahresausgabe(k)
  = Summe über alle Bedarfsgemeinschaften und Bezugsmonate
    (Komponentenbetrag(k,b,m) × Gewicht(b,m))
```

Unterjährige Zu- und Abgänge, Alterswechsel, Einkommensänderungen, Umzüge und Bezugsunterbrechungen werden über Monatszustände oder explizite Bezugsmonate abgebildet. Die Hochrechnung nennt verwendete Stichprobengröße, Gewichtssumme und Zahl der simulierten Bezugsmonate.

## Leistungsbestandteile und Kostenträger

Anspruchsberechnung und staatliche Finanzierungsabgrenzung sind getrennte Schichten.

Mindestens ausgewiesen werden:

- Regelbedarf,
- Mehrbedarfe,
- Unterkunft,
- Heizung,
- sonstige modellierte Leistungen,
- Einkommen und vorrangige Leistungen als bedarfsmindernde Positionen,
- Leistungsminderungen.

Die Kostenträgerzuordnung enthält mindestens Bund und kommunale Träger. Weitere Träger werden ergänzt, wenn die jeweilige Position fachlich in den Modellumfang aufgenommen wird. Eine Änderung der Finanzierungsquote darf den individuellen Anspruch nicht verändern.

## Amtlicher Abgleich

Der Referenzlauf wird nicht durch eine freie Restgröße künstlich auf eine Haushaltszahl gezwungen.

Verglichen werden mindestens:

- Zahl der Bedarfsgemeinschaften,
- Personen in Bedarfsgemeinschaften,
- Bedarfsgemeinschaftstypen,
- Zahlungsansprüche,
- Regelbedarf und Mehrbedarf,
- Unterkunft und Heizung,
- Einkommen und Erwerbstätigkeit,
- regionale Verteilung,
- Bundes- und kommunale Ausgabenabgrenzungen.

Die Statistik der Bundesagentur für Arbeit unterscheidet Bestände und Zahlungsansprüche zu statistischen Stichtagen von tatsächlichen Ausgabenströmen. Der Bundeshaushalt bildet wiederum Titel und Kostenträgerabgrenzungen ab. Diese Größen werden nicht als identisch behandelt.

Der Abgleich zeigt für jede Komponente:

| Kennzahl | Bedeutung |
|---|---|
| Referenzwert | amtliche Vergleichsgröße |
| Modellwert | Ergebnis des festen Referenzlaufs |
| absolute Abweichung | Modell minus Referenz |
| relative Abweichung | absolute Abweichung geteilt durch Referenz |
| Abgrenzungsstatus | direkt vergleichbar, teilweise vergleichbar oder nicht vergleichbar |
| Ursachen | bekannte Daten-, Zeit-, Rechts- oder Modellunterschiede |

## Unsicherheit und Qualitätskennzeichnung

### Niedrige Unsicherheit

- gesetzlicher Eurobetrag oder Prozentsatz mit eindeutigem Rechtsstand,
- deterministische Anwendung auf vollständig bekannte Merkmale,
- direkte arithmetische Aggregation.

### Mittlere Unsicherheit

- synthetische gemeinsame Verteilung trotz guter Randkalibrierung,
- regionale Hochrechnung aus teilweise verfügbaren Unterkunftsdaten,
- modellierte Bezugsdauer und unterjährige Übergänge.

### Hohe Unsicherheit

- medizinische oder verwaltungsrechtliche Einzelfallmerkmale ohne repräsentative Mikrodaten,
- Fallback für fehlende kommunale Angemessenheitswerte,
- Nichtinanspruchnahme,
- Verhaltens- und langfristige Folgewirkungen.

Jedes Ergebnis erhält Datenstand, Rechtsstand, Modellversion, Quellen-IDs, Qualitätsstatus, Unsicherheitsklasse und bekannte Einschränkungen.

## Szenarien und Benutzeroberfläche

Der Einfachmodus darf Parametergruppen proportional verändern, muss daraus aber denselben kanonischen Parametersatz erzeugen wie der Expertenmodus.

Im Expertenmodus sind mindestens bearbeitbar:

- Regelbedarfe in Euro pro Monat,
- Mehrbedarfsprozentsätze und Obergrenzen,
- Freibetragssegmente,
- regionale Unterkunftsgrenzen,
- Heizkostenregeln,
- ausgewählte Minderungsregeln,
- Kostenträgerquoten, getrennt von der Anspruchsberechnung.

Jedes Eingabefeld zeigt Einheit, Baseline, Szenariowert, Quelle, Rechtsstand und Unsicherheit. Die Ergebnisansicht zeigt Baseline, Szenario und Differenz nach Komponenten sowie betroffene Personen und Bedarfsgemeinschaften.

## Mindestprüffälle

Die Implementierung benötigt Golden Cases für mindestens:

1. alleinstehende Person ohne Einkommen,
2. Paar ohne Einkommen,
3. Paar mit Kindern und Kindergeld,
4. alleinerziehende Person mit Mehrbedarf,
5. erwerbstätige aufstockende Person an jeder Freibetragsgrenze,
6. tatsächliche Miete unterhalb, auf und oberhalb der regionalen Grenze,
7. Karenz- und Übergangsfall für Unterkunft,
8. dezentrale Warmwassererzeugung,
9. Nullanspruch durch Einkommen,
10. Teilleistung durch Einkommen,
11. Vermögensausschluss,
12. Leistungsminderung,
13. unterjähriger Ein- und Austritt,
14. Bedarfsgemeinschaft mit Rundungsrest.

Für jeden Fall werden Eingaben, Zwischenwerte, Rundung und erwartetes Ergebnis versioniert gespeichert.

## Quellen

- [Sozialgesetzbuch II](https://www.gesetze-im-internet.de/sgb_2/)
- [BMAS: Leistungen und Bedarfe in der Grundsicherung für Arbeitsuchende](https://www.bmas.de/DE/Arbeit/Grundsicherung-fuer-Arbeitsuchende/Leistungen-und-Bedarfe-in-der-Grundsicherung-fuer-Arbeitsuchende/leistungen-und-bedarfe-in-der-grundsicherung-fuer-arbeitsuchende.html)
- [BMAS: Fortschreibung der Regelbedarfe 2026](https://www.bmas.de/DE/Service/Gesetze-und-Gesetzesvorhaben/verordnung-zur-fortschreibung-der-regelbedarfe-fuer-das-jahr-2026.html)
- [Bundesagentur für Arbeit: Grundsicherung für Arbeitsuchende – Statistik](https://statistik.arbeitsagentur.de/DE/Navigation/Statistiken/Fachstatistiken/Grundsicherung-fuer-Arbeitsuchende-SGBII/Grundsicherung-fuer-Arbeitsuchende-SGBII-Nav.html)
- [Bundesagentur für Arbeit: Bedarfe, Zahlungen, Einkommen und Wohnkosten](https://statistik.arbeitsagentur.de/DE/Navigation/Statistiken/Fachstatistiken/Grundsicherung-fuer-Arbeitsuchende-SGBII/Leistungen-Einkommen-Bedarfe-Wohnkosten/Leistungen-Einkommen-Bedarfe-Wohnkosten-Nav.html)
- [Bundeshaushalt digital](https://www.bundeshaushalt.de/DE/Bundeshaushalt-digital/bundeshaushalt-digital.html)

## Verwandte Kapitel

- [Ausgabenmodule 2026](ausgabenmodule.md)
- [Synthetische Bevölkerung](../03-daten/synthetische-bevoelkerung.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
- [Quellenregister](../06-evidenz/quellenregister.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
