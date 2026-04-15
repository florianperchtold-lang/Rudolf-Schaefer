# 04_CONTENT — Texte & Inhalte
<!-- Rudolf Schäfer KG | April 2026 -->
<!-- Quellen: rudolfschaefer_deutsch.docx + rudolfschaefer_english.docx (März 2026) -->

---

## Content-Prinzipien

- **Kein Hardcoding** – alle Texte über CMS-Felder, nie im Template
- **Genau eine H1** pro Seite – Primary Keyword am Anfang
- **Alt-Text Pflichtfeld** im CMS – kein Upload ohne Alt-Text möglich
- **Single Source of Truth** – Firmendaten einmal im Settings-Singleton
- **FAQ auf jeder Leistungsseite** – als Schema FAQPage markiert
- **Mindest-Wortanzahl** je Seitentyp einhalten (→ 05_SEO)

---

## Globale Firmendaten (Settings-Singleton)

```
firmenname:      Rudolf Schäfer KG
strasse:         Max-Joseph-Straße 8
plz:             80333
ort:             München
telefon:         089 – 59 98 91 00
fax:             089 – 550 40 95
email:           info@rudolfschaefer.de
gruendungsjahr:  1922
mitarbeitende:   23
geo_lat:         48.1399
geo_lng:         11.5708

oeffnungszeiten:
  Mo/Mi/Do: 08:00–12:00 & 13:00–17:00
  Di:       08:00–12:00
  Fr:       08:00–13:00

app_ios_url:     https://apps.apple.com/bg/app/rudolf-schäfer-kg/id6451483817
app_android_url: https://play.google.com/store/apps/details?id=de.idwell.rudolfschaefer
app_login_url:   https://rudolfschaefer.idwell.com/login
```

---

## Navigation

```
DE: Hausverwaltung | Vermietung | Verkauf | Service | Über uns | Team | Kontakt
EN: Property Management | Rentals | Sale | Service | About | Team | Contact
```

---

## Startseite (/)

### Hero
- **H1:** Ihre Immobilienprofis für München – seit 1922
- **Subline:** Aus dem Kreis der größtenteils langjährigen Auftraggeberinnen und Auftraggeber bestehen uns Privatpersonen und institutionelle Anleger.
- **CTA:** Leistungen entdecken → /hausverwaltung/
- **Trust-Badges:** seit 1922 | ~23 Mitarbeitende | mehrere tausend Einheiten
- **Foto:** [OFFEN – Büro / Repräsentatives Münchner Objekt]

### Intro-Text (ca. 200 Wörter, SEO-optimiert)
> Die Rudolf Schäfer KG zählt zu den traditionsreichsten und renommiertesten Immobilienunternehmen Münchens. Sie ist nicht nur im klassischen Hausverwaltungssegment kompetenter Ansprechpartner, sondern auch bei der Immobilienvermarktung. Die Rudolf Schäfer KG verwaltet in München und Umgebung Mietshäuser und Gewerbeanlagen im Umfang von mehreren tausend Einheiten.

### Kernstärken (4 Felder – aufklappbar)
| Titel | Text |
|-------|------|
| Kompetenz | Seriöse, sorgfältige Beratung in allen Immobilienfragen |
| Klarheit | Transparente Darstellung von Zahlungsströmen und Ausgaben |
| Kontinuität | Jahrzehntelange Marktbeobachtung im Münchner Raum |
| Kundenorientierung | Optimale Unterstützung bei der Immobilienbewirtschaftung |

### Trust-Counter (alle Werte aus CMS)
- 100+ Jahre Erfahrung
- ~23 Mitarbeitende
- 5.921 Newsletter-Abonnenten
- mehrere tausend Wohn- und Gewerbeeinheiten

### Testimonials (3 Kundenstimmen – vorhanden)
1. *„Meine Familie und ich fühlen uns seit mehreren Jahrzehnten bei den Herren Schäfer und deren Mitarbeitern in besten Händen."* — Geschwister Schmuck
2. *„Ich habe die Hausverwaltung Schäfer bereits mehrfach weiterempfohlen."* — H. Traut
3. *„Wir vertrauen der Firma Rudolf Schäfer nun schon seit Jahrzehnten."* — E. Burkhardt

### App-Teaser
→ Aus App-Settings + 3 Features (schnell / interaktiv / transparent)

### Referenzen (Startseite-Flag in Referenz-CT)
Aus DE-Dokument: Nymphenburg (2x MFH), Schwabing (2x WGH), Maxvorstadt (WGH), Lehel (WGH), Altstadt (Verkauf MFH), Schwabing-West (Investmentobjekt)

---

## Hausverwaltung (/hausverwaltung/)

- **H1:** Hausverwaltung München – professionell seit 1922
- **Mindest-Wortanzahl:** 1.500+

### 5 Leistungsbereiche (Akkordeon)

**Geschäftsleitung**
- Ansprechpartner für Eigentümer in allen Belangen
- Wertanalyse, Entwicklung Verkaufs- und Vermarktungsstrategie
- Prüfung von Optimierungsmöglichkeiten (Wertsteigerung, Modernisierungen)
- Mediation im Streitfall

**Verwaltung**
- Laufende kaufmännische Betreuung, Vertretung gegenüber Mietern, Behörden und Gerichten
- Überprüfung und Anpassung der Miethöhen
- Management aller Hausverwalter-Verträge (Hausmeister, Versicherungen etc.)
- Abrechnung der Betriebs- und Heizkosten
- Anlegen und Abrechnen der Kautionen
- Überwachung des Hausfriedens und der Hausordnung

**Technik**
- Veranlassung von Reparaturen und Instandsetzungen
- Technische Betreuung und Kontrolle
- Überwachung von Sanierungen und Renovierungen
- Auswahl professioneller Handwerksunternehmen, Einholung von Angeboten
- Vorausplanung von Instandhaltungen sowie Prüfung von Sicherheitseinrichtungen
- Verfolgung von Gewährleistungsansprüchen, Abwicklung von Versicherungsschäden

**Buchhaltung**
- Regelmässige Hausabrechnungen durch hausinterne Buchhaltung
- Individuelle und persönliche Beratung
- Entgegennahme der Mieten und Verfolgung der Zahlungsansprüche
- Kontenverwaltung (Miet- und WEG-Bereich)
- Umfängliches Rechnungswesen

**Vermietung (als Teil der Hausverwaltung)**
- Vermietung freiwerdender Wohnungen und Gewerberäume
- Vermarktung über mehrere Kanäle
- Vertragsgestaltung gemäss gesetzlicher Vorgaben
- Berechnung und Empfehlung von Miethöhen
- Persönliche Mieterauswahl inkl. Bonitätsprüfungen

### Philosophie
> Kombination aus langjähriger Erfahrung, aktueller Marktübersicht und persönlicher Beratung. Fokus auf Werterhalt und Wertsteigerung. Ehrenamtliches Engagement im IVD und der IHK München und Oberbayern.

### Referenzen (8 Objekte – aus DE-Dokument)
Obersendling (Bürohaus), Bogenhausen (MFH), Maxvorstadt (WGH), Schwabing (WGH), Ludwigsvorstadt (MFH), Schwabing (MFH), Sendling (Wohnhaus), Haidhausen (WGH)

### Ansprechpartner
Martin Schäfer – Komplementär | 089 – 59 98 91 00 | info@rudolfschaefer.de

---

## Vermietung (/vermietung/)

- **H1:** Mietwohnungen und Gewerbeflächen in München
- Intro: Das verwaltete Eigentum ist so vielfältig wie der Münchner Immobilienmarkt...
- **Aktuelle Angebote:** nativ aus Mietobjekt-CT (kein iframe)
- **Filter:** Objektart / Stadtteil / Zimmer / Preis
- **Hinweis:** Alle Wohnungen provisionsfrei
- **Newsletter-Anmeldung:** 5.921 Abonnenten-Bestand (System klären)

### Maklerservice (4 Schritte)
1. **Exposé** – Verfassen mit Fotos und Immobilieninfos
2. **Vermarktung** – Interessentenliste, Newsletter, Internetanzeigen
3. **Besichtigung** – Organisation, Vorstellungsgespräche, Bonitätsprüfung
4. **Mietvertrag** – Mietervorschlag, Vertragsgestaltung, Übergabe, Kaution

### Ansprechpartner Vermietung
- Peter Gemander – Leitung HV Wohnen/Technik/Vermietung | p.gemander@rudolfschaefer.de
- Karin Breyl – Vermietung | vermietung@rudolfschaefer.de
- Elea Franke – Vermietung | e.franke@rudolfschaefer.de
- Monika Montenbruck – Sekretariat/Vermietung | m.montenbruck@rudolfschaefer.de

---

## Verkauf (/verkauf/)

- **H1:** Immobilie verkaufen in München – kompetente Begleitung
- Intro: Umfassende Kenntnis des Münchner Immobilienmarkts...

### 6 Prozessschritte
1. **Beratung** – Persönliches Erstgespräch, Klärung von Wünschen
2. **Bewertung** – Marktgerechte Schätzung durch Martin Schäfer (Immobilienbewerter DIA)
3. **Exposé** – Hochwertiges Exposé mit Fotos
4. **Vermarktung** – Interessentenkontakte, Netzwerk-Aktivierung
5. **Besichtigung & Prüfung** – Organisation, Bonitätsprüfung, Finanzierungsmodelle
6. **Kaufvertrag** – Notarauswahl, Vertragsausarbeitung, Beurkundungsbegleitung, Übergabe

### Referenzen Verkauf
- Altstadt | München – Mehrfamilienhaus (Komplettvermarktung)
- Schwabing-West | München – Investmentobjekt
- Nymphenburg | München – Wohnung

### Ansprechpartner
Martin Schäfer – Komplementär | Tel.: 089 – 59 98 91 00 | info@rudolfschaefer.de
IVD-Süd Vorstand seit 2007 | IHK München seit 2010 | Ehrenamtlicher Finanzrichter seit 2016

---

## Service (/service/)

- **H1:** Service – Ihre direkte Verbindung zur Hausverwaltung

### Rudolf Schäfer App
Kostenlose App – powered by iDWELL

| Vorteil | Beschreibung |
|---------|--------------|
| Schnell & effizient | Digitale Dokumentenmappe, 24/7 abrufbar |
| Interaktiv | Schadensmeldungen mit Fotos, Status-Updates |
| Transparent | Digitales Schwarzes Brett, Nachrichtenfunktion |

Download: App Store | Google Play | Web-Login: rudolfschaefer.idwell.com/login

### FAQ (15 Fragen DE – vollständig aus Dokument)

**Für Mieter:**
- Wie melde ich mich für den Vermietungs-Newsletter an? → Kontaktformular auf Vermietungsseite
- Wie ändere ich meinen Mietvertrag? → Online-Formular, Post, E-Mail oder Fax
- Wann beginnt ein Mietvertrag? → Am 1. oder 16. des Monats
- Wie kündige ich einen Mietvertrag? → Schriftlich per Post (nicht E-Mail/Fax), von allen Mietern unterschrieben
- Wie erhalte ich einen neuen Schlüssel? → Schriftlich mit Schlossername, Schliessnummer, Schlüsselnummer
- Wann erhalte ich meine Kaution zurück? → In der Regel 6–8 Wochen nach Mietende, max. 6 Monate
- Wer hilft im Notfall? → Hausmeister (Aushang im Treppenhaus)
- Geschäftszeiten? → Mo–Do 8–12 & 13–17, Fr 8–13
- Ist eine Provision fällig? → Nein, alle Wohnungen provisionsfrei
- Wie hoch ist die Kaution? → Wohnen: 3 Nettokaltmieten | Gewerbe: 3 Bruttowarmmieten inkl. MwSt.
- Was tun bei Heizungsausfall? → Hausmeister, dann Heizungsdienst
- Was ist eine Legionellenprüfung? → EU-rechtlich vorgeschriebene Beprobung des Trinkwassers
- Wo sind die Wertstoffhöfe in München? → Link: muenchen.de/notdienste
- Notfall-Link: www.muenchen.de/leben/service/notdienste/gewerblich.html

**Für Eigentümer:** [OFFEN – 10+ Fragen ausarbeiten]

---

## Über Uns (/ueber-uns/)

- **H1:** Rudolf Schäfer KG – Immobilienverwaltung mit Geschichte

### Unternehmenszahlen (Trust-Counter, alle aus CMS)
- 100+ Jahre | 23 Mitarbeitende | mehrere tausend Einheiten | 5.921 Newsletter-Abonnenten | Ø 140 Anrufe/Tag | Ø 460 E-Mails/Tag

### Zitat Martin Schäfer
> „Für meinen Vater, meine rund 20 Mitarbeitenden und mich steht die seriöse, kompetente und persönliche Beratung der Vermieterinnen und Vermieter im Vordergrund. Wir sind seit der Firmengründung 1922 durch meinen Großvater Rudolf Schäfer eine Konstante im sich schnell wandelnden Münchner Wohnungsmarkt und dennoch – oder gerade deshalb – am Puls der Zeit."

### Timeline (15 Meilensteine – vollständig)

| Jahr | Meilenstein |
|------|-------------|
| 1922 | Gründung durch Rudolf Schäfer (21 Jahre), Nordendstraße, Schwabing |
| 1930 | Erster Umzug: Neuhauser Straße 9 (heutige Fußgängerzone) |
| 1943 | Kriegsbedingt: Umzug nach Bogenhausen, Pienzenauerstraße 2 |
| 1951 | Rückkehr in die Innenstadt: Sendlinger Straße 23 |
| 1955 | Erwerb des Grundstücks Max-Joseph-Straße 8, Baubeginn |
| 1957 | Fertigstellung und Bezug des heutigen Firmensitzes |
| 1963 | Eintritt von Erich Schäfer (24 Jahre, Sohn des Gründers) |
| 1972 | 50-jähriges Jubiläum im Hotel Continental |
| 1983 | Erich Schäfer wird Komplementär |
| 2000 | Eintritt von Martin Schäfer (24 Jahre, Enkelsohn) |
| 2006 | Martin Schäfer wird Komplementär (Immobilienfachwirt DIA) |
| 2016 | ~20 Mitarbeitende, mehrere tausend Einheiten |
| 2019 | Martin Schäfer: Vorstandsvorsitzender IVD Süd (einstimmig) |
| 2022 | 100-jähriges Jubiläum, IHK-Ehrenurkunde an Martin Schäfer |

### Auszeichnungen Erich Schäfer
- Bundesverdienstkreuz am Bande
- Ehrenmedaille der IHK Oberbayern
- Goldene Ehrennadel des IVD Bundesverbandes
- Landesvorsitzender RDM Bayern (1974–1983)
- Ehrenvorsitzender des IVD-Süd

### Ämter Martin Schäfer
- Seit 2007: Vorstand IVD-Süd (Fachausschuss Verwalter)
- Seit 2010: Mitglied Vollversammlung IHK München und Oberbayern
- Seit 2019: Vorstandsvorsitzender IVD Süd
- Seit 2020: Ehrenamtlicher Verwaltungsrichter am Verwaltungsgericht

### Karriere-Sektion
Stellenangebote aus CMS (`job`-Content-Typ) | Bewerbungsformular

---

## Team (/team/)

25 Personen – vollständig dokumentiert:

| Name | Funktion | Abteilung | Seit |
|------|----------|-----------|------|
| Erich Schäfer | Kommanditist | Geschäftsleitung | 1963 |
| Martin Schäfer | Komplementär | Geschäftsleitung | 2000 |
| Monika Montenbruck | Sekretariat GL / Objektbetr. / Vermietung | – | 2008 |
| Julia Schäfer | Öffentlichkeitsarbeit & Marketing M.A. | – | 2018 |
| Peter Gemander | Leitung HV Wohnen/Technik/Vermietung | – | 2007 |
| Janina Tillich | Objektbetreuerin / Teamleitung Verwaltung | – | 2018 |
| Sonja Tafelmeier | Objektbetreuerin | – | 2020 |
| Ina Schreiber | Objektbetreuerin, Immobilienfachwirtin IHK | – | 2023 |
| Karin Breyl | Vermietung / Nebenkosten / Indexierung | – | 2009 |
| Elea Franke | Vermietung, Immobilienkauffrau | – | 2024 |
| Michael Seremek | Technik, Immobilienfachwirt | – | 2022 |
| Claudia Westner | Technische Abt., Dipl.-Ing. Bauwesen | – | 2010 |
| Thomas Schmid | Technik, Schreiner / Dipl.-Ing. Bauwesen | – | 2024 |
| Claudia Ottens | Technische Abt., Immobilienverwalterin GTW | – | 2018 |
| Yvonne Herz | Leitung Buchhaltung und HV Gewerbe/WEG | – | 2017 |
| Angelika Zeitler | Buchhaltungsexpertin (Leiterin 1999–2019) | – | 1997 |
| Susanne Rosak | Buchhaltung, Bankkauffrau | – | 2002 |
| Doris Kreuzer | Büroorganisation, Bankkontoristin | – | 1992 |
| Ute Zimmermann | Buchhaltung, Rechtsanwaltsfachangestellte | – | 1992 |
| Maximilian Langbauer | Buchhaltung & Abrechnung Nebenkosten | – | 2020 |
| Maja Siric | Buchhaltung, Wirtschaftsingenieurin | – | 2024 |
| Petra Matthiesen | Buchhaltung | – | 2017 |
| Natalja Glinska | Buchhaltung | – | 2024 |
| Jonas Ludwig | Objektverwalter, Immobilienkaufmann | – | 2025 |
| Martina Heyer | Telefonzentrale | – | 2020 |

> **[OFFEN]** Portraits für alle 25 Personen (Foto-Shooting ausstehend)

---

## Partnerschaften (/partnerschaften/)

> **[OFFEN – Inhalt vom Kunden zu liefern]**
> Welche Partner sollen auf der Website erscheinen?
> Bitte je Partner: Name, Bereich, Website, Beschreibungstext, Logo.

Die Seite wird technisch als leere Seite mit `partner`-Content-Typ angelegt und kann jederzeit befüllt werden.

---

## Kontakt (/kontakt/)

Alle Daten aus Firmen-Settings-Singleton.

### Kontaktformular-Felder
- Firma (optional)
- Vorname (Pflicht)
- Nachname (Pflicht)
- E-Mail (Pflicht)
- Straße / Nr. (optional)
- PLZ / Ort (optional)
- Nachricht (Pflicht, min. 20 Zeichen)
- Datenschutz-Checkbox (Pflicht)

### Karte
OpenStreetMap + Leaflet.js (kein Google Maps Embed)

---

## Pflichtseiten

### /impressum/
Pflichtangaben §5 TMG – aktuell vorhanden auf rudolfschaefer.de/impressum/
> **[OFFEN]** An neues Setup anpassen, rechtlich prüfen lassen

### /datenschutzerklaerung/
Aktuell vorhanden. Neu generieren je nach eingesetzten Tools (Hosting, Formular, Analytics).

### /newsletter-abbestellen/
Bestand beibehalten – Pflichtlink in Newslettern.

---

## Offene Content-Aufgaben

| # | Aufgabe | Verantwortlich | Prio |
|---|---------|----------------|------|
| 1 | Foto-Shooting: 25 Team-Portraits + Büro | Kunde | Optional |
| 2 | SEO-Texte alle Seiten nach Content-Briefings | Agentur | Kritisch |
| 3 | Stadtteiltexte: 8 Seiten à 500–700 Wörter | Agentur | Hoch |
| 4 | Partnerschaften: Inhalte liefern | Kunde | Offen |
| 5 | FAQ Eigentümer: 10+ Fragen ausarbeiten | Agentur | Hoch |
| 6 | Mietangebote-System klären + Datenmigration | Kunde + Agentur | Kritisch |
| 7 | Newsletter-System: 5.921 Abonnenten sichern | Kunde | Kritisch |
| 8 | Partner-Logos beschaffen | Agentur → Kunde | Offen |
| 9 | Stellenangebote aktuell? | Kunde | Mittel |
| 10 | EN-Übersetzung aller Seiten | Agentur | Hoch |
| 11 | Impressum + Datenschutz rechtlich aktualisieren | Rechtsanwalt | Hoch |

---

## News-Bereich – Content-Strategie

### Was nicht funktioniert hat (Fairrank-Ansatz)
Fairrank wollte folgende Themen für den News-Bereich:
Nebenkostenabrechnung, DSGVO, Schimmelprävention, Mietrecht, Kündigung/Räumung,
Heizungswartung, Mieterauswahl, Beschwerdemanagement, Hausordnung,
Objektübergabe, Handwerkermanagement, Leerstandsmanagement, Rauchmelderpflicht,
E-Mobilität, Barrierefreiheit.

**Problem:** Zu mieterorientiert, zu negativ, verfehlt Kernzielgruppe Vermieter.
Bisherige Praxis (IVD Süd-Pressemitteilungen übernehmen) reicht ebenfalls
nicht aus – eigener Content mit Mehrwert ist nötig.

### Was stattdessen gilt (Eberhard-Strategie)
News und Evergreen Content mit Eigentümer-Fokus, verzahnt mit Leistungsseiten:

**Evergreen-Cluster (Beispiele):**
- Was kostet eine Hausverwaltung in München? (Eigentümer-Frage)
- Hausverwaltung wechseln – Ablauf und typische Fehler
- WEG-Verwaltung vs. Mietverwaltung – Unterschiede für Eigentümer
- Checkliste: Die richtige Hausverwaltung in München finden
- Rechte und Pflichten einer Hausverwaltung (Eigentümer-Perspektive)

**News (aktuell, Eigentümer-relevant):**
- Grundsteuerreform München – was bedeutet das für Vermieter?
- WEG-Gesetz Änderungen – aktuell
- Münchner Immobilienmarkt – Mietpreisentwicklung
- IVD-Marktberichte (mit eigenem Mehrwert aufbereitet, nicht 1:1 übernommen)

**Tone of Voice für News:**
Alle Themen aus Eigentümer-Perspektive schreiben. Kein Angst-Content.
Kein Schreiben für Mieter. Jeder Artikel mündet in einem CTA zur
relevanten Leistungsseite.

### Technische Content-Anforderungen
- Alle News und Evergreen-Artikel: min. 600–800 Wörter
- Eigenständige WordPress-Posts (kein externes CMS)
- Kategorie-System: Hausverwaltung / Vermietung / Immobilienmarkt / WEG
- Autor: Martin Schäfer oder Rudolf Schäfer KG Redaktion
- Schema.org: NewsArticle je Artikel automatisch

---

## Custom Post Types – vollständige Struktur

### CPT 1: News (WordPress Posts nativ)

WordPress Standard-Posts werden verwendet – kein eigener CPT nötig.

**ACF-Ergänzungen:**
```
Kategorie (Taxonomy): hausverwaltung | vermietung | immobilienmarkt | weg
Zielgruppe (Checkbox): eigentümer | mieter | investoren
Featured: ja/nein (für Startseiten-Vorschau)
```

**Redakteur-Workflow:**
Neuer Artikel → Titel → Text (Gutenberg oder ACF) → Kategorie → Beitragsbild → Veröffentlichen

---

### CPT 2: Team

**Slug:** `team`
**Archiv-URL:** `/team/`

**ACF-Felder:**
```
portrait          Bild (Pflicht – Alt-Text Pflichtfeld)
name              Text (Pflicht)
funktion          Text (Pflicht)
abteilung         Select: geschaeftsleitung | verwaltung | technik |
                           buchhaltung | vermietung | sekretariat
email             E-Mail
telefon           Text (optional – nur bei Ansprechpartnern)
eintrittsjahr     Zahl
sprachen          Checkbox: deutsch | englisch (optional)
ansprechpartner   Checkbox: ja/nein (steuert Sichtbarkeit auf Leistungsseiten)
reihenfolge       Zahl (für manuelle Sortierung)
```

**Template-Logik:**
- `/team/` → alle Mitglieder, sortiert nach `reihenfolge`
- Leistungsseiten → nur Mitglieder mit `ansprechpartner = ja`
  gefiltert nach passender `abteilung`

---

### CPT 3: Immobilien

**Slug:** `immobilie`
**Kein eigenes Archiv** – Inhalte erscheinen auf bestehenden Seiten
via `WP_Query` gefiltert nach `bereiche`.

**ACF-Felder:**
```
bereiche          Checkbox (Mehrfachauswahl – Pflicht):
                    [x] verwaltung  → /hausverwaltung/referenzen/
                    [x] vermietung  → /vermietung/
                    [x] verkauf     → /verkauf/

titel             Text (Pflicht)
stadtteil         Text / Select (München-Stadtteile)
objekttyp         Select: mehrfamilienhaus | wohn-geschaeftshaus |
                          buerohaus | eigentumswohnung | investmentobjekt
status            Select: verfuegbar | vermietet | verkauft | referenz

// Vermietung-spezifisch (nur sichtbar wenn bereiche = vermietung)
zimmer            Zahl
wohnflaeche       Zahl (m²)
mietpreis         Zahl (€/Monat, Kaltmiete)
nebenkosten       Zahl (€/Monat)
verfuegbar_ab     Datum
expose_pdf        Datei

// Verkauf-spezifisch (nur sichtbar wenn bereiche = verkauf)
kaufpreis         Zahl
grundstueck       Zahl (m²)
baujahr           Zahl
verkauft          Checkbox

// Allgemein
fotos             Galerie (multiple Bilder, je mit Alt-Text Pflichtfeld)
beschreibung      Rich Text
lage_text         Text (für SEO-relevante Lagebeschreibung)
geo_lat           Zahl (für Karte)
geo_lng           Zahl (für Karte)
onoffice_id       Text (Verknüpfung mit OnOffice, falls API genutzt)
```

**Query-Beispiel Vermietungsseite:**
```php
$args = [
  'post_type'  => 'immobilie',
  'meta_query' => [[
    'key'     => 'bereiche',
    'value'   => 'vermietung',
    'compare' => 'LIKE'
  ]],
  'orderby' => 'date',
  'order'   => 'DESC'
];
```

**OnOffice-Integration:**
OnOffice hat eine OpenImmo-Schnittstelle zu WordPress.
Prüfen: Können Objekte automatisch aus OnOffice in den CPT importiert werden?
Falls ja: `onoffice_id` als Verknüpfungsfeld, Sync via WP-CLI oder Cron.
Falls nein: Manuelle Eingabe über ACF-Interface.

---

## Redaktionelle Pflege – Übersicht

| Bereich | Wer pflegt | Wie oft | Aufwand je Eintrag |
|---------|-----------|---------|-------------------|
| News | Julie Schäfer / Redaktion | 1–2×/Monat | ~30 Min. |
| Team | Perchti / Interne | Bei Personaländerung | ~10 Min. |
| Immobilien Vermietung | Karin Breyl / Elea Franke | Bei neuem Angebot | ~20 Min. |
| Immobilien Verkauf | Martin Schäfer | Bei neuem Objekt | ~20 Min. |
| Immobilien Referenzen | Perchti | Projektabschluss | ~15 Min. |
| FAQ | Julie Schäfer | Bei Bedarf | ~10 Min. |
| Testimonials | Martin Schäfer / Julie | Bei neuem Feedback | ~5 Min. |

