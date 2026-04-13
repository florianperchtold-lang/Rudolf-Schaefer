# 03_TECHSPEC — Technisches Spec-Sheet
<!-- Rudolf Schäfer KG | April 2026 -->

---

## Stack (fixiert)

| Ebene | Tool | Status |
|-------|------|--------|
| CMS | Google Antigravity | ✓ fixiert |
| Visual Builder | VC Studio | ✓ fixiert |
| KI-Coding (primär) | Claude Code | ✓ fixiert |
| KI-Coding (ergänzend) | Google Gemini | ✓ fixiert |
| KI-Coding (ergänzend) | GitHub Copilot | ✓ fixiert |
| Versionierung | GitHub (.env gitignored) | ✓ fixiert |
| Hosting | Plesk → GitHub Repo-Verbindung | ✓ fixiert |
| Domain | rudolfschaefer.de (Bestand) | ✓ fixiert |
| Sprachen | Deutsch (primär) + Englisch | ✓ fixiert |

---

## Offene Tech-Entscheidungen

| Frage | Optionen | Abhängigkeit |
|-------|---------|--------------|
| Antigravity Version | Stable vs. aktuell | Tech-Setup |
| Hosting-Plan | Shared Plesk vs. VPS | Performance-Anforderungen |
| Bildoptimierung | Antigravity-nativ vs. Plugin | Tech-Setup |
| Mietangebote-Feed | Immobilie1 API / IS24 / OpenImmo / manuell | **[OFFEN – Kunde]** |
| Analytics | Matomo self-hosted vs. Plausible CE | Datenschutz-Entscheidung |
| Staging-Domain | staging.rudolfschaefer.de | Hosting-Setup |

---

## Architektur-Grundsatz: Drei Schichten

```
Schicht 1 – CMS/DB        Alle Texte, Bilder, Zahlen, Links
                           → Redakteur ändert, kein Entwickler nötig

Schicht 2 – Komponenten   HTML-Struktur + CSS-Klassen (keine Inhalte)
                           → Entwickler ändert nur bei strukturellen Änderungen

Schicht 3 – Design-System CSS Custom Properties (Farben, Spacing, Typo)
                           → Eine Datei, wirkt global
```

**Kernregel:** Kein Text, keine URL, keine Zahl, keine Farbe direkt im Template-Code.

---

## Content-Typen (Antigravity CMS)

| Content-Typ | Slug | Mehrsprachig |
|-------------|------|--------------|
| Seite | `page` | DE + EN |
| Mietobjekt | `mietobjekt` | DE + EN |
| Referenz | `referenz` | DE |
| Teammitglied | `teammitglied` | DE + EN |
| News-Artikel | `news` | DE (EN optional) |
| FAQ-Eintrag | `faq` | DE + EN |
| Testimonial | `testimonial` | DE |
| Firmen-Meilenstein | `meilenstein` | DE + EN |
| Partner | `partner` | DE + EN |
| Stadtteil | `stadtteil` | DE |
| Stellenangebot | `job` | DE |
| Firmen-Settings | `settings` | Singleton, DE + EN |

### Settings-Singleton (Single Source of Truth)

Alle globalen Firmendaten **einmal** – Footer, Kontaktseite, Schema.org, Header ziehen alle aus dieser Quelle:

```
firmenname, strasse, plz, ort, telefon, fax, email,
gruendungsjahr, mitarbeitende_anzahl,
oeffnungszeiten[], geo_lat, geo_lng,
app_ios_url, app_android_url, app_login_url
```

---

## Flexible Block-System (Page Builder)

Alle Seiten nutzen eine flexible `blocks[]`-Liste statt fixer Seitenstruktur:

```
blocks: [
  { type: 'hero-section',         ... },
  { type: 'leistungs-akkordeon',  ... },
  { type: 'referenz-grid',        ... },
  { type: 'faq-akkordeon',        ... },
  { type: 'kontakt-cta',          ... }
]
```

Neue Sektion = neuer CMS-Eintrag. Kein neuer Code.

---

## Mehrsprachigkeit (DE/EN)

```
DE: /hausverwaltung/            (Default, kein Präfix)
EN: /en/property-management/

hreflang:
  de   → /hausverwaltung/
  en   → /en/property-management/
  x-default → /hausverwaltung/
```

Templates sind sprach-agnostisch – sie rendern was das CMS liefert.

---

## CSS-Architektur

```
/css/
├── design-tokens.css       ← EINZIGE Quelle für Farben/Spacing/Typo
├── base.css                ← Reset, Body, globale Typografie-Grundlagen
├── layout/
│   ├── grid.css
│   └── section.css
├── components/             ← 1 Datei pro Komponente, max. 100 Zeilen
│   ├── btn.css
│   ├── hero.css
│   ├── card.css
│   └── ...
└── utilities.css
```

**Verboten:** Seiten-spezifische CSS-Dateien (`/css/pages/` existiert nicht).

---

## JS-Architektur

```
/js/
├── main.js                 ← Nur Module-Imports, max. 50 Zeilen
├── modules/                ← 1 Datei pro Feature, max. 80 Zeilen
│   ├── akkordeon.js
│   ├── sticky-header.js
│   ├── lazy-load.js
│   ├── counter-animation.js
│   ├── filter.js           ← Mietangebote-Filter
│   ├── map.js              ← Leaflet.js
│   └── form.js
└── utils/
    ├── dom.js
    └── a11y.js
```

---

## Datei-Grössen-Limits

| Dateityp | Max. Zeilen | Wenn überschritten |
|----------|-------------|-------------------|
| Komponente HTML | 80 | Teil-Komponenten extrahieren |
| Komponente CSS | 100 | Modifier-CSS auslagern |
| Komponente JS | 80 | Helper in utils.js |
| design-tokens.css | 120 | Kategorie-Dateien aufteilen |
| main.js | 50 | Immer nur Imports |

> **Warum?** Kleinere Dateien = KI-Tools sehen nur relevanten Scope = weniger Tokens, weniger Fehler, schnellere Iteration.

---

## Mietangebote – technische Integration

> ⚠️ **Kein iframe von Immobilie1** – kein SEO-Wert, kein Crawling.

| Option | SEO | Aufwand | Empfehlung |
|--------|-----|---------|------------|
| iframe (Bestand) | ❌ kein Wert | minimal | Nicht verwenden |
| Immobilie1 API → nativ rendern | ✅ voll | mittel | **Empfehlung wenn API verfügbar** |
| IS24 / OpenImmo Feed | ✅ voll | mittel | Ideal wenn IS24 genutzt |
| Manuelle CMS-Eingabe | ✅ voll | hoch (Pflege) | Fallback |
| Hybrid (Auto-Import + manuell) | ✅ voll | mittel | **Beste Lösung** |

Jedes Objekt bekommt eine eigene URL:
```
/vermietung/schwabing-3-zimmer-wohnung-001/
```

---

## Schema.org – automatisch aus CMS

Schema.org-Markup wird **nicht manuell** gepflegt – generiert aus CMS-Feldern:

```
/       → RealEstateAgent + LocalBusiness (aus Settings-Singleton)
/team/  → Person je Teammitglied
/news/  → NewsArticle je Artikel
/service/faq/ → FAQPage (aus FAQ-CT)
alle    → BreadcrumbList (auto aus Seitenhierarchie)
```

---

## Performance-Ziele

| Metrik | IST (März 2026) | Ziel Relaunch |
|--------|-----------------|---------------|
| Lighthouse Desktop | 46 | > 90 |
| Lighthouse Mobile | 47 | > 80 |
| LCP Desktop | 4,9 s | < 2,5 s |
| LCP Mobile | 23,6 s | < 2,5 s |
| CLS | 0,27 | < 0,1 |
| TTFB | 3,1 s | < 0,8 s |
| Lighthouse SEO | 85 | 100 |

---

## DSGVO-Strategie

| Element | Lösung |
|---------|--------|
| Analytics | Matomo self-hosted oder Plausible CE – kein Cookie-Banner nötig |
| Schriften | Self-hosted – kein fonts.googleapis.com |
| Karte | OpenStreetMap + Leaflet.js – keine Einwilligung nötig |
| Kontaktformular | SMTP via Plesk – keine US-Dienste |
| Spam-Schutz | Honeypot + serverseitige Validierung |
| Cookie-Banner | Klaro.js – nur wenn externe Dienste aktiv |

---

## Deployment-Workflow

```
Lokale Entwicklung (Antigravity + VC Studio + Claude Code)
        ↓
git commit -m "feat: ..."
        ↓
git push origin staging
        ↓
Plesk → Auto-Deploy auf staging.rudolfschaefer.de
        ↓
Review + Freigabe
        ↓
Merge in main → Deploy auf rudolfschaefer.de
```

---

## .env Variablen (Vorlage)

```bash
# .env.example – NIEMALS .env committen

# CMS
ANTIGRAVITY_DB_HOST=
ANTIGRAVITY_DB_NAME=
ANTIGRAVITY_DB_USER=
ANTIGRAVITY_DB_PASS=

# SMTP
SMTP_HOST=
SMTP_PORT=587
SMTP_USER=info@rudolfschaefer.de
SMTP_PASS=
CONTACT_RECIPIENT=info@rudolfschaefer.de

# Mietangebote (je nach gewählter Option)
IMMOBILIE1_API_KEY=
IMMOBILIE1_PROVIDER_ID=

# Analytics
MATOMO_URL=
MATOMO_SITE_ID=
```

---

## Sicherheit

```
HTTPS: Let's Encrypt via Plesk (auto-renewal)
HSTS: Strict-Transport-Security Header
HTTP Security Headers:
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
Formulare: CSRF-Token + Honeypot + Rate-Limiting (5/h je IP)
```

---

## Offene Tech-Entscheidungen

- [ ] Antigravity CMS: Plugin-Verfügbarkeit prüfen (SEO, i18n, Bildoptimierung)
- [ ] VC Studio: Custom-Komponenten-Support bestätigen
- [ ] Mietangebote: Welches System nutzt Kunde aktuell? API verfügbar?
- [ ] Hosting: Plesk-Plan – Node.js verfügbar? PHP-Version?
- [ ] Analytics: Matomo vs. Plausible final entscheiden
- [ ] Newsletter: Welche Plattform? 5.921 Abonnenten-Export möglich?
