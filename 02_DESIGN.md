# 02_DESIGN — Corporate Design & Visuelles Konzept
<!-- Rudolf Schäfer KG | April 2026 -->
<!-- Farben extrahiert aus rudolfschaefer.de via Frame-Analyse, April 2026 -->

---

## Design-Grundprinzipien

Die neue Website übernimmt das bestehende Farbsystem der Rudolf Schäfer KG – kein Bruch mit der Markenidentität, sondern technisch saubere Weiterentwicklung als CSS Design-Tokens.

- **Mobile First** – alle Designs zuerst für Mobile konzipieren
- **Performance-Design** – keine schweren Animationen, kein übermässiges JS
- **Komponenten-Architektur** – isolierte, wiederverwendbare Bausteine in VC Studio
- **Kein Hardcoding** – alle Farben über CSS Custom Properties, alle Inhalte über CMS

---

## Farbsystem (aus bestehender Website extrahiert)

> Alle Werte via Frame-by-Frame-Analyse der Live-Website (April 2026).
> Kein Hex-Wert erscheint direkt in Komponenten-CSS – ausschliesslich via `var(--color-*)`.

### Primärfarben – Rot (Markenfarbe)

| Name | Hex | RGB | CSS-Variable | Quelle / Verwendung |
|------|-----|-----|--------------|---------------------|
| Schäfer Rot | `#B4001E` | 180/0/30 | `--color-primary` | Logo, App-Banner, Unterstriche, Haupt-CTAs |
| Schäfer Rot Hell | `#DC3C46` | 220/60/70 | `--color-primary-light` | Buttons (Weiterlesen), Hover-States |
| Schäfer Rot Dunkel | `#8C0018` | 140/0/24 | `--color-primary-dark` | Aktive States |

### Sekundärfarben – Oliv/Khaki

| Name | Hex | RGB | CSS-Variable | Quelle / Verwendung |
|------|-----|-----|--------------|---------------------|
| Schäfer Oliv | `#6E6450` | 110/100/80 | `--color-secondary` | Kompetenz-Kreis, Feature-Cards |
| Schäfer Oliv Hell | `#8C8264` | 140/130/100 | `--color-secondary-light` | Hover auf Oliv-Elementen |

### Neutrale Farben

| Name | Hex | RGB | CSS-Variable | Quelle / Verwendung |
|------|-----|-----|--------------|---------------------|
| Weiss | `#FFFFFF` | 255/255/255 | `--color-white` | Haupthintergrund, Karten |
| Hellgrau | `#F5F5F5` | 245/245/245 | `--color-bg-light` | Alternierende Sections |
| Schäfer Creme | `#E6E6D2` | 230/230/210 | `--color-bg-cream` | Sidebar rechts, ruhige Flächen |
| Schäfer Dunkel | `#28281E` | 40/40/30 | `--color-dark` | Footer-Hintergrund |
| Schäfer Grau-Braun | `#504646` | 80/70/70 | `--color-section-dark` | Dunkle Content-Sektionen |
| Text Dunkel | `#2D2D2D` | 45/45/45 | `--color-text` | Fliesstext, Headlines |
| Text Grau | `#6B6B6B` | 107/107/107 | `--color-text-muted` | Labels, Metadaten |
| Text auf Dunkel | `#FFFFFF` | 255/255/255 | `--color-text-on-dark` | Text auf Footer/Dark-Sections |
| Border | `#D8D8C8` | 216/216/200 | `--color-border` | Formular-Borders, Trennlinien |

---

## Farbverwendung nach Bereichen

| Bereich | Hintergrund | Text | Akzent |
|---------|-------------|------|--------|
| Navigation | `--color-white` | `--color-text` | `--color-primary` (Hover) |
| Hero | Bild + dunkles Overlay | `--color-text-on-dark` | `--color-primary` (Unterstriche) |
| White Sections | `--color-white` | `--color-text` | `--color-primary` (CTAs, Linien) |
| Dark Content Section | `--color-section-dark` | `--color-text-on-dark` | `--color-primary-light` |
| Stärken-Kreis | `--color-secondary` | `--color-text-on-dark` | `--color-white` |
| App-Section | `--color-primary` / `--color-primary-dark` | `--color-text-on-dark` | `--color-white` |
| Sidebar / Creme | `--color-bg-cream` | `--color-text` | `--color-secondary` |
| Referenz-Kacheln | `--color-white` | `--color-text` | `--color-primary` (Slider-Dots) |
| News-Cards | `--color-white` | `--color-text` | `--color-primary` (Button) |
| Footer | `--color-dark` | `--color-text-on-dark` | `--color-primary` (Logo) |

---

## Vollständiges CSS Design-Token Set

```css
/* ================================================================
   design-tokens.css
   Rudolf Schäfer KG – Website-Relaunch 2026
   EINZIGE Quelle für alle Farbwerte, Spacing und Typografie.
   Farben extrahiert aus rudolfschaefer.de (April 2026).
   Kein Hex-Wert in Komponenten-CSS – nur via var()
   ================================================================ */

:root {

  /* ── ROT (Markenfarbe) ─────────────────────────────────────── */
  --color-primary:         #B4001E;  /* Logo, CTAs, Unterstriche   */
  --color-primary-light:   #DC3C46;  /* Buttons, Hover             */
  --color-primary-dark:    #8C0018;  /* Aktive States              */

  /* ── OLIV / KHAKI (Sekundär) ───────────────────────────────── */
  --color-secondary:       #6E6450;  /* Kompetenz-Kreis, Cards     */
  --color-secondary-light: #8C8264;  /* Hover Sekundär             */

  /* ── HINTERGRÜNDE ─────────────────────────────────────────── */
  --color-white:           #FFFFFF;
  --color-bg-light:        #F5F5F5;  /* Alternierende Sections     */
  --color-bg-cream:        #E6E6D2;  /* Sidebar, ruhige Flächen    */
  --color-dark:            #28281E;  /* Footer                     */
  --color-section-dark:    #504646;  /* Dunkle Content-Sektionen   */

  /* ── TEXT ─────────────────────────────────────────────────── */
  --color-text:            #2D2D2D;
  --color-text-muted:      #6B6B6B;
  --color-text-on-dark:    #FFFFFF;
  --color-text-on-cream:   #2D2D2D;

  /* ── BORDER / INTERAKTION ─────────────────────────────────── */
  --color-border:          #D8D8C8;
  --color-border-light:    #EBEBEB;
  --color-focus:           #DC3C46;

  /* ── SPACING (4px Basis) ──────────────────────────────────── */
  --space-1:   0.25rem;   /*   4px */
  --space-2:   0.5rem;    /*   8px */
  --space-3:   0.75rem;   /*  12px */
  --space-4:   1rem;      /*  16px */
  --space-6:   1.5rem;    /*  24px */
  --space-8:   2rem;      /*  32px */
  --space-12:  3rem;      /*  48px */
  --space-16:  4rem;      /*  64px */
  --space-24:  6rem;      /*  96px */
  --space-32:  8rem;      /* 128px */

  /* ── TYPOGRAFIE ───────────────────────────────────────────── */
  --font-display: 'Playfair Display', Georgia, serif;
  --font-body:    'Inter', system-ui, sans-serif;

  --font-size-xs:       0.75rem;
  --font-size-sm:       0.875rem;
  --font-size-base:     1rem;
  --font-size-md:       1.125rem;
  --font-size-lg:       1.25rem;
  --font-size-xl:       1.5rem;
  --font-size-2xl:      2rem;
  --font-size-3xl:      clamp(1.75rem, 3vw, 2.5rem);
  --font-size-display:  clamp(2.5rem, 5vw, 4rem);

  --line-height-tight:   1.2;
  --line-height-normal:  1.6;
  --line-height-relaxed: 1.75;

  /* ── SONSTIGES ────────────────────────────────────────────── */
  --radius-sm:       2px;
  --radius-md:       4px;
  --shadow-sm:       0 1px 3px rgba(0,0,0,0.12);
  --shadow-md:       0 4px 16px rgba(0,0,0,0.10);
  --transition:      200ms ease;
  --transition-slow: 350ms ease;
}
```

---

## Typografie

### Schrift-Entscheidung

| Rolle | Schrift | Gewicht | CSS-Variable |
|-------|---------|---------|--------------|
| Display / Hero / H1–H2 | Playfair Display | 300, 400 | `--font-display` |
| Body / UI / Labels | Inter | 400, 500, 600 | `--font-body` |

**Hinweis:** Das Logo nutzt eine kalligraphische Kursivschrift – wird als SVG beibehalten, kein Web-Font.

**Self-hosted:** Alle Schriften lokal via `@font-face` – kein `fonts.googleapis.com` (DSGVO + Performance).

```
Download: google-webfonts-helper.herokuapp.com
→ Playfair Display: 300, 400  →  /assets/fonts/playfair/
→ Inter: 400, 500, 600        →  /assets/fonts/inter/
→ Subset: latin, latin-ext
→ Format: woff2 + woff Fallback
```

---

## Layout-System

| Element | Wert |
|---------|------|
| Container-Max-Width | 1280px, zentriert |
| Grid | 12-Spalten CSS Grid |
| Breakpoints | sm 640px / md 768px / lg 1024px / xl 1280px / 2xl 1536px |
| Gutter | `--space-4` Mobile / `--space-6` Tablet / `--space-8` Desktop |
| Typische Spaltenaufteilung | 7/5 oder 8/4 – nie starr zentriert |

---

## Komponenten (VC Studio)

### Globale Komponenten

| Komponente | CMS-Felder | Besonderheit |
|------------|------------|--------------|
| `site-header` | Logo, Navigation[], CTA, Sprachschalter | Keine hardcodierten Nav-Links |
| `site-footer` | Aus Firmen-Settings | `var(--color-dark)` Hintergrund |
| `breadcrumb` | Auto aus Seitenhierarchie | BreadcrumbList Schema auto |
| `cookie-banner` | Texte aus CMS | Klaro.js |

### Seiten-Komponenten

| Komponente | CMS-Felder (Auswahl) | Verwendet auf |
|------------|----------------------|---------------|
| `hero-section` | Bild, Overlay-Opacity, H1, Subline, CTA, Trust-Badges[] | Alle Seiten |
| `leistungs-akkordeon` | Titel, Icon, Kurztext, Detailtext, CTA | Hausverwaltung, Start |
| `feature-kreis` | 4× [Icon, Titel, Text] aus CMS | Startseite (Stärken) |
| `referenz-grid` | Stadtteil, Typ, Foto, Beschreibung | Hausverwaltung, Start |
| `team-grid` | Portrait, Name, Funktion, Kontakt | Team |
| `faq-akkordeon` | Frage, Antwort, Kategorie | FAQ, Leistungsseiten |
| `mietobjekt-liste` | Filter + Objekte aus DB | Vermietung |
| `mietobjekt-card` | Foto, Lage, Zimmer, Preis, Status | Vermietung |
| `timeline-block` | Jahr, Titel, Text, Foto (opt.) | Über Uns |
| `testimonial-slider` | Zitat, Name, Funktion | Hausverwaltung, Start |
| `trust-counter` | Label, Zahl, Einheit – alle aus CMS | Startseite, Über uns |
| `app-teaser` | Screenshots, Features[], Store-Links | Service/App, Start |
| `news-grid` | Automatisch aus News-CT | News, Start |
| `kontakt-block` | Aus Firmen-Settings | Kontakt, Footer |
| `partner-grid` | Logo, Name, Beschreibung, URL | Partnerschaften **[OFFEN]** |
| `stadtteil-intro` | Stadtteil, SEO-Text, Referenzen[] | Stadtteil-Seiten |

---

## Animations-Konzept

### Erlaubt

| Animation | Trigger | Umsetzung |
|-----------|---------|-----------|
| Fade-in + translateY | Scroll (Intersection Observer) | CSS Transition |
| Trust-Counter hochzählen | Scroll in Viewport | Kleines JS-Snippet |
| Akkordeon öffnen/schliessen | Klick | CSS max-height Transition |
| Button Hover | Hover | `filter: brightness(0.88)` auf Primary |
| Sticky Header | Scroll > 80px | CSS-Klasse per JS |
| Bild Lazy-Load Fade | Intersection Observer | CSS opacity |
| Nav-Unterstrich | Hover | CSS `::after` Transform scaleX |

### Verboten

- ❌ GSAP, Framer Motion, Locomotive Scroll
- ❌ Page Transitions (Barba.js)
- ❌ Custom Cursor
- ❌ Parallax-Effekte
- ❌ Video-Backgrounds

> Alle Animationen respektieren `prefers-reduced-motion: reduce`.

---

## Offene Design-Fragen

- [ ] Logo: SVG-Dateien in allen Varianten vorhanden? (Quer hell/dunkel, Hoch hell/dunkel)
- [ ] Corporate Design Manual vorhanden?
- [ ] Foto-Shooting: Stil-Briefing abstimmen
- [ ] Kalligraphie-Schrift des Logos identifizieren (ggf. für Headline-Akzente)
