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

> Konkrete Schriften werden in der Design-Phase festgelegt (abhängig vom Corporate Design).

**Prinzip:** Alle Schriften self-hosted, kein Aufruf an fonts.googleapis.com (DSGVO + Performance).

| Rolle | Charakter | CSS-Variable | Gewichte (ca.) |
|-------|-----------|--------------|----------------|
| Display | Serifen-Schrift | `--font-display` | 300, 400, (600) |
| Body | Sans-Serif | `--font-body` | 400, 500, 600 |

```
/assets/fonts/
├── display/    ← Serifen-Schrift (TBD)
└── body/       ← Sans-Serif (TBD)
```

> Format: woff2 (primär) + woff (Fallback). Subset: latin, latin-ext. Nur benötigte Gewichte laden.

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
Schriften:     [schriftname]-latin-regular.woff2

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

## Skyline-Grafik München (SVG)

Grafisches Kernelement der Website – Outline-Silhouette der Münchner Skyline (Frauenkirche, Olympiaturm, Theatinerkirche, Maximilianeum u.a.).

**Produktionsstrategie: Iterativ**

| Phase | Vorgehen | Status |
|-------|----------|--------|
| **1. Sofortlösung** | Öffentliche Quellen (Wikimedia Commons, OpenStreetMap-Derivate, freie SVG-Repositories) – lizenzrechtlich prüfen, ggf. CC0 oder Public Domain | ⏳ Recherche |
| **2. Anpassung** | Bestehende SVG manuell nachbearbeiten – Stilisierung, Reduktion auf Linien (`stroke only`), Anpassung an das Farbsystem | ⏳ Entwicklung |
| **3. Finalisierung** | Eigene, projektspezifische Illustration – entweder intern oder beauftragt | ⏳ Produktion |

**Technische Anforderungen:**
- Format: SVG, inline-fähig
- Stil: primär als Linie (`stroke`), flächige Varianten möglich – Entscheidung in Produktion
- Farbe: via CSS-Variable (kein hardcodiertes Hex im SVG)
- Responsive: skaliert via `viewBox`, keine fixen Pixelbreiten
- Dateiname: `grafik-muenchen-skyline-outline.svg`

> Entscheidung über finale Qualität und Herkunft fällt in der Produktionsphase. Start mit öffentlichen Quellen ist ausdrücklich geplant.

---

## Offene Asset-Aufgaben

| # | Aufgabe | Prio | Timing |
|---|---------|------|--------|
| 1 | Logo SVG-Varianten vom Kunden beschaffen | Kritisch | Sofort |
| 2 | Favicon + Apple Touch Icon + OG-Default erstellen | Kritisch | Design-Phase |
| 3 | Foto-Shooting terminieren (25 Portraits + Büro) | Optional | Design-Phase |
| 4 | Schriften herunterladen + @font-face einrichten | Hoch | Tech-Setup |
| 5 | Lucide Icon Sprite generieren | Hoch | Entwicklung |
| 6 | Skyline-SVG recherchieren (öffentliche Quellen) | Hoch | Design-Phase |
| 7 | Skyline-SVG anpassen und stilisieren | Mittel | Entwicklung |
| 8 | Partner-Logos beschaffen | Offen | Wenn Partnerinhalte vorliegen |
| 9 | Bestehende CD-Fotos in WebP konvertieren | Mittel | Content-Phase |
| 10 | OG-Images je Hauptseite erstellen (1200×630) | Mittel | Vor Launch |
