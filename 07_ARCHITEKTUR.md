# 07_ARCHITEKTUR — Website-Architektur
<!-- Rudolf Schäfer KG | April 2026 -->
<!-- Antigravity CMS + VC Studio + Claude Code + Gemini + Copilot -->

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
.btn { background: #1B4E8C; }

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
