# 03_TECHSPEC — Technisches Spec-Sheet
<!-- Rudolf Schäfer KG | April 2026 -->
<!-- Update: Stack-Entscheidung WordPress + Bricks + ACF (April 2026) -->

---

## Stack (aktueller Stand)

| Ebene | Tool | Status |
|-------|------|--------|
| CMS | WordPress | ✓ fixiert |
| Page Builder | Bricks Builder (Lifetime-Lizenz) | ✓ Tendenz – Entscheidung ausstehend |
| Custom Fields | ACF (Advanced Custom Fields) | ✓ Tendenz – Pro vs. Free offen |
| KI-Coding (primär) | Claude Code | ✓ fixiert |
| KI-Coding (ergänzend) | Google Gemini | ✓ fixiert |
| KI-Coding (ergänzend) | GitHub Copilot | ✓ fixiert |
| Versionierung | GitHub (.env gitignored) | ✓ fixiert |
| Hosting | Plesk → GitHub Repo-Verbindung | ✓ fixiert |
| Domain | rudolfschaefer.de (Bestand) | ✓ fixiert |
| Sprachen | Deutsch (primär) + Englisch | ✓ fixiert |
| Lokale Entwicklung | Local (by Flywheel) | ✓ fixiert |
| WordPress Connector | Claude Settings → Connectors → WordPress | ✓ fixiert |
| Node.js | Voraussetzung für Claude Code | ✓ fixiert |

---

## Stack-Begründungen

### WordPress
Basis-CMS. Robert Eberhard (cult consult, IST-Analyse März 2026) empfiehlt
WordPress als neue Basis. Builder-Entscheidung war offen – wurde separat
getroffen.

### Bricks Builder (Lifetime-Lizenz)
- Sauberer, minimaler HTML/CSS-Output
- Lädt CSS nur für verwendete Elemente (kein Overhead wie Elementor)
- Hohe Claude Code Kompatibilität (saubere Template-Struktur)
- Einmalige Lifetime-Lizenz – kein Abo
- Direkte Konkurrenz: Breakdance (günstiger), Oxygen (günstig, einmalig)

**Verworfen: Elementor**
Elementor generiert aufgeblähten Code, render-blockierende Ressourcen,
übermässiges JavaScript. War Hauptursache für Lighthouse 46/47 auf der
aktuellen Seite – würde das Problem nach dem Relaunch wiederholen.


### ACF (Advanced Custom Fields)
Ersetzt ein separates Headless-CMS. Verwaltet alle Custom Content-Typen:
Team, FAQ, Referenzen, Mietobjekte, Testimonials, Meilensteine,
Partner, Settings-Singleton.

**Offen:** ACF Pro (kostenpflichtig) vs. ACF Free – je nach benötigten
Features (Repeater, Flexible Content → vermutlich Pro nötig).

### Alternativen zu Bricks (falls Kosten problematisch)

| Builder | Lizenz | Performance | Claude Code | Bewertung |
|---------|--------|-------------|-------------|-----------|
| **Bricks** | Lifetime ~$299 | ★★★★★ | ★★★★★ | Empfehlung |
| **Breakdance** | Lifetime ~$149 | ★★★★★ | ★★★★☆ | Gute Alternative |
| **Oxygen** | Einmalig ~$100 | ★★★★★ | ★★★★☆ | Günstigste Option |
| **Kadence Blocks** | Kostenlos | ★★★★☆ | ★★★★☆ | Gratis-Option |
| **GenerateBlocks** | Kostenlos | ★★★★★ | ★★★☆☆ | Sehr minimal |
| Elementor | Abo | ★★☆☆☆ | ★★★☆☆ | Nicht verwenden |

---

## Claude Code Skills (.claude/skills/)

Relevante WordPress Skills die aktiviert werden:

| Skill | Zweck |
|-------|-------|
| `wp-block-themes` | Block themes: theme.json, templates, patterns |
| `wp-block-development` | Gutenberg blocks: block.json, attributes |
| `wp-plugin-development` | Plugin-Architektur, hooks, settings API |
| `wp-rest-api` | REST API routes, schema, auth |
| `wp-performance` | Profiling, caching, DB-Optimierung |
| `wp-wpcli-and-ops` | WP-CLI, automation, search-replace |
| `wpds` | WordPress Design System |
| `elementor-safe-edit` | Falls doch Elementor-Elemente vorhanden |

Ordner: `/projektordner/.claude/skills/`

---

## Entwicklungs-Workflow (Phasen)

### Phase 1 – Design (Google Stitch)
- Referenzseiten sammeln (Dribbble, awwwards.com, Wettbewerber)
- Screenshots + `02_DESIGN.md` (Farben, Tokens) als Basis
- Stitch-Prompts je Seite (Startseite zuerst)
- Stitch-Export = visueller Prototyp, kein produktiver Code
- Iteration bis Design stimmt
- Stitch → Export → Briefing für Claude Code

### Phase 2 – Lokale Umgebung
- Local (by Flywheel) installieren
- WordPress-Site anlegen + Backup-Strategie aktivieren
- WordPress mit Claude verbinden (Settings → Connectors → WordPress URL)
- `.claude/skills/` Ordner anlegen, relevante Skills einfügen
- Bricks + ACF installieren und lizenzieren
- MCP einrichten (Novamira oder Alternative – noch offen)

### Phase 3 – Theme & Architektur (Claude Code)
Reihenfolge strikt einhalten:
1. `design-tokens.css` (Farben, Spacing – einmalig)
2. Globale Komponenten (Header, Footer, Navigation)
3. Bricks-Templates einzeln (Hero, Akkordeon, Grid etc.)
4. ACF-Feldgruppen definieren (Settings, Team, FAQ, Referenzen...)
5. Seiten-Templates

### Phase 4 – Content
- ACF Settings-Singleton befüllen (Firmendaten einmalig)
- Inhalte aus `04_CONTENT.md` eintragen
- Mietangebote-Integration (Immobilie1 API oder ACF manuell)
- SEO-Felder je Seite (nach `05_SEO.md`)

### Phase 5 – Staging & QA
- Local → Staging-Server (Plesk → staging.rudolfschaefer.de)
- Notion MCP als Checklist für Site Scan
- Lighthouse messen (Ziel: > 90)
- Security: Wordfence + Malka
- SEO-Audit: Schema.org, hreflang, Redirects
- Cross-Device Testing

### Phase 6 – Go-Live
- 301 Redirect-Map aktivieren
- robots.txt: Staging sperren, Prod freigeben
- Google Search Console verbinden, Sitemap einreichen
- Google Business Profile URL aktualisieren
- Monitoring: Analytics-Tool (TBD) + Search Console

---

## Design-Workflow (Google Stitch)

```
Referenzen sammeln
(Dribbble, awwwards.com)
        ↓
Screenshots erstellen
        ↓
Prompt in Google Stitch
(Layout + Farben aus 02_DESIGN.md)
        ↓
Stitch Editing (iterieren)
        ↓
Export → Briefing für Claude Code
        ↓
Claude Code baut WordPress/Bricks-Template
```

**Design Cloning Workflow (Alternative):**
```
Whisk (labs.google) → Screenshot einer Referenzseite
        ↓
Google AI Studio → Analyse + Prompt-Generierung
        ↓
ezgif.com/video-to-jpg → falls Video-Referenz
        ↓
Google Stitch oder direkt Claude Code
```

---

## Architektur-Grundsatz: Drei Schichten

```
Schicht 1 – WordPress/ACF   Alle Texte, Bilder, Zahlen, Links
                             → Redakteur ändert, kein Entwickler nötig

Schicht 2 – Bricks Templates HTML-Struktur + CSS-Klassen (keine Inhalte)
                             → Entwickler ändert nur bei strukturellen Änderungen

Schicht 3 – Design-System   CSS Custom Properties (Farben, Spacing, Typo)
                             → Eine Datei, wirkt global
```

**Kernregel:** Kein Text, keine URL, keine Zahl, keine Farbe direkt
im Template-Code. Alles aus ACF-Feldern oder design-tokens.css.

---

## ACF Content-Typen (ersetzt Antigravity)

| Content-Typ | ACF-Feldgruppe | Mehrsprachig |
|-------------|----------------|--------------|
| Seite | Page Settings | DE + EN (WPML) |
| Mietobjekt | Rental Property | DE + EN |
| Referenz | Reference Object | DE |
| Teammitglied | Team Member | DE + EN |
| News-Artikel | WordPress Post | DE (EN optional) |
| FAQ-Eintrag | FAQ Entry | DE + EN |
| Testimonial | Testimonial | DE |
| Firmen-Meilenstein | Company Milestone | DE + EN |
| Partner | Partner | DE + EN |
| Stadtteil | District Page | DE |
| Stellenangebot | Job Listing | DE |
| Firmen-Settings | **Options Page (Singleton)** | DE + EN |

### Settings Options Page (Single Source of Truth)

ACF Options Page = WordPress-äquivalent zum Antigravity Settings-Singleton.
Alle globalen Firmendaten **einmal** – Footer, Kontaktseite, Schema.org
ziehen alle aus dieser Quelle:

```
firmenname, strasse, plz, ort, telefon, fax, email,
gruendungsjahr, mitarbeitende_anzahl,
oeffnungszeiten[], geo_lat, geo_lng,
app_ios_url, app_android_url, app_login_url
```

---

## Bricks-spezifische Architektur-Regeln

### 1 – Eigene Template-Datei je Block-Typ
```
/bricks/templates/
├── hero-section.php
├── leistungs-akkordeon.php
├── faq-akkordeon.php
├── team-grid.php
├── trust-counter.php
├── mietobjekt-card.php
├── referenz-grid.php
├── app-teaser.php
└── ...
```

### 2 – ACF-Felder statt Hardcoding in Bricks
```php
// ✗ FALSCH
echo '<h1>Hausverwaltung München seit 1922</h1>';

// ✓ RICHTIG
echo '<h1>' . get_field('hero_h1') . '</h1>';
// oder via Bricks Dynamic Data: {acf_hero_h1}
```

### 3 – CSS aus Bricks-Output raus
Bricks → Settings → Performance → CSS Loading Method:
**"External Files"** (nicht inline)

### 4 – design-tokens.css als Root
```css
/* design-tokens.css wird als erstes geladen */
:root {
  --color-primary: #B4001E;
  --color-secondary: #6E6450;
  /* etc. */
}
```
Bricks-Komponenten nutzen ausschliesslich `var(--color-*)`.

---

## Mehrsprachigkeit (DE/EN)

```
DE: /hausverwaltung/            (Default, kein Präfix)
EN: /en/property-management/

Plugin: WPML oder Polylang
hreflang: de → /, en → /en/, x-default → /
```

---

## CSS-Architektur

```
/wp-content/themes/schaefer/
├── design-tokens.css       ← EINZIGE Quelle für Farben/Spacing/Typo
├── style.css               ← WordPress Theme-Header + Base
├── css/
│   ├── base.css
│   ├── layout/
│   │   ├── grid.css
│   │   └── section.css
│   ├── components/         ← 1 Datei pro Komponente, max. 100 Zeilen
│   │   ├── btn.css
│   │   ├── hero.css
│   │   ├── akkordeon.css
│   │   └── ...
│   └── utilities.css
```

---

## Mietangebote – technische Integration

> ⚠️ Kein iframe von Immobilie1 – kein SEO-Wert, kein Crawling.

| Option | SEO | Empfehlung |
|--------|-----|------------|
| iframe (Bestand) | ❌ | Nicht verwenden |
| Immobilie1 API → ACF nativ | ✅ | Empfehlung wenn API verfügbar |
| IS24 / OpenImmo Feed | ✅ | Ideal wenn IS24 genutzt |
| ACF manuelle Eingabe | ✅ | Fallback |
| Hybrid (Auto-Import + manuell) | ✅ | Beste Lösung |

---

## Performance-Ziele

| Metrik | IST (März 2026) | Ziel |
|--------|-----------------|------|
| Lighthouse Desktop | 46 | > 90 |
| Lighthouse Mobile | 47 | > 80 |
| LCP Desktop | 4,9 s | < 2,5 s |
| LCP Mobile | 23,6 s | < 2,5 s |
| CLS | 0,27 | < 0,1 |
| TTFB | 3,1 s | < 0,8 s |
| Lighthouse SEO | 85 | 100 |

---

## Security

```
Wordfence     ← WordPress Security Plugin
Malka         ← Zusätzliche Security-Ebene
Let's Encrypt ← SSL via Plesk (auto-renewal)
HSTS          ← Strict-Transport-Security Header
HTTP Headers:
  X-Frame-Options: DENY
  X-Content-Type-Options: nosniff
  Referrer-Policy: strict-origin-when-cross-origin
Formulare: CSRF-Token + Honeypot + Rate-Limiting
```

---

## DSGVO-Strategie

| Element | Lösung |
|---------|--------|
| Analytics | Matomo self-hosted, Plausible CE oder Google Analytics – **Entscheidung Robert Eberhard** |
| Schriften | Self-hosted – kein fonts.googleapis.com |
| Karte | OpenStreetMap + Leaflet.js |
| Kontaktformular | SMTP via Plesk |
| Spam-Schutz | Honeypot + serverseitige Validierung |
| Cookie-Banner | Klaro.js – nur wenn externe Dienste aktiv |

---

## Deployment-Workflow

```
Lokale Entwicklung (Local by Flywheel + Bricks + ACF + Claude Code)
        ↓
git commit -m "feat: ..."
        ↓
git push origin staging
        ↓
Plesk → Auto-Deploy auf staging.rudolfschaefer.de
        ↓
Review + Freigabe (Notion MCP Checklist)
        ↓
Merge in main → Deploy auf rudolfschaefer.de
```

---

## .env Variablen (Vorlage)

```bash
# .env.example – NIEMALS .env committen

# WordPress DB
WP_DB_HOST=
WP_DB_NAME=
WP_DB_USER=
WP_DB_PASS=

# SMTP
SMTP_HOST=
SMTP_PORT=587
SMTP_USER=info@rudolfschaefer.de
SMTP_PASS=
CONTACT_RECIPIENT=info@rudolfschaefer.de

# Mietangebote
IMMOBILIE1_API_KEY=
IMMOBILIE1_PROVIDER_ID=

# Analytics
MATOMO_URL=
MATOMO_SITE_ID=
```

---

## Offene Tech-Entscheidungen

- [ ] Bricks vs. Breakdance vs. Oxygen – finale Builder-Entscheidung
- [ ] ACF Pro vs. ACF Free – Feature-Bedarf klären
- [ ] Mehrsprachigkeit: WPML vs. Polylang
- [ ] MCP: Novamira oder Alternative
- [ ] Mietangebote: Immobilie1 API verfügbar? IS24?
- [ ] Analytics: Matomo / Plausible CE / Google Analytics – Empfehlung Robert Eberhard einholen
- [ ] Newsletter-System: aktuell verwendete Plattform? Export möglich?
- [ ] Hosting: Plesk-Plan – Node.js verfügbar? PHP-Version?

## Video-Referenzen (Workflow-Research)

- https://www.youtube.com/watch?v=opQJU2_VZDo (WordPress Studio + Claude Code + Telex)
- https://www.youtube.com/watch?v=BPevMfqqsr0 (WordPress Studio + Claude Code)
- https://www.youtube.com/watch?v=KbEkYmqc0ss (Claude Site Local + Skills)
- https://www.youtube.com/watch?v=m9o34HnjE1k (Google Stitch Design-Workflow)
- https://www.youtube.com/watch?v=BH4j9TMtQ8Y (Antigravity + Claude Code)
- https://www.youtube.com/watch?v=j74kjYvzzLk (Design Cloning Workflow)

---

## Mietangebote – Bestehende Integration (IST)

<!-- Quelle: Julie Schäfer E-Mail, 23.03.2026 + Perchti Statusreport Aug. 2025 -->

| Element | Wert |
|---------|------|
| CRM / Immobilien-Software | **OnOffice** |
| Portal | **Immobilie1** (ausschliesslich) |
| Aktuelle Integration | Immobilie1-Widget / iframe – Konflikte mit WordPress-Code bekannt |
| Problem | Immobilie1 hat 2025 auf neues System umgestellt → Darstellungseinschränkungen |
| SEO-Wert aktuell | Keiner (iframe, kein Crawling) |

**Für Relaunch:** OnOffice hat OpenImmo-Schnittstelle zu WordPress.
Eberhard empfiehlt Klärung welche API/Schnittstelle verfügbar ist.
Ziel: Jedes Mietobjekt bekommt eine eigene WordPress-URL mit eigenem SEO-Wert.

---

## Analytics – IST vs. SOLL

| | IST (Bestand) | SOLL (Relaunch) |
|--|---------------|-----------------|
| Tool | etracker (von Fairrank genutzt) | Matomo / Plausible CE / Google Analytics – **offen, Entscheidung Robert Eberhard** |
| Cookie-Banner | Ja (etracker benötigt Einwilligung) | Abhängig vom gewählten Tool |
| Daten-Kontrolle | Bei etracker GmbH | Abhängig vom gewählten Tool |
| Google Analytics | Nein | Möglich – Entscheidung ausstehend |

---

## Bekannte technische Probleme der alten Website
<!-- Quelle: Perchti Statusreport Aug. 2025, Martin Schäfer E-Mail Aug. 2025 -->
<!-- Wichtig für Relaunch: Diese Fehler dürfen sich nicht wiederholen -->

- Newsletter-Registrierung auf iPhone nicht funktionsfähig (Button reagiert nicht)
- Seite „wackelt" im iPhone Hochformat (Responsive-Problem)
- Team-Bereich: Ladezeit-Probleme durch viele Bilder → als eigene Seite ausgelagert
- Immobilie1-Integration: Konflikte im Code nach System-Umstellung
- Seite war häufig offline (Hosting-Instabilität, IONOS)
- Links in englischer Version waren fehlerhaft/veraltet
- Datenschutz/Impressum war nur auf Deutsch vorhanden
- 404-Fehler auf EN-Seite: Estate Agent Service, Contact Person, Rental-Newsletter
- Kein Metadaten-Plugin → Fairrank konnte Metadaten nicht bearbeiten (Yoast nachinstalliert)
- Seiten-Ranking: 94,4 % Traffic auf Startseite – strukturelles Problem

**Konsequenzen für Relaunch:**
- Mobile-Testing zwingend (iPhone + Android) vor Launch
- Hosting: Plesk/VPS mit garantierter Uptime
- Metadaten: via RankMath oder SEOPress nativ in WordPress
- Alle EN-Links vor Launch testen
- Immobilie1: nativ integrieren, kein iframe

---

## WordPress-Grundanforderungen

### Redaktionell pflegbare Bereiche (Custom Post Types)

| CPT | Slug | Redakteur kann | Technisch |
|-----|------|----------------|-----------|
| News | `post` (WordPress nativ) | Artikel anlegen, Kategorien, Bilder | Standard WordPress Posts |
| Team | `team` | Portrait, Name, Funktion, Abteilung, Kontakt | Eigener CPT + ACF |
| Immobilien | `immobilie` | Objekt anlegen, Fotos, Beschreibung, Zuordnung | Eigener CPT + ACF + Checkbox |

### Immobilien CPT – Checkbox-Zuteilung

Ein einziger CPT `immobilie` mit ACF-Checkbox-Feld `bereiche`:

```php
// ACF Checkbox-Feld: bereiche
Optionen:
  [ ] verwaltung   → erscheint auf /hausverwaltung/referenzen/
  [ ] vermietung   → erscheint auf /vermietung/
  [ ] verkauf      → erscheint auf /verkauf/

// Ein Objekt kann mehreren Bereichen zugeordnet sein
// Kein doppeltes Einpflegen
```

Archiv-Seiten filtern per `tax_query` oder `meta_query` nach dem
jeweiligen Checkbox-Wert. Template ist identisch – nur die Datenmenge
unterscheidet sich je Bereich.

---

## Plugin-Philosophie

**Grundsatz:** Fertige Plugins nur verwenden wenn das Problem nicht selbst
lösbar ist (ohne Plugin oder mit eigenem kleinen Plugin).

### Verwende ich (keine Alternative sinnvoll)
| Plugin | Zweck | Kosten |
|--------|-------|--------|
| Bricks Builder | Page Builder | Lifetime-Lizenz |
| ACF (Advanced Custom Fields) | Custom Fields | Free / Pro |
| Wordfence | Security | Free |
| RankMath oder SEOPress | SEO-Metadaten | Free |

### Eigene Lösung bevorzugt
| Bedarf | Statt Plugin | Eigene Lösung |
|--------|-------------|---------------|
| Kontaktformular | Contact Form 7, Gravity Forms | Eigenes PHP-Formular, ~50 Zeilen |
| Cookie-Banner | Cookiebot, OneTrust | Klaro.js (self-hosted, kostenlos) |
| Karte | Google Maps Plugin | Leaflet.js + OpenStreetMap |
| Lazy Loading | Lazy Load Plugin | WordPress nativ (loading="lazy") |
| Bildkonvertierung | Imagify, ShortPixel | Eigener Upload-Hook (PHP/Imagick) |
| Caching | WP Rocket, W3 Total Cache | Nginx FastCGI Cache via Plesk |
| Sitemap | Yoast Sitemap | RankMath oder WordPress nativ |
| SMTP | WP Mail SMTP | Eigene wp_mail() Konfiguration |

### Verboten
- Elementor (Performance-Killer)
- Yoast SEO (war Fairrank-Tool, wird abgelöst)
- Google Analytics (DSGVO)
- Google Fonts via CDN (DSGVO)
- Jetpack (Overhead)
- Page Speed Plugins die Code verändern (brechen Bricks-Output)

---

## Performance-Strategie

### Bildformat-Pipeline

**Priorität:** AVIF → WebP → JPEG/PNG (Fallback)

```html
<!-- Bricks-Template rendert automatisch: -->
<picture>
  <source srcset="bild-400w.avif 400w, bild-800w.avif 800w, bild-1200w.avif 1200w"
          type="image/avif">
  <source srcset="bild-400w.webp 400w, bild-800w.webp 800w, bild-1200w.webp 1200w"
          type="image/webp">
  <img src="bild-800w.jpg"
       srcset="bild-400w.jpg 400w, bild-800w.jpg 800w, bild-1200w.jpg 1200w"
       alt="{{ acf_alt_text }}"
       width="800" height="600"
       loading="lazy">
</picture>
```

**Grössen je Verwendungszweck:**

| Verwendung | Breiten | Lazy Loading |
|------------|---------|--------------|
| Hero | 800w, 1200w, 1600w, 2400w | Nein (above fold) |
| Team-Portrait | 200w, 400w, 600w | Ja |
| Referenz-Foto | 400w, 800w, 1200w | Ja |
| News-Beitragsbild | 400w, 800w, 1200w | Ja |
| OG-Image | 1200×630 fix (JPG) | – |

**Voraussetzung Server:** PHP Imagick mit AVIF-Support
(Plesk → PHP 8.1+ mit Imagick kompiliert, AVIF ab Imagick 7.0.25)

```bash
# Prüfen ob AVIF verfügbar:
php -r "echo (new Imagick())->queryFormats('AVIF') ? 'OK' : 'Fehler';"
```

Falls AVIF serverseitig nicht verfügbar: WebP als Primär, JPEG als Fallback.

### Weitere Performance-Massnahmen

| Massnahme | Umsetzung |
|-----------|-----------|
| CSS external only | Bricks → Settings → Performance |
| Kein render-blocking JS | Alle Scripts mit `defer` oder `async` |
| Nginx FastCGI Cache | Plesk → Nginx Cache aktivieren |
| Schriften self-hosted | @font-face, kein CDN |
| Kein Google Maps | Leaflet.js + OpenStreetMap |
| Kein iframe Mietangebote | OnOffice/Immobilie1 API nativ |
| HTTP/2 | Plesk → SSL + HTTP/2 aktivieren |
| GZIP / Brotli | Plesk → Kompression aktivieren |
| Critical CSS | Bricks inline critical, rest deferred |

---

## DSGVO-Strategie (vollständig)

### Grundsatz: Privacy by Default
Kein externer Service wird geladen ohne explizite Nutzereinwilligung.
Ausnahmen: Self-hosted Services (Matomo, Schriften, OpenStreetMap).

### Cookie-Banner: Klaro.js
- Self-hosted (kein SaaS, kein CDN-Aufruf)
- Kostenlos, Open Source
- DSGVO-konform, kein Cookie ohne Einwilligung
- Konfigurierbar via JSON

```javascript
// klaro-config.js – alle Services deklarieren
var klaroConfig = {
  services: [
    { name: 'matomo', title: 'Matomo Analytics',
      purposes: ['analytics'], default: false },
    // Weitere Services nur wenn aktiv
  ]
};
```

### Services im Überblick

| Service | Hosting | Cookie-Banner nötig | Einwilligung |
|---------|---------|---------------------|--------------|
| Matomo Analytics | Self-hosted | Nein (DSGVO-Modus) | Nein |
| Schriften (self-hosted, TBD) | Self-hosted | Nein | Nein |
| OpenStreetMap + Leaflet.js | CDN jsDelivr | Ja (empfohlen) | Optional |
| Kontaktformular | Eigener Server | Nein | Nein |
| Immobilie1 API | Extern | Ja | Ja |
| Keine Social Media Buttons | – | – | – |
| Kein Google Analytics | – | – | – |
| Kein Google Maps | – | – | – |
| Kein Google Fonts CDN | – | – | – |

---

## Barrierefreiheit (WCAG 2.1 AA)

**Ziel:** WCAG 2.1 Level AA – gesetzliche Anforderung für öffentlich
zugängliche Websites ab 2025 (EU Web Accessibility Directive).

### Technische Anforderungen

| Bereich | Anforderung | Umsetzung |
|---------|-------------|-----------|
| Alt-Texte | Alle Bilder mit Alt-Text | Pflichtfeld im ACF-Medienfeld |
| Kontraste | min. 4,5:1 (Normal), 3:1 (Gross) | Farbsystem aus design-tokens.css prüfen |
| Tastaturnavigation | Alle Funktionen per Tastatur | Focus-Styles in btn.css, nav.css |
| Skip-Links | „Zum Inhalt springen" | Im base.html als erstes Element |
| ARIA-Labels | Alle Icons, Buttons ohne sichtbaren Text | In Bricks-Templates ergänzen |
| Überschriften-Hierarchie | H1 → H2 → H3, keine Lücken | Bricks-Templates prüfen |
| Formular-Labels | Alle Inputs mit `<label>` | Im eigenen Formular-Code |
| Fokus sichtbar | Fokus-Ring auf allen interaktiven Elementen | `--color-focus: #DC3C46` in tokens |
| Sprach-Attribut | `lang="de"` auf `<html>` | In base.html |
| PDF-Alternativtext | Alle verlinkten PDFs beschriftet | Im CMS-Link-Feld |

### Farb-Kontrast-Check (aus design-tokens.css)

| Kombination | Kontrast | Anforderung | Status |
|-------------|----------|-------------|--------|
| #2D2D2D auf #FFFFFF | 13,9:1 | 4,5:1 | ✓ |
| #FFFFFF auf #B4001E | 5,1:1 | 4,5:1 | ✓ |
| #FFFFFF auf #28281E | 16,1:1 | 4,5:1 | ✓ |
| #FFFFFF auf #6E6450 | 4,2:1 | 4,5:1 | ⚠ prüfen |
| #6B6B6B auf #FFFFFF | 5,7:1 | 4,5:1 | ✓ |

> ⚠️ `--color-secondary` (#6E6450) auf Weiss knapp unter AA.
> Für Fliesstext nicht verwenden – nur für dekorative Elemente oder grosse Texte.

---

## Sicherheit (vollständig)

### WordPress-Härtung

```php
// wp-config.php Ergänzungen
define('DISALLOW_FILE_EDIT', true);      // Editor deaktivieren
define('DISALLOW_FILE_MODS', true);      // Plugin/Theme-Updates nur via WP-CLI
define('WP_DEBUG', false);               // Kein Debug in Production
define('FORCE_SSL_ADMIN', true);         // Admin nur via HTTPS

// Eigene Security Keys (frisch generieren):
// https://api.wordpress.org/secret-key/1.1/salt/
```

### HTTP Security Headers (Nginx via Plesk)

```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
add_header X-Frame-Options "DENY" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
add_header Permissions-Policy "camera=(), microphone=(), geolocation=()" always;
add_header Content-Security-Policy "default-src 'self'; ..." always;
```

### Plugins & Tools

| Tool | Zweck | Kosten |
|------|-------|--------|
| Wordfence Free | Firewall, Malware-Scan, Login-Schutz | Kostenlos |
| Malka | Zusätzliche Sicherheitsebene | Klären |
| Let's Encrypt | SSL via Plesk (auto-renewal) | Kostenlos |
| WP-CLI | Updates headless, kein FTP | Kostenlos |

### Weitere Massnahmen

- Login-URL ändern (kein `/wp-admin/` default)
- Brute-Force-Schutz (Wordfence)
- XML-RPC deaktivieren
- REST API auf authentifizierte Nutzer beschränken (wo möglich)
- Dateirechte: 644 (Dateien), 755 (Ordner), 600 (wp-config.php)
- Automatische WordPress-Core-Updates aktivieren (Minor)
- Datenbank-Prefix ändern (nicht `wp_`)
