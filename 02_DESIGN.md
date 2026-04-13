# 02_DESIGN — Corporate Design & Visuelles Konzept
<!-- Rudolf Schäfer KG | April 2026 -->

---

## Design-Grundprinzipien

Die Website muss zwei Anforderungen gleichzeitig erfüllen: Seriosität und Tradition eines 100-jährigen Münchner Familienunternehmens – und modern, schnell, mobil-optimiert. Kein Maklerbüro-Look, kein Startup-Feel.

- **Mobile First** – alle Designs zuerst für Mobile
- **Performance-Design** – keine schweren Animationen, kein übermässiges JS
- **Komponenten-Architektur** – isolierte, wiederverwendbare Bausteine in VC Studio
- **Kein Hardcoding** – alle Farben über CSS Custom Properties, alle Inhalte über CMS

---

## Farbsystem

### Primärfarben

| Name | Hex | CSS-Variable | Verwendung |
|------|-----|--------------|------------|
| Schäfer Blau | `#1B4E8C` | `--color-primary` | Header, CTAs, Links, starke Elemente |
| Schäfer Dunkelblau | `#0F3460` | `--color-primary-dark` | Hover, Footer, dunkle Abschnitte |
| Schäfer Hellblau | `#D6E4F7` | `--color-primary-light` | Hintergründe, Cards, ruhige Flächen |

### Akzentfarben

| Name | Hex | CSS-Variable | Verwendung |
|------|-----|--------------|------------|
| Schäfer Gold | `#C8A84B` | `--color-accent` | Tradition/Qualitätssignal, Jahreszahl-Highlights |
| Schäfer Gold Hell | `#FDF6E3` | `--color-accent-light` | Sanfte Highlight-Flächen |

### Neutrale Farben

| Name | Hex | CSS-Variable | Verwendung |
|------|-----|--------------|------------|
| Weiss | `#FFFFFF` | `--color-white` | Karten, Formulare |
| Hellgrau | `#F8F9FA` | `--color-bg-light` | Seitenhintergrund, Alternativ-Sections |
| Grau | `#6C757D` | `--color-text-muted` | Sekundärtext, Labels |
| Dunkel | `#1A1A1A` | `--color-text` | Fliesstext |

> **Regel:** Kein einziger Hex-Wert erscheint direkt in Komponenten-CSS – ausschliesslich via `var(--color-*)`.

---

## Typografie

### Schrift-Entscheidung

| Rolle | Schrift | Gewicht | CSS-Variable |
|-------|---------|---------|--------------|
| Display / Hero / H1–H2 | Playfair Display | 300–400 | `--font-display` |
| Body / UI / Labels | Inter | 400–600 | `--font-body` |

**Hosting:** Self-hosted via `@font-face` – kein Aufruf an `fonts.googleapis.com` (DSGVO + Performance).

### Grössen-System (Fluid Typography)

```css
--font-size-xs:      0.75rem;
--font-size-sm:      0.875rem;
--font-size-base:    1rem;
--font-size-md:      1.125rem;
--font-size-lg:      1.25rem;
--font-size-xl:      1.5rem;
--font-size-2xl:     2rem;
--font-size-3xl:     clamp(1.75rem, 3vw, 2.5rem);
--font-size-display: clamp(2.5rem, 5vw, 4rem);
```

---

## Spacing-System (4px Base)

```css
--space-1: 0.25rem;   /* 4px  */
--space-2: 0.5rem;    /* 8px  */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-6: 1.5rem;    /* 24px */
--space-8: 2rem;      /* 32px */
--space-12: 3rem;     /* 48px */
--space-16: 4rem;     /* 64px */
--space-24: 6rem;     /* 96px */
--space-32: 8rem;     /* 128px */
```

> **Regel:** Keine magic numbers in Komponenten-CSS. Ausschliesslich `var(--space-*)`.

---

## Layout

- **Container-Max-Width:** 1280px, zentriert
- **Grid:** 12-Spalten CSS Grid
- **Breakpoints:** sm 640px / md 768px / lg 1024px / xl 1280px / 2xl 1536px
- **Asymmetrie:** Content-Bereiche 7/5 oder 8/4 Spalten – nie starr zentriert

---

## Komponenten (VC Studio)

### Globale Komponenten

| Komponente | CMS-Felder | Anmerkung |
|------------|------------|-----------|
| `site-header` | Logo, Navigation[], CTA, Sprachschalter | Keine hardcodierten Nav-Links |
| `site-footer` | Aus Firmen-Settings | Copyright-Jahr aus DB |
| `breadcrumb` | Auto aus Seitenhierarchie | BreadcrumbList Schema auto |
| `cookie-banner` | Texte aus CMS | Klaro.js |

### Seiten-Komponenten

| Komponente | CMS-Felder (Auswahl) | Verwendet auf |
|------------|----------------------|---------------|
| `hero-section` | Bild, H1, Subline, CTA, Trust-Badges[] | Alle Seiten |
| `leistungs-akkordeon` | Titel, Icon, Kurztext, Detailtext, CTA | Hausverwaltung, Start |
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
| `partner-grid` | Logo, Name, Beschreibung, URL | Partnerschaften (**[OFFEN – Inhalt folgt]**) |
| `stadtteil-intro` | Stadtteil, SEO-Text, Referenzen[] | Stadtteil-Seiten |

---

## Animations-Konzept

### Erlaubt (CSS-only oder minimales JS)

| Animation | Umsetzung |
|-----------|-----------|
| Fade-in + translateY beim Scrollen | CSS Transition + Intersection Observer |
| Trust-Counter hochzählen | Kleines JS-Snippet, einmalig |
| FAQ / Akkordeon öffnen | CSS max-height Transition |
| Hover Button Fill | CSS `::before` pseudo-element |
| Sticky Header Transition | CSS-Klasse via Scroll-Event |
| Image Lazy-Load Fade | CSS opacity + Intersection Observer |

### Verboten (Performance-Killer)

- ❌ GSAP, Framer Motion, Locomotive Scroll
- ❌ Page Transitions (Barba.js)
- ❌ Custom Cursor
- ❌ Parallax-Effekte
- ❌ Video-Backgrounds

> **Regel:** Alle Animationen respektieren `prefers-reduced-motion`.

---

## Offene Design-Fragen

- [ ] Logo: SVG-Dateien in allen Varianten vorhanden? (Quer hell/dunkel, Hoch hell/dunkel)
- [ ] Corporate Design Manual vorhanden?
- [ ] Designreferenzen vom Kunden gewünscht?
- [ ] Foto-Shooting: Stil-Briefing abstimmen (Kleidung, Hintergrund, Stimmung)
