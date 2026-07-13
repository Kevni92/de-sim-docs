---
title: Weitere Einnahmemodule
summary: Fachlicher Vertrag für Umsatzsteuer, Erbschaftsteuer, Vermögensteuer, Sozialbeiträge, Körperschaftsteuer, Kapitalertragsteuer sowie Energie- und Verbrauchsteuern.
status: Arbeitsstand 0.5
last_updated: 2026-07-13
---

# Weitere Einnahmemodule

Milestone 5 ergänzt sieben Einnahmemodule neben der Einkommensteuer. Sie verwenden ein gemeinsames fachliches Muster, dürfen aber ihre unterschiedlichen Steuerobjekte und Datenlagen nicht in eine scheinbar einheitliche Mikrosimulation vermischen.

## Gemeinsames Modellmuster

Jedes Modul trennt fünf Größen:

1. **Baseline**: gerundetes Ausgangsaufkommen und geltende Tarif- oder Beitragsparameter,
2. **Szenarioparameter**: durch Nutzende veränderbare Sätze, Freibeträge, Bemessungsgrenzen oder Indizes,
3. **statische Erstwirkung**: Wirkung bei unveränderter Bemessungsgrundlage,
4. **Verhaltenskomponente**: gesonderte Anpassungsannahme für Nachfrage, Ausweichen, Investitionen oder Deklaration,
5. **Unsicherheit und Inzidenz**: Bandbreite und modellierte wirtschaftliche Wirkungsträger.

Die allgemeine Aggregatlogik lautet:

\[
R_s = f(R_0, \theta_0, \theta_1)
\]

\[
R = R_s - (R_s - R_0) \cdot \varepsilon_m
\]

mit Ausgangsaufkommen \(R_0\), statischem Szenarioaufkommen \(R_s\), Parametersatz \(\theta\) und modulspezifischer Reaktionsstärke \(\varepsilon_m\). Die Reaktionsstärke ist eine Szenarioannahme und keine Prognose.

## Umsatzsteuer

### Baseline

- Regelsteuersatz: **19 Prozent**,
- ermäßigter Steuersatz: **7 Prozent**,
- Baseline-Aufkommen im Simulator: **291,4 Mrd. Euro**.

Die gesetzlichen Sätze folgen § 12 UStG. Steuerbefreiungen, Vorsteuerabzug und die Zuordnung einzelner Produkte sind im aktuellen Aggregatmodell nicht einzeln abgebildet.

### Parameter

- Regelsteuersatz,
- ermäßigter Steuersatz,
- Anteil ermäßigter steuerpflichtiger Umsätze,
- Preisweitergabe an Verbraucherpreise.

Die statische Wirkung wird über einen gewichteten Durchschnittssatz berechnet. Der Anteil ermäßigter Umsätze und die Preisweitergabe sind sichtbar gekennzeichnete Modellannahmen. Eine belastbare Verteilungswirkung erfordert später haushaltsspezifische Konsumprofile.

## Erbschaft- und Schenkungsteuer

Das Erbschaftsteuerrecht unterscheidet Steuerklassen, persönliche Freibeträge, progressive Steuersätze, sachliche Befreiungen und Verschonungsregeln. Das aktuelle Modul verdichtet diese Struktur bewusst zu einem Aggregatmodell.

Veränderbar sind:

- durchschnittlicher Modellsteuersatz,
- persönlicher Referenzfreibetrag,
- pauschalisierte Verschonung von Betriebsvermögen.

Die Berechnung darf nicht als Einzelfallberechnung nach dem ErbStG interpretiert werden. Besonders unsicher sind die Zusammensetzung großer Erwerbe, Betriebsvermögensbewertungen, Schenkungen innerhalb von Zehnjahreszeiträumen und Verhaltensreaktionen.

## Vermögensteuer

Die Vermögensteuer wird im Simulator mit einer **Baseline von null** geführt. Jede positive Einstellung ist daher ein hypothetisches Reformszenario und keine Fortschreibung einer gegenwärtigen Erhebung.

Veränderbar sind:

- proportionaler Steuersatz,
- persönlicher Freibetrag,
- Bewertungsabschlag.

Die vereinfachte Formel lautet:

\[
R_s = B_V \cdot s \cdot (1-a_F) \cdot (1-a_B)
\]

mit modellierter Vermögensbasis \(B_V\), Steuersatz \(s\), Freibetragsfaktor \(a_F\) und Bewertungsabschlag \(a_B\).

Die Vermögensbasis ist keine amtlich festgestellte aktuelle Steuerbemessungsgrundlage. Topvermögen, Unternehmensvermögen, Bewertung, Liquiditätseffekte und Ausweichreaktionen erzeugen deshalb ein besonders breites Unsicherheitsband.

## Sozialversicherungsbeiträge

Das Modul umfasst Renten-, Kranken-, Pflege- und Arbeitslosenversicherung. Für 2026 werden unter anderem folgende Ausgangsparameter verwendet:

- Rentenversicherung: **18,6 Prozent**,
- Arbeitslosenversicherung: **2,6 Prozent**,
- allgemeiner Krankenversicherungsbeitrag: **14,6 Prozent**,
- durchschnittlicher Zusatzbeitrag: **2,9 Prozent**,
- Pflegeversicherung: **3,6 Prozent** als Grundbeitrag im vereinfachten Modell,
- Beitragsbemessungsgrenze Rente und Arbeitslosigkeit: **101.400 Euro pro Jahr**,
- Beitragsbemessungsgrenze Kranken- und Pflegeversicherung: **69.750 Euro pro Jahr**.

Kinderlosenzuschlag, Abschläge nach Kinderzahl, kassenindividuelle Zusatzbeiträge, Minijobs, Selbstständige und weitere Sondergruppen werden noch nicht auf eine Modellbevölkerung verteilt. Die wirtschaftliche Last zwischen Beschäftigten und Arbeitgebern ist daher zunächst eine explizite Inzidenzannahme.

## Körperschaftsteuer

Die gesetzliche Körperschaftsteuer beträgt **15 Prozent**; der Solidaritätszuschlag wird als Zuschlag auf die festgesetzte Körperschaftsteuer parametrisiert. Das Aggregatmodell enthält zusätzlich:

- nutzbare Verlustverrechnung,
- pauschale investitionsfördernde Abzüge,
- eine getrennte Verhaltenskomponente.

Gewerbesteuer, Organschaften, internationale Mindestbesteuerung und grenzüberschreitende Gewinnverlagerung sind noch nicht vollständig integriert. Die dargestellte Verteilung auf Anteilseigner, Beschäftigte und Kundschaft ist eine Inzidenzannahme.

## Kapitalertragsteuer

Das Modul verwendet als Baseline einen Steuersatz von **25 Prozent**. Veränderbar sind:

- Abgeltungsteuersatz,
- Sparer-Pauschbetrag,
- nutzbare Verlustverrechnung.

Kirchensteuer, Günstigerprüfung, Investmentsteuer, unterschiedliche Verlustverrechnungstöpfe und die Verteilung von Kapitalerträgen werden noch nicht vollständig simuliert. Ergebnisse bleiben deshalb Aggregatrechnungen mit breitem Unsicherheitsband.

## Energie- und Verbrauchsteuern

Kraftstoffe, Strom, Tabak und Alkohol haben unterschiedliche physische Steuerbemessungsgrundlagen. Das Modul führt deshalb keine fiktive gemeinsame Prozentsteuer ein, sondern getrennte Belastungsindizes:

- Kraftstoffsteuer-Index,
- Stromsteuer-Index,
- Tabaksteuer-Index,
- Alkoholsteuer-Index.

Index 100 entspricht jeweils der Baseline. Änderungen skalieren den zugeordneten Aufkommensanteil. Mengenreaktionen werden ausschließlich über die gesonderte Verhaltenskomponente berücksichtigt.

## Ergebnisdarstellung

Für jedes Modul werden angezeigt:

- Baseline-Aufkommen,
- statisches Szenarioaufkommen,
- Ergebnis nach Verhaltensannahme,
- statische Veränderung,
- Verhaltenskomponente,
- Unsicherheitsband,
- angenommene Wirkungsträger,
- Formel, Parameter, Quellen und bekannte Grenzen.

Das Dashboard aggregiert ausschließlich die berechneten Aufkommensänderungen. Die Nettokreditaufnahme wird nicht automatisch als Gegenbuchung verändert; der Effekt erscheint im Budgetsaldo.

## Validierung

Mindestens folgende Tests sind verpflichtend:

- unveränderte Parameter reproduzieren die Baseline,
- eine Umsatzsteuererhöhung verändert statische und verhaltensbereinigte Wirkung nachvollziehbar,
- die Vermögensteuer bleibt bei einem Steuersatz von null bei null,
- Parameter bleiben nach Neuladen über Worker und IndexedDB erhalten,
- JSON-Export und -Import erhalten sämtliche Modulparameter,
- Dashboard und Detailseite zeigen denselben Szenariowert,
- jede Kennzahl öffnet den zugehörigen Nachweis,
- Mobile- und Desktop-Nutzerflüsse bleiben bedienbar.

## Bekannte Grenzen

- Noch keine gemeinsame repräsentative Mikrobevölkerung für alle Module.
- Teilweise kalibrierte Aggregatbemessungsgrundlagen statt Einzelfalldaten.
- Inzidenzannahmen sind nicht mit Verteilungsdaten validiert.
- Keine makroökonomische Gleichgewichtsrechnung.
- Keine automatische Interaktion zwischen Steuern, Beiträgen, Preisen, Löhnen und Unternehmensentscheidungen.
- Rechts- und Datenstände müssen bei jeder Aktualisierung neu geprüft werden.

## Quellen

- [Umsatzsteuergesetz, insbesondere § 12](https://www.gesetze-im-internet.de/ustg_1980/)
- [Erbschaftsteuer- und Schenkungsteuergesetz](https://www.gesetze-im-internet.de/erbstg_1974/)
- [Vermögensteuergesetz](https://www.gesetze-im-internet.de/vstg_1974/)
- [BMAS: Sozialversicherungsrechengrößen-Verordnung 2026](https://www.bmas.de/DE/Service/Gesetze-und-Gesetzesvorhaben/sozialversicherungs-rechengroessenverordnung-2026.html)
- [BMG: Beiträge der gesetzlichen Krankenversicherung](https://www.bundesgesundheitsministerium.de/beitraege)
- [BMF: Körperschaftsteuer](https://www.bundesfinanzministerium.de/Content/DE/Glossareintraege/K/koerperschaftsteuer.html?view=renderHelp)
- [BMF: Kapitalertragsteuer](https://www.bundesfinanzministerium.de/Content/DE/Standardartikel/Video-Textfassungen/Finanzisch/textfassung-kapitalertragsteuer.html)
- [Generalzolldirektion: Energie- und Verbrauchsteuern](https://www.zoll.de/DE/Fachthemen/Steuern/Verbrauchsteuern/Energie/energie_node.html)

## Verwandte Kapitel

- [Einnahmen und Steuern](einnahmen-und-steuern.md)
- [Einkommensteuer-Modul 2026](einkommensteuer-modul.md)
- [Systemgrenze und Baseline](systemgrenze-und-baseline.md)
- [Unsicherheit und Szenarien](../04-modell/unsicherheit-und-szenarien.md)
- [Berechnung und Quellen](../06-evidenz/berechnungstransparenz.md)
