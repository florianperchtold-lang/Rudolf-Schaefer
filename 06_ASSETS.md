# 06_ASSETS — Asset-Inventar & Medien-Konzept
<!-- Rudolf Schäfer KG | April 2026 -->

---

## Asset-Architektur-Prinzipien

- **Kein Asset im Template oder Code** – alle Bilder/Logos über CMS-Medienfelder
- **Alt-Texte sind Pflichtfelder** – kein Upload ohne Alt-Text im CMS möglich
- **Bilder automatisch optimiert** – WebP-Konvertierung und responsive Grössen bei Upload
- **SVG-Logos inline** oder über Icon-Sprite – nie als `<img src>`
- **Schriften self-hosted** – kein CDN-Aufruf (DSGVO + Performance)
- **Naming-Konvention** einheitlich (siehe unten)

---

## Logo & Signet

> **[OFFEN – Logo-Dateien vom Kunden anfordern]**

### Benötigte Varianten

| Datei | Format | Verwendung | Status |
|-------|--------|------------|--------|
| `logo-rudolf-schaefer-kg-quer.svg` | SVG | Header (hell) | ⚠ anfordern |
| `logo-rudolf-schaefer-kg-quer-weiss.svg` | SVG | Header (dunkel), Footer | ⚠ anfordern |
| `logo-rudolf-schaefer-kg-hoch.svg` | SVG | Mobile, Karten | ⚠ anfordern |
| `logo-rudolf-schaefer-kg-hoch-weiss.svg` | SVG | Dark-Sections | ⚠ anfordern |
| `favicon.svg` | SVG | Browser Tab | ⚠ erstellen |
| `favicon-512.png` | PNG | PWA, OG-Fallback | ⚠ erstellen |
| `apple-touch-icon.png` | PNG 180px | iOS Home Screen | ⚠ erstellen |
| `og-image-default.jpg` | JPG 1200×630 | Open Graph Standard | ⚠ erstellen |

---

## Foto-Anforderungen

### Team-Portraits (Shooting ausstehend – Kritisch)

| Motiv | Verwendung | Format |
|-------|------------|--------|
| Portrait je Teammitglied (25 Personen) | Team-Seite, Ansprechpartner-Sektionen | Hochformat 4:5 |
| Martin Schäfer – Profilbild gross | Hero Über Uns, Google Business, Schema | Quadrat 1:1 |
| Erich Schäfer – Profilbild | Über Uns, Geschichte | Quadrat 1:1 |
| Team-Gruppenfoto | Über Uns, Startseite (optional) | Querformat 16:9 |

**Stil:** Seriös, professionell, natürliches Licht. Kleidung: Dunkel (Anzug). Kein Stock-Foto-Feeling. Hintergrund: Büroumgebung.

### Büro & Gebäude

| Motiv | Verwendung | Status |
|-------|------------|--------|
| Aussenansicht Max-Joseph-Str. 8 | Über Uns, Kontakt, Google Business | ✓ vorhanden (aus CD-Präsentation) |
| Isar-Panorama München | Allgemein | ✓ vorhanden (aus CD-Präsentation) |
| Markus Wilde in Robe | – | ✗ falsches Projekt, nicht verwenden |
| Empfang / Eingangsbereich | Kontaktseite | ⚠ Shooting nötig |
| Besprechungsraum | Über Uns | ⚠ Shooting nötig |
| Büroatmosphäre allgemein | Startseite Hero | ⚠ Shooting nötig |

### Referenz-Objekte / Stadtteile

Für 11 Referenzobjekte und 8 Stadtteil-Seiten: repräsentative Fotos der jeweiligen Münchner Stadtteile. Eigene Fotos bevorzugt, Stock nur als Fallback.

---

## Icons

**Bibliothek:** Lucide Icons (Open Source, MIT) – https://lucide.dev
**Format:** SVG Sprite – nie Font-Icon
**Farbe:** Via `color` CSS – nie hardcodiert in SVG

| Leistung/Bereich | Icon-Name (Lucide) |
|------------------|--------------------|
| Hausverwaltung | `building-2` |
| WEG-Verwaltung | `users` |
| Gewerbeverwaltung | `briefcase` |
| Vermietung | `key` |
| Verkauf | `trending-up` |
| Immobilienbewertung | `calculator` |
| Buchhaltung | `file-spreadsheet` |
| Technik | `wrench` |
| App | `smartphone` |
| Kontakt / Telefon | `phone` |
| Adresse | `map-pin` |
| E-Mail | `mail` |
| Öffnungszeiten | `clock` |
| Schadensmeldung | `alert-triangle` |
| Dokumente | `folder` |
| Suche | `search` |
| Schliessen | `x` |
| Menü | `menu` |
| Pfeil rechts | `arrow-right` |
| Pfeil runter | `chevron-down` |

---

## Schriften (self-hosted)

| Schrift | Gewichte | Subset | Download |
|---------|----------|--------|----------|
| Playfair Display | 300, 400, 600 | latin, latin-ext | google-webfonts-helper.herokuapp.com |
| Inter | 400, 500, 600 | latin, latin-ext | google-webfonts-helper.herokuapp.com |

```
/assets/fonts/
├── playfair/
│   ├── playfair-display-v37-latin-300.woff2
│   ├── playfair-display-v37-latin-regular.woff2
│   └── playfair-display-v37-latin-600.woff2
└── inter/
    ├── inter-v13-latin-regular.woff2
    ├── inter-v13-latin-500.woff2
    └── inter-v13-latin-600.woff2
```

> Nur benötigte Gewichte laden. Kein Aufruf an fonts.googleapis.com.

---

## Naming-Konventionen

**Schema:** `[kategorie]-[beschreibung]-[variante].[format]`

```
Logos:         logo-rudolf-schaefer-kg-quer-weiss.svg
Team:          team-martin-schaefer-portrait.jpg
Objekte:       objekt-schwabing-mehrfamilienhaus-01.jpg
Stadtteile:    stadtteil-schwabing-muenchen.jpg
Icons:         icon-hausverwaltung.svg
OG-Images:     og-hausverwaltung-muenchen.jpg
Schriften:     inter-v13-latin-regular.woff2

Verboten:      IMG_1234.jpg | foto (1).jpg | Bild-NEU.png
```

---

## Bildformate & Responsive

| Verwendung | Ausgabeformat | Grössen (srcset) |
|------------|---------------|-----------------|
| Hero-Bilder | WebP + JPG | 2400w, 1600w, 1200w, 800w |
| Team-Portraits | WebP + JPG | 800w, 600w, 400w |
| Referenz-Fotos | WebP + JPG | 1200w, 800w, 600w |
| Logos | SVG | Skaliert via CSS |
| Icons | SVG Sprite | Inline, via CSS |
| OG-Images | JPG (fix) | 1200×630px |
| Favicon | SVG + PNG 512 + ICO 32 | Mehrere Grössen |

---

## Ordnerstruktur Assets

```
/assets/
├── fonts/
│   ├── playfair/
│   └── inter/
├── icons/
│   └── sprite.svg          ← Alle Lucide Icons als SVG Sprite
└── logo/
    ├── logo-...-quer.svg
    ├── logo-...-quer-weiss.svg
    ├── logo-...-hoch.svg
    ├── logo-...-hoch-weiss.svg
    ├── favicon.svg
    ├── favicon-512.png
    └── apple-touch-icon.png
```

> Fotos und Dokumente liegen **nicht** im Code-Repository – sie werden über das CMS-Medienmanagement verwaltet.

---

## Offene Asset-Aufgaben

| # | Aufgabe | Prio | Timing |
|---|---------|------|--------|
| 1 | Logo SVG-Varianten vom Kunden beschaffen | Kritisch | Sofort |
| 2 | Favicon + Apple Touch Icon + OG-Default erstellen | Kritisch | Design-Phase |
| 3 | Foto-Shooting terminieren (25 Portraits + Büro) | Kritisch | Design-Phase |
| 4 | Schriften herunterladen + @font-face einrichten | Hoch | Tech-Setup |
| 5 | Lucide Icon Sprite generieren | Hoch | Entwicklung |
| 6 | Partner-Logos beschaffen | Offen | Wenn Partnerinhalte vorliegen |
| 7 | Bestehende CD-Fotos in WebP konvertieren | Mittel | Content-Phase |
| 8 | OG-Images je Hauptseite erstellen (1200×630) | Mittel | Vor Launch |
