# 07_ARCHITEKTUR — Website-Architektur
<!-- Rudolf Schäfer KG | April 2026 -->
<!-- WordPress + Bricks + ACF + Claude Code + Gemini + Copilot -->

---

## Kernprinzip

> **Kein Hardcoding. Alle Inhalte über CMS/DB. Kleine, isolierte Komponenten.**

Drei konkrete Probleme die diese Architektur löst:

1. **Kleine Änderungen, grosser Aufwand:** Wenn Inhalte im Template stehen, muss bei jeder Textänderung ein Entwickler ran – der gesamte Code wird durchlaufen, Tokens werden verbraucht, Fehlerquellen entstehen.
2. **Duplikate:** Telefonnummer an 12 Stellen → wird eine geändert, werden 11 vergessen.
3. **Seiteneffekte:** Seitenspezifisches CSS kann unbeabsichtigt alle anderen Seiten treffen.

---

## Drei-Schichten-Architektur

```
┌─────────────────────────────────────────────────────────────┐
│  SCHICHT 1 – CMS/DB                                         │
│  Alle Texte, Bilder, Zahlen, Links, Konfiguration           │
│  → Redakteur ändert, KEIN Entwickler nötig                  │
├─────────────────────────────────────────────────────────────┤
│  SCHICHT 2 – Komponenten                                    │
│  HTML-Struktur + CSS-Klassen (keine Inhalte drin)           │
│  → Entwickler ändert nur bei strukturellen Anpassungen      │
├─────────────────────────────────────────────────────────────┤
│  SCHICHT 3 – Design-System                                  │
│  CSS Custom Properties: Farben, Spacing, Typo               │
│  → Eine Datei, wirkt global, sehr selten geändert           │
└─────────────────────────────────────────────────────────────┘
```

**Faustregel:** Schicht 1 ändern = kein Code. Schicht 2 ändern = nur betroffene Komponente. Schicht 3 ändern = wirkt sauber überall.

---

## Ordnerstruktur

```
rudolfschaefer-website/
│
├── cms/
│   ├── content-types/          ← 1 JSON-Datei je Content-Typ
│   │   ├── page.json
│   │   ├── mietobjekt.json
│   │   ├── teammitglied.json
│   │   ├── faq.json
│   │   ├── news.json
│   │   ├── referenz.json
│   │   ├── testimonial.json
│   │   ├── meilenstein.json
│   │   ├── partner.json
│   │   ├── stadtteil.json
│   │   ├── job.json
│   │   └── settings.json       ← Singleton
│   └── blocks/                 ← 1 JSON je Block-Typ
│
├── templates/
│   ├── base.html               ← head, header, footer, Schema.org
│   ├── pages/
│   │   ├── default.html        ← Standard-Seitentemplate
│   │   ├── mietobjekt.html
│   │   └── stadtteil.html
│   └── blocks/                 ← 1 HTML je Block-Typ, max. 80 Zeilen
│       ├── hero-section.html
│       ├── leistungs-akkordeon.html
│       ├── referenz-grid.html
│       ├── faq-akkordeon.html
│       ├── team-grid.html
│       ├── testimonial-slider.html
│       ├── trust-counter.html
│       ├── app-teaser.html
│       ├── news-grid.html
│       ├── kontakt-block.html
│       ├── timeline-block.html
│       ├── partner-grid.html
│       └── stadtteil-intro.html
│
├── css/
│   ├── design-tokens.css       ← EINZIGE Quelle für alle Farbwerte/Spacing
│   ├── base.css                ← Reset, Body, Typografie-Basis
│   ├── layout/
│   │   ├── grid.css
│   │   └── section.css
│   ├── components/             ← 1 Datei je Komponente, MAX. 100 Zeilen
│   │   ├── btn.css
│   │   ├── hero.css
│   │   ├── card.css
│   │   ├── akkordeon.css
│   │   ├── nav.css
│   │   ├── footer.css
│   │   ├── form.css
│   │   └── ...
│   └── utilities.css
│
├── js/
│   ├── main.js                 ← Nur Imports, MAX. 50 Zeilen
│   ├── modules/                ← 1 Datei je Feature, MAX. 80 Zeilen
│   │   ├── akkordeon.js
│   │   ├── sticky-header.js
│   │   ├── lazy-load.js
│   │   ├── counter-animation.js
│   │   ├── filter.js
│   │   ├── map.js
│   │   └── form.js
│   └── utils/
│       ├── dom.js
│       └── a11y.js
│
├── assets/
│   ├── fonts/                  ← Self-hosted Schriften
│   ├── icons/
│   │   └── sprite.svg          ← SVG Sprite alle Icons
│   └── logo/                   ← Alle Logo-Varianten
│
├── .env.example
├── .gitignore
└── README.md
```

---

## Datei-Grössen-Limits

| Dateityp | Max. Zeilen | Was tun wenn überschritten |
|----------|-------------|---------------------------|
| Template / Block HTML | 80 | Teil-Blöcke als Includes auslagern |
| Komponente CSS | 100 | Modifier in eigene Datei |
| Modul JS | 80 | Helper in utils/ auslagern |
| design-tokens.css | 120 | Kategorie-Dateien aufteilen |
| main.js | 50 | Immer nur Imports |

> **Warum?** Kleinere Dateien = Claude Code / Gemini sehen nur relevanten Scope = weniger Tokens, weniger Fehlerquellen, schnellere Iteration.

---

## Single Source of Truth

### Settings-Singleton
Alle globalen Firmendaten **einmal** – Footer, Kontaktseite, Schema.org ziehen alle daraus:

```
settings.firmenname      → Im Footer, in Schema.org, im Impressum
settings.telefon         → Im Footer, auf Kontaktseite, in Schema.org
settings.oeffnungszeiten → Auf Kontaktseite, im GBP-Schema, in FAQ
settings.geo_lat/lng     → In Schema.org, in Leaflet.js Karte
```

**Regel:** Kein Wert steht an mehr als einer Stelle.

### Flexibles Block-System
Alle Seiten nutzen `blocks[]` – keine feste Seitenstruktur:

```
// Beispiel Hausverwaltungs-Seite
blocks: [
  { type: 'leistungs-akkordeon', ... },
  { type: 'referenz-grid',       filter: 'hausverwaltung' },
  { type: 'testimonial-slider',  ... },
  { type: 'faq-akkordeon',       kategorie: 'hausverwaltung' },
  { type: 'kontakt-cta',         ... }
]

// Template – sprachagnostisch, inhaltsneutral:
{% for block in page.blocks %}
  {% include 'blocks/' + block.type + '.html' with block %}
{% endfor %}
```

Neue Sektion = neuer CMS-Eintrag. Kein neuer Code.

---

## Die 5 Gesetze sauberer Komponenten

**1 – Eine Aufgabe**
Eine `hero-section` rendert einen Hero. Keine Businesslogik, keine DB-Abfragen, keine SEO-Entscheidungen.

**2 – Kein Hardcoding**
Kein Text, keine URL, keine Zahl, keine Farbe im Komponenten-Code. Alles als Parameter von aussen.

**3 – Kein Seitenkontext**
Die Komponente weiss nicht auf welcher Seite sie ist. Sie funktioniert mit den übergebenen Daten – überall gleich.

**4 – CSS-Isolation**
Styles einer Komponente betreffen nur diese. Ausschliesslich `var(--color-*)` und `var(--space-*)` – kein Hex, keine magic numbers.

**5 – Deklarativ**
Template beschreibt WAS gerendert wird. Businesslogik (Sortierung, Filterung) gehört in den CMS-Layer.

---

## Richtig vs. Falsch

```html
<!-- ✗ FALSCH – hardcodiert, seitenspezifisch -->
<div class="hero">
  <h1>Hausverwaltung München seit 1922</h1>
  <a href="/kontakt/">Jetzt kontaktieren</a>
</div>

<!-- ✓ RICHTIG – alle Daten als Parameter -->
<div class="hero">
  <h1>{{ block.h1 }}</h1>
  <a href="{{ block.cta_url }}">{{ block.cta_text }}</a>
</div>
```

```css
/* ✗ FALSCH – Hex-Wert in Komponente */
.btn { background: #B4001E; }

/* ✓ RICHTIG – Design-Token */
.btn { background: var(--color-primary); }
```

```
/* ✗ FALSCH – Seiten-CSS */
/css/pages/hausverwaltung.css   ← existiert nicht

/* ✓ RICHTIG – Komponenten-CSS */
/css/components/hero.css
/css/components/btn.css
```

---

## Schema.org – automatisch aus CMS

Kein manuelles Markup. Alle Schema-Templates werden aus CMS-Feldern befüllt:

```html
<!-- base.html – einmal eingebunden, überall gültig -->
<script type="application/ld+json">
{
  "@type": ["RealEstateAgent", "LocalBusiness"],
  "name": "{{ settings.firmenname }}",
  "telephone": "{{ settings.telefon }}",
  "foundingDate": "{{ settings.gruendungsjahr }}",
  "address": {
    "streetAddress": "{{ settings.strasse }}",
    "addressLocality": "{{ settings.ort }}",
    "postalCode": "{{ settings.plz }}"
  }
}
</script>
```

---

## KI-Coding-Workflow

### Tool-Zuständigkeiten

| Tool | Primäre Aufgaben |
|------|-----------------|
| **Claude Code** | Komponenten-Architektur, Schema-Markup, Redirect-Map, Code-Review, komplexe Logik, DSGVO-Checks |
| **Google Gemini** | SEO-Texte generieren/prüfen, Alt-Texte, FAQ-Content, DE→EN Übersetzung |
| **GitHub Copilot** | IDE-Autocomplete, Boilerplate, repetitive Patterns beschleunigen |

### Effizienz-Prinzip

```
// ✗ INEFFIZIENT – ganzer Seiten-Code im Kontext
"Hier ist meine komplette Seite (800 Zeilen). Ändere den Button-Text."

// ✓ EFFIZIENT – isolierte Komponente
"Hier ist /css/components/btn.css (20 Zeilen).
Füge einen Modifier .btn--outline hinzu."

// ✓ EFFIZIENT – Inhalt via CMS, kein Code
"Button-Text ändern" → CMS-Eintrag bearbeiten, fertig.
```

---

## Mehrsprachigkeit (DE/EN)

```
DE: /hausverwaltung/          ← Default, kein Präfix
EN: /en/property-management/

Templates: sprach-agnostisch
  <html lang="{{ page.sprache }}">
  <link rel="alternate" hreflang="de" href="{{ page.url_de }}">
  <link rel="alternate" hreflang="en" href="{{ page.url_en }}">
  <link rel="alternate" hreflang="x-default" href="{{ page.url_de }}">
```

---

## Architektur-Checkliste (vor Go-Live)

### Kein Hardcoding
- [ ] `grep -r 'Rudolf Schäfer' templates/` → 0 Treffer im Content (Settings-Referenzen OK)
- [ ] `grep -r '089' templates/` → 0 Treffer
- [ ] `grep -r '#[0-9A-Fa-f]' css/components/` → 0 Treffer
- [ ] Kein `<img src="/...">` im Template ohne CMS-Feld

### Komponenten
- [ ] Alle Dateien unter Zeilenlimit
- [ ] Kein `/css/pages/` Ordner vorhanden
- [ ] Icon-Sprite komplett
- [ ] Schriften self-hosted, kein fonts.googleapis.com im Network-Tab

### CMS
- [ ] Settings-Singleton vollständig befüllt
- [ ] Alt-Text Pflichtfeld aktiv (Upload ohne Alt = Validierungsfehler)
- [ ] DE + EN Content-Items vorhanden
- [ ] Schema.org wird automatisch generiert, nicht manuell gepflegt
- [ ] hreflang-URLs automatisch aus CMS-Relationen

---

## Token-effiziente Entwicklung mit Claude Code + Bricks Builder + WordPress/ACF

> Dieses Kapitel beschreibt konkret wie die Zusammenarbeit zwischen KI-Tools
> und dem CMS/Builder so aufgesetzt wird, dass Änderungen minimal invasiv sind.
> Das Ziel: Claude Code sieht bei jeder Aufgabe nur die relevanten Dateien –
> nie die gesamte Seite.

---

### Das Grundprinzip: Scope-Kontrolle

**Problem ohne saubere Architektur:**
Eine Änderung an einem FAQ-Text zwingt Claude Code, 800 Zeilen zu laden,
zu parsen, zu verstehen – und dann 800 Zeilen neu zu schreiben.
Fehlerrisiko hoch, Token-Verbrauch enorm, Entwicklung langsam.

**Lösung: Scope = Datei**
Jede Aufgabe hat genau eine verantwortliche Datei. Claude Code bekommt
immer nur diese eine Datei. Alles andere ist unsichtbar.

| Aufgabe | Schlechte Architektur | Gute Architektur |
|---------|----------------------|------------------|
| FAQ-Text ändern | ~2.400 Tokens (ganze Seite) | 0 Tokens (CMS-Eintrag) |
| Button-Farbe ändern | ~1.800 Tokens (CSS suchen) | ~80 Tokens (design-tokens.css) |
| Telefonnummer updaten | ~3.200 Tokens (12 Stellen) | ~30 Tokens (settings.json) |
| Neue Stadtteil-Seite | ~4.000 Tokens (neu schreiben) | ~150 Tokens (CMS-Eintrag, Template existiert) |
| Akkordeon-Animation tweaken | ~800 Tokens (JS durchsuchen) | ~200 Tokens (akkordeon.js, 60 Zeilen) |

---

### Konkret: Bricks Builder (Visual Composer Studio)

Bricks Builder arbeitet mit Elementen, Templates und Theme-Dateien.
Die folgenden Regeln stellen sicher, dass der Output sauber und
KI-freundlich bleibt.

#### Regel 1 – Eigene Element-Datei je Block-Typ

In Bricks Builder wird jeder wiederverwendbare Block als **eigenes Custom Element**
registriert – nicht als Teil einer langen Theme-Datei.

```
/vc-studio/elements/
├── hero-section.php          ← nur Hero
├── leistungs-akkordeon.php   ← nur Akkordeon
├── faq-akkordeon.php         ← nur FAQ
├── team-grid.php             ← nur Team
├── trust-counter.php         ← nur Counter
├── mietobjekt-card.php       ← nur Objekt-Karte
├── referenz-grid.php         ← nur Referenzen
├── app-teaser.php            ← nur App
├── testimonial-slider.php    ← nur Testimonials
├── news-grid.php             ← nur News
└── partner-grid.php          ← nur Partner
```

**Warum:** Claude Code bekommt den Auftrag
`"Ändere faq-akkordeon.php"` – und sieht nur diese 50 Zeilen.
Nicht die gesamte Seitenstruktur.

#### Regel 2 – Params vs. Hardcoding in Bricks Builder

Jedes Element deklariert seine Inhalte als **Params** – nicht hardcodiert.

```php
// ✗ FALSCH – hardcodiert im Element
function render() {
    return '<h2>Unsere Leistungen</h2>
            <p>Seit 1922 verwalten wir...</p>';
}

// ✓ RICHTIG – Params aus Bricks Builder Builder
vc_map([
    'name'   => 'Leistungs-Akkordeon',
    'params' => [
        ['param_name' => 'titel',    'type' => 'textfield'],
        ['param_name' => 'eintraege','type' => 'param_group'],
        ['param_name' => 'cta_text', 'type' => 'textfield'],
        ['param_name' => 'cta_url',  'type' => 'vc_link'],
    ]
]);

function render($atts) {
    extract(shortcode_atts(['titel' => '', 'cta_text' => ''], $atts));
    return "<h2>{$titel}</h2>...";
}
```

**Warum:** Inhalte werden im VC Builder eingegeben – nie im Code.
Ändert sich ein CTA-Text, ist das eine Builder-Aktion, kein Code-Edit.

#### Regel 3 – CSS aus Bricks Builder raus, in eigene Dateien

Bricks Builder neigt dazu, inline-CSS zu generieren. Das verhindert saubere
Token-Effizienz. Konfiguration in Bricks Builder:

```
Bricks Builder → Settings → General → Load CSS → "External file only"
```

Dann gilt:

```
/css/
├── design-tokens.css        ← Claude Code ändert hier Farben/Spacing
├── components/
│   ├── btn.css              ← Claude Code ändert nur Buttons
│   ├── hero.css             ← Claude Code ändert nur Hero
│   ├── akkordeon.css        ← Claude Code ändert nur Akkordeon
│   └── ...
```

**Kein** `style="color: #B4001E"` im PHP/HTML-Output von Bricks Builder Elementen.
Ausschliesslich `class="btn btn--primary"` – die Klasse kennt ihre Farbe
aus `btn.css` via `var(--color-primary)`.

#### Regel 4 – Bricks Builder Seiten-Templates minimal halten

Das Seiten-Template in Bricks Builder ist nur ein Rahmen:

```php
// page-hausverwaltung.php – ~30 Zeilen, kein Inhalt
get_header();
while (have_posts()) {
    the_post();
    echo do_shortcode(get_the_content()); // VC Builder rendert Blöcke
}
get_footer();
```

**Kein Inhalt im Template.** Alle Inhalte kommen aus den VC Builder-Blöcken.

#### Workflow mit Claude Code + Bricks Builder

```
Aufgabe: "Akkordeon soll beim Öffnen sanfter animieren"

Claude Code bekommt NUR:
  /css/components/akkordeon.css   (30 Zeilen)

Claude Code ändert:
  transition: max-height 200ms ease
  → transition: max-height 350ms cubic-bezier(0.4, 0, 0.2, 1)

Fertig. Keine andere Datei wurde gelesen oder geändert.
```

---

### Konkret: WordPress CMS

WordPress/ACF trennt Content-Typen, Templates und Assets sauber –
wenn es von Anfang an richtig konfiguriert wird.

#### Regel 1 – Block-Templates als eigenständige Dateien

In WordPress/ACF werden Block-Templates im `/templates/blocks/` Verzeichnis
als **einzelne Dateien** verwaltet. Jede Datei = ein Block-Typ.

```
/templates/blocks/
├── hero-section.html         ← max. 60 Zeilen
├── leistungs-akkordeon.html  ← max. 50 Zeilen
├── faq-akkordeon.html        ← max. 45 Zeilen
├── team-grid.html            ← max. 40 Zeilen
├── trust-counter.html        ← max. 30 Zeilen
├── mietobjekt-card.html      ← max. 35 Zeilen
├── referenz-grid.html        ← max. 40 Zeilen
├── app-teaser.html           ← max. 45 Zeilen
├── testimonial-slider.html   ← max. 35 Zeilen
├── news-grid.html            ← max. 40 Zeilen
└── partner-grid.html         ← max. 35 Zeilen
```

**Wichtig:** WordPress/ACF's Block-Rendering-System einbinden:

```html
<!-- base.html – Seiten-Template, ~25 Zeilen, kein Inhalt -->
{% extends "base.html" %}
{% block content %}
  {% for block in page.blocks %}
    {% include "blocks/" + block.type + ".html" with block %}
  {% endfor %}
{% endblock %}
```

Neue Sektion = neuer Block im CMS. Kein neuer Code. Claude Code wird
nicht gebraucht.

#### Regel 2 – Content-Typen mit strikten Feldgrenzen

Jeder WordPress/ACF Content-Typ hat exakt die Felder die er braucht –
nicht mehr. Kein "misc"-Feld, kein Sammelsurium.

```yaml
# /cms/content-types/faq.json
{
  "name": "faq",
  "fields": [
    {"name": "frage",     "type": "text",     "required": true},
    {"name": "antwort",   "type": "richtext",  "required": true},
    {"name": "kategorie", "type": "select",    "options": ["mieter","eigentuemer","allgemein"]},
    {"name": "seite",     "type": "multiref",  "ref": "page"}
  ]
}
```

**Warum:** Claude Code kann den Content-Typ als Referenz bekommen
(~15 Zeilen JSON) wenn es ein neues Template-Feature baut –
ohne die gesamte CMS-Konfiguration zu laden.

#### Regel 3 – Settings-Singleton als einzige globale Datenquelle

Alle Firmendaten in **einem** WordPress/ACF Singleton. Kein weiterer Ort
für Telefonnummer, Adresse oder App-URL.

```
settings.telefon      → Footer, Kontaktseite, Schema.org
settings.email        → alle Formulare, Footer
settings.gruendungsjahr → Trust-Counter, Schema.org, Timeline
settings.app_ios_url  → App-Teaser, Service-Seite
```

Änderung der Telefonnummer: Ein Feld im CMS. Null Code. Null Tokens.

#### Regel 4 – Schema.org automatisch aus WordPress/ACF-Feldern

Schema-Templates sind eigene Dateien in `/templates/schema/`:

```
/templates/schema/
├── local-business.html    ← zieht aus settings.*
├── faq-page.html          ← zieht aus faq-ct loop
├── person.html            ← zieht aus teammitglied-ct
├── news-article.html      ← zieht aus news-ct
└── breadcrumb.html        ← auto aus Seitenhierarchie
```

Claude Code, das an Schema-Markup arbeitet, bekommt nur die relevante
Schema-Template-Datei (~20 Zeilen) – nicht die Seite selbst.

#### Regel 5 – WordPress/ACF Asset Pipeline

```
/assets/                   ← Statische Assets (Fonts, Icons, Logo)
                              Liegen im Git-Repo, werden nie vom CMS
                              verwaltet. Claude Code kann sie direkt
                              öffnen ohne CMS-Kontext.

CMS Medienmanager          ← Alle Fotos, PDFs, dynamische Bilder.
                              Werden nie in Git committet.
                              Claude Code greift nie direkt auf
                              Medien-Uploads zu.
```

#### Workflow mit Claude Code + WordPress/ACF

```
Aufgabe: "Trust-Counter soll auch Newsletter-Zahl zeigen"

Schritt 1 – CMS (kein Code):
  settings.json → Feld "newsletter_abonnenten": 5921 hinzufügen

Schritt 2 – Claude Code bekommt NUR:
  /templates/blocks/trust-counter.html  (28 Zeilen)

Claude Code fügt hinzu:
  <div class="counter">
    <span data-target="{{ settings.newsletter_abonnenten }}">0</span>
    <label>Newsletter</label>
  </div>

Fertig. Keine andere Datei wurde angefasst.
```

---

### Der Claude-Code-Auftrag: So formulieren

Der grösste Hebel für Token-Effizienz ist die **Formulierung des Auftrags**.

```
// ✗ INEFFIZIENT – ganzer Kontext, vage
"Schau dir die Hausverwaltungsseite an und verbessere das FAQ."

// ✓ EFFIZIENT – enger Scope, präzise
"Hier ist /templates/blocks/faq-akkordeon.html (42 Zeilen).
Füge dem äussersten <div> das Attribut data-schema='faq' hinzu."

// ✓ EFFIZIENT – Design-Token, minimal
"Hier ist /css/design-tokens.css.
Ändere --transition von 200ms auf 300ms ease."

// ✓ EFFIZIENT – neue Komponente mit Muster
"Erstelle /templates/blocks/stadtteil-intro.html nach dem Muster
von /templates/blocks/referenz-grid.html (40 Zeilen).
Felder: name, seo_text, referenzen[]"

// ✓ EFFIZIENT – CMS-Feld, kein Code
"FAQ 'Wie hoch ist die Kaution?' → Antwort in WordPress/ACF
aktualisieren. Kein Code nötig."
```

---

### Datei-Grössen-Limits (verbindlich)

Wenn eine Datei das Limit überschreitet, ist das ein Signal dass
sie zu viel tut – nicht ein Signal zum Ignorieren.

| Dateityp | Limit | Was tun bei Überschreitung |
|----------|-------|---------------------------|
| Block-Template (HTML) | 60 Zeilen | Teil-Includes extrahieren |
| Komponente CSS | 80 Zeilen | Modifier auslagern |
| JS-Modul | 80 Zeilen | Helper in `utils/` |
| design-tokens.css | 100 Zeilen | Kategorie-Dateien (colors.css, spacing.css) |
| Content-Typ JSON | 50 Zeilen | Feldgruppen aufteilen |
| Schema-Template | 40 Zeilen | Teil-Templates |
| Seiten-Template | 30 Zeilen | Nur Rahmen, alle Inhalte in Blöcken |

---

### Checkliste: Token-effizientes Setup (vor Entwicklungsbeginn)

**Bricks Builder**
- [ ] Custom Elements als einzelne PHP-Dateien registriert (1 Datei = 1 Block)
- [ ] Alle Inhalte als Params deklariert, nichts hardcodiert
- [ ] CSS External Only aktiviert – kein inline-Style Output
- [ ] Seiten-Templates auf ~30 Zeilen reduziert

**WordPress**
- [ ] Block-Templates unter `/templates/blocks/` als Einzeldateien
- [ ] Settings-Singleton vollständig als einzige Quelle für Firmendaten
- [ ] Schema-Templates als eigene Dateien unter `/templates/schema/`
- [ ] Asset-Trennung: Git (statisch) vs. CMS-Medien (dynamisch)
- [ ] Content-Typ-Felder strikt definiert – kein "misc"-Catch-all

**Allgemein**
- [ ] design-tokens.css existiert und ist die EINZIGE Datei mit Hex-Werten
- [ ] Kein `style=""` Attribut in Template-Dateien
- [ ] Kein Inhalt in Template-Dateien (nur Struktur + `{{ variablen }}`)
- [ ] Alle Dateien unter ihrem Limit
- [ ] Claude Code Aufträge enthalten immer den Dateinamen + Zeilenzahl

---

## Bild-Workflow: Automatisierte Verarbeitung & WordPress-Import

### Übersicht

200 Bilder aus der bestehenden WordPress-Mediathek (+ Originale) werden
in einem einmaligen vollautomatisierten Prozess aufbereitet:
konvertiert, umbenannt, mit KI-Metadaten versehen und in die neue
WordPress-Instanz importiert.

```
/bilder-original/           ← Originale einmalig hier ablegen
├── team/
├── objekte/
│   ├── schwabing/
│   ├── maxvorstadt/
│   └── ...
├── buero/
└── allgemein/

        ↓ Node.js Skript (einmalig)

/bilder-output/             ← Fertige Bilder für WordPress-Import
├── team-martin-schaefer-portrait-400w.avif
├── team-martin-schaefer-portrait-400w.webp
├── team-martin-schaefer-portrait-400w.jpg
├── objekte-schwabing-mfh-800w.avif
├── ...
└── metadata.json           ← Alt-Texte, Titel, Beschreibungen
```

---

### Schritt 1 – Ordnerstruktur & Benennung

Der Ordnername liefert automatisch den SEO-Kontext für Dateiname und Alt-Text.

**Namenskonvention:**
```
[ordner]-[beschreibung]-[breite]w.[format]

Beispiele:
  team-martin-schaefer-komplementaer-400w.avif
  objekte-schwabing-mehrfamilienhaus-800w.webp
  buero-max-joseph-strasse-aussenansicht-1200w.jpg
  allgemein-muenchen-skyline-isar-1600w.avif
```

**Automatische Umbenennung per Skript:**
Der Dateiname wird aus Ordner + ursprünglichem Dateinamen generiert,
bereinigt (Umlaute → ae/oe/ue, Leerzeichen → Bindestrich, lowercase).

---

### Schritt 2 – Konvertierung & Grössen (sharp)

```javascript
// image-processor.js
const sharp = require('sharp');
const path  = require('path');
const fs    = require('fs');

const SIZES = {
  team:       [200, 400, 600],
  objekte:    [400, 800, 1200],
  buero:      [800, 1200, 1600],
  allgemein:  [800, 1200, 1600, 2400],
};
const FORMATS = ['avif', 'webp', 'jpg'];

async function processImage(inputPath, outputDir, category) {
  const sizes   = SIZES[category] || SIZES.allgemein;
  const baseName = path.basename(inputPath, path.extname(inputPath));
  const results  = [];

  for (const width of sizes) {
    for (const format of FORMATS) {
      const outName = `${baseName}-${width}w.${format}`;
      const outPath = path.join(outputDir, outName);

      await sharp(inputPath)
        .resize(width)
        .toFormat(format, {
          quality: format === 'avif' ? 60 : 80,
          effort:  format === 'avif' ? 6  : undefined,
        })
        .toFile(outPath);

      results.push({ width, format, path: outPath });
    }
  }
  return results;
}
```

**Aufwand:** ~10 Minuten Rechenzeit für 200 Bilder lokal.

---

### Schritt 3 – KI-Metadaten (Claude API)

Pro Bild werden automatisch generiert:
- `alt_text` – SEO-optimiert, beschreibend (max. 125 Zeichen)
- `title` – Keyword-relevant
- `caption` – Optional, für Bildunterschriften
- `description` – Längere Beschreibung für Mediathek

```javascript
// metadata-generator.js
const Anthropic = require('@anthropic-ai/sdk');
const client    = new Anthropic();

async function generateMetadata(imagePath, context) {
  const imageData = fs.readFileSync(imagePath).toString('base64');
  const ext       = path.extname(imagePath).slice(1);

  const response = await client.messages.create({
    model:      'claude-opus-4-6',
    max_tokens: 300,
    messages: [{
      role: 'user',
      content: [
        { type: 'image',
          source: { type: 'base64',
                    media_type: `image/${ext}`,
                    data: imageData }},
        { type: 'text',
          text: `Du bist SEO-Experte für Rudolf Schäfer KG,
                 Hausverwaltung München seit 1922.
                 Kontext: ${context}
                 Erstelle JSON mit:
                 alt_text (max 125 Zeichen, beschreibend, SEO-optimiert),
                 title (max 60 Zeichen, Keyword-relevant),
                 description (max 200 Zeichen).
                 Nur JSON, kein anderer Text.` }
      ]
    }]
  });

  return JSON.parse(response.content[0].text);
}

// Beispiel-Output:
// {
//   "alt_text": "Mehrfamilienhaus Schwabing München –
//                Hausverwaltung Rudolf Schäfer KG",
//   "title": "Referenzobjekt Schwabing | Rudolf Schäfer KG",
//   "description": "Wohn- und Geschäftshaus in München-Schwabing,
//                   verwaltet seit 2008"
// }
```

**Kosten:** ~0,20–0,50 € für alle 200 Bilder (Claude API).
**Qualitätskontrolle:** metadata.json öffnen, in ~2–3 Stunden
alle 200 Einträge prüfen und bei Bedarf korrigieren.

---

### Schritt 4 – WordPress-Import (WP-CLI)

```bash
#!/bin/bash
# wp-import.sh – Bilder + Metadaten in WordPress importieren

# Nur Original-Grössen importieren (WordPress generiert Rest via Hook)
# ODER: Alle Grössen importieren und WordPress-Generierung deaktivieren

# Bild importieren
wp media import /bilder-output/objekte-schwabing-mfh-800w.jpg \
  --title="Referenzobjekt Schwabing | Rudolf Schäfer KG" \
  --alt="Mehrfamilienhaus Schwabing München – Rudolf Schäfer KG" \
  --caption="" \
  --desc="Wohn- und Geschäftshaus in München-Schwabing"

# Batch via metadata.json:
node wp-batch-import.js metadata.json
```

```javascript
// wp-batch-import.js
// Liest metadata.json, importiert alle Bilder via WP-CLI
// Setzt alt_text, title, description automatisch
const { execSync } = require('child_process');
const metadata     = require('./metadata.json');

for (const item of metadata) {
  const cmd = `wp media import "${item.path}"
    --title="${item.title}"
    --alt="${item.alt_text}"
    --desc="${item.description}"
    --path=/var/www/rudolfschaefer`;
  execSync(cmd, { stdio: 'inherit' });
}
```

---

### Schritt 5 – Automatischer Upload-Hook (dauerhaft)

Ab Go-Live werden alle neuen Bilder beim Upload automatisch verarbeitet.

```php
// inc/image-processing.php
// Wird in functions.php eingebunden

add_filter('wp_handle_upload', 'rs_process_uploaded_image');

function rs_process_uploaded_image($upload) {
  if (!in_array($upload['type'],
      ['image/jpeg', 'image/png', 'image/webp'])) {
    return $upload;
  }

  $source = $upload['file'];
  $dir    = dirname($source);
  $name   = pathinfo($source, PATHINFO_FILENAME);

  // AVIF erzeugen (wenn Imagick AVIF unterstützt)
  if (rs_imagick_supports_avif()) {
    $imagick = new Imagick($source);
    $imagick->setImageFormat('avif');
    $imagick->setCompressionQuality(60);
    $imagick->writeImage($dir . '/' . $name . '.avif');
  }

  // WebP erzeugen (immer)
  $imagick = new Imagick($source);
  $imagick->setImageFormat('webp');
  $imagick->setCompressionQuality(80);
  $imagick->writeImage($dir . '/' . $name . '.webp');

  return $upload;
}

function rs_imagick_supports_avif() {
  return in_array('AVIF', (new Imagick())->queryFormats());
}
```

---

### Aufwands-Übersicht (einmaliger Batch)

| Schritt | Methode | Zeit |
|---------|---------|------|
| Originale in Ordner sortieren | Manuell | ~1 Std. |
| Umbenennen + Konvertieren | sharp Skript | ~10 Min. |
| KI-Metadaten generieren | Claude API | ~5 Min. + ~0,50 € |
| Metadaten QS + Korrektur | Manuell | ~2–3 Std. |
| WordPress-Import | WP-CLI Batch | ~10 Min. |
| **Gesamt** | | **~halber Tag** |

---

### Voraussetzungen

```
Lokal (für Batch):
  Node.js 18+
  npm install sharp @anthropic-ai/sdk

Server (für dauerhaften Hook):
  PHP 8.1+ mit Imagick
  Imagick 7.0.25+ (AVIF-Support)
  WP-CLI installiert

Prüfen:
  php -r "echo implode(', ', (new Imagick())->queryFormats());"
  → muss AVIF und WEBP enthalten
```

---

### Datei-Grössen-Vergleich (Beispiel 1200px Breite)

| Format | Dateigrösse | Browser-Support |
|--------|-------------|-----------------|
| JPEG | ~180 KB | Universal |
| WebP | ~120 KB | 95 %+ |
| AVIF | ~70 KB | 90 %+ |

AVIF spart gegenüber JPEG ~60 % – direkte Auswirkung auf LCP und
Core Web Vitals.
