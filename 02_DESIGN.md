# 02_DESIGN — Corporate Design & Visuelles Konzept
<!-- Rudolf Schäfer KG | April 2026 -->
<!-- Farben extrahiert aus rudolfschaefer.de via Frame-Analyse, April 2026 -->

---

## Design-Philosophie & Gestaltungsmetapher

### Die Leitidee: Vertikal

Die neue Website ist kein Redesign – sie ist ein gestalterisches Statement. Das Design spiegelt die Identität des Unternehmens: **geerdet und bodenständig, mit einem vertikalen Bestreben nach Weiterentwicklung.**

Die Metapher ist konkret und inhärent:
- **Gebäude sind vertikal.** Fassaden, Stockwerke, Türme – das Kerngeschäft selbst ist vertikal.
- **Wachstum ist vertikal.** Das Bestreben, sich stets weiterzuentwickeln, drückt sich in Aufwärtsbewegung aus.
- **Solidität ist die Basis.** Nicht Leichtigkeit, sondern Substanz. Von unten gewachsen, nach oben strebend.

Das Ergebnis: Eine Site, die als **State of the Art** erkannt wird – innovativ und dynamisch in der Gestaltung, ohne den Charakter einer 100-jährigen Institution zu verlieren.

```
        ↑  Bestreben, Wachstum, Innovation
        │
        │  strukturiert · dynamisch · vertikal
        │
▓▓▓▓▓▓▓▓▓  solide Basis · Tradition · München
```

### Gestaltungsprinzipien

| Prinzip | Bedeutung |
|---------|-----------|
| **Vertikal** | Komposition, Raster, Bewegungsrichtung – immer von unten nach oben |
| **Fluid, nicht rows** | Kein mechanisches Reihen-Layout; Bereiche entstehen flüssig, organisch |
| **Weißraum als Aussage** | Grosszügige Luft ist kein Fehler – sie ist Haltung. Man muss sich Weißraum leisten können. |
| **State of the Art** | Die Seite soll als modern und innovativ wahrgenommen werden – Gestaltung auf Augenhöhe mit Premiummarken |
| **Storytelling durch Scroll** | Inhalte werden nicht präsentiert, sondern erzählt – der Scroll ist der Erzähler |
| **Strukturiert & kreativ** | Klare Ordnung, aber nie starr. Grid als Rahmen, nicht als Käfig. |

---

## Hero-Section — Das Signature-Element

Der Hero ist das visuelle Aushängeschild der Seite und setzt die Designmetapher unmittelbar um.

### Konzept: Fünf vertikale Balken

```
┌──┬────────┬──┬────────┬──┐
│  │        │  │        │  │
│  │  Bild  │↕ │  Bild  │  │
│  │        │  │        │  │
│  │        │[TEXT]     │  │
│  │        │vertikal   │  │
│  │        │  │        │  │
└──┴────────┴──┴────────┴──┘
  1     2    3     4    5
```

- **5 senkrechte Rechtecke** teilen den Hero-Bereich auf
- Die Balken dienen als **Clip-Mask für das Hintergrundbild** – das Bild scheint durch die Balken hindurch
- Balken **2 oder 4** enthält den **Hero-Text 90° rotiert** – `writing-mode: vertical-rl; transform: rotate(180deg)` – von unten nach oben lesbar
- Die Balken haben **unterschiedliche vertikale Positionen** – leicht versetzt, nicht bündig ausgerichtet
- Eine **organische, subtile Bewegung** animiert die Balken beim Laden oder beim Scroll (leichte Verschiebung auf der Y-Achse, unterschiedliches Timing per Balken)
- Auf Mobile: Reduktion auf 3 Balken oder Übergang in vertikale Vollbreite

### Hero-Inhalt

| Element | Position | Beschreibung |
|---------|----------|--------------|
| Hintergrundbild | Vollflächig, durch Masken sichtbar | München-Panorama oder Architektur-Motiv |
| H1 | Im Textbalken (2 oder 4), 90° rotiert von unten nach oben | Kurz, präzise – max. 4–5 Wörter |
| Subline | Unterhalb der H1 im selben Balken, ebenfalls rotiert | Positionierungsaussage |
| CTA | Am unteren Ende des Textbalkens | Primär-Button (horizontal, normal lesbar) |
| Trust-Badges | Unterhalb der Balken, volle Breite | „Seit 1922 · München · 100+ Jahre" |

### CSS-Grundlage Textbalken

```css
.hero-text-bar {
  writing-mode: vertical-rl;
  transform: rotate(180deg);   /* → liest von unten nach oben */
  text-orientation: mixed;
}
```

---

## Scroll-Experience & Storytelling

Die Seite wird nicht gelesen – sie wird **erlebt**. Der Scroll ist kein Navigationsmittel, er ist der **Erzählrhythmus**.

### Prinzipien

- **Smooth Scrolling** – kein hartes Springen zwischen Sektionen
- **Elemente entstehen**, sie erscheinen nicht einfach – Fade, leichtes translateY, Timing gestaffelt
- **Sections lösen sich auf** und gehen ineinander über – kein hartes Raster-Ende
- **Fluid Transitions** zwischen Inhaltsbereichen: Farb- und Bildübergänge folgen dem Scroll
- **Narrative Logik:** Jede Section beantwortet die Frage, die die vorherige aufgeworfen hat

### Scroll-Effekte (erlaubt & erwünscht)

| Effekt | Trigger | Umsetzung |
|--------|---------|-----------|
| Hero-Balken Einfahrt | Page Load | CSS Keyframes, gestaffeltes Delay je Balken |
| Hero-Balken Parallax (subtil) | Scroll | CSS `transform: translateY` via JS scroll-listener |
| Section-Elemente fade-in + rise | Intersection Observer | CSS Transition + translateY(24px → 0) |
| Text-Reveal gestaffelt | Scroll in Viewport | Staggered Animation, children mit delay |
| Trust-Counter hochzählen | Scroll in Viewport | Kleines JS-Snippet |
| Sticky-Header | Scroll > 80px | CSS-Klasse per JS |
| Bild Lazy-Load Fade | Intersection Observer | CSS opacity |
| Nav-Unterstrich | Hover | CSS `::after` Transform scaleX |
| Akkordeon öffnen/schliessen | Klick | CSS max-height Transition |

> **Alle Animationen respektieren `prefers-reduced-motion: reduce`.**
> Performance-Budget: Keine Animation darf Layout-Recalculation triggern → ausschliesslich `transform` und `opacity`.

### Verboten (Performance & Fokus)

- ❌ GSAP, Framer Motion, Locomotive Scroll *(Library-Overhead)*
- ❌ Page Transitions (Barba.js)
- ❌ Custom Cursor
- ❌ Exzessiver Parallax (Hintergrundbilder die bei jedem Scroll-Pixel neu rechnen)
- ❌ Video-Backgrounds
- ❌ Scroll-Hijacking (natürlicher Scroll-Flow muss erhalten bleiben)

---

## Fluid Layout — kein Row-Denken

Die Seite folgt keiner klassischen „Section nach Section"-Logik. Stattdessen:

- **Elemente überlappen** bewusst Section-Grenzen (Cards die aus einer Section in die nächste ragen)
- **Hintergründe wechseln graduell**, nicht abrupt (CSS `background-attachment`, sanfte Farbübergänge)
- **Asymmetrie ist erlaubt**: Nicht jede Section ist zentriert oder gleichmässig aufgeteilt
- **Negative Space ist aktiv**: Weißraum wird platziert, nicht als Lücke toleriert
- **Schrift kann gross sein**: Headlines dürfen die Bildschirmbreite füllen, wenn der Inhalt es trägt

### Layout-Archetypen (statt starrer Rows)

| Typ | Beschreibung | Einsatz |
|-----|-------------|---------|
| **Vollbild-Anker** | Volle Viewporthöhe, ein dominantes Element | Hero, Key-Statements |
| **Offset-Grid** | Bild und Text überlappen, unterschiedliche Startpunkte | Leistungsbereiche |
| **Floating Cards** | Cards ohne expliziten Container-Rahmen | Referenzen, Team |
| **Text-Dominant** | Grosser Weißraum, wenig Elemente, viel Luft | Zitate, USP-Statements |
| **Dichte Kachel** | Strukturiertes Raster für viele gleichwertige Items | Mietobjekte, News |

---

## München-Identität im Design

### Leitprinzip: „Laptop und Lederhose"

München ist keine bayerische Klischeestadt – es ist eine der modernsten Metropolen Europas, die gleichzeitig tief in ihrer Geschichte verwurzelt ist. Das Design spiegelt genau das: **urban, zeitgemäss, weltgewandt – und unverkennbar münchnerisch.**

Was das bedeutet:

| Erwünscht | Verboten |
|-----------|----------|
| Skyline-Silhouette als grafisches Mittel | Weissblaue Rauten, Bierkrug-Assoziationen |
| Stadtteile als Orientierungspunkte | Touristisches Postkarten-München |
| Zeitgeschichte als Substanz | Folklore-Ästhetik |
| Architektonische Präzision | Gemütlichkeits-Kitsch |
| Modernes München mit Tiefe | Beliebige Großstadt-Optik |

---

### Outline-Skyline als grafisches Element

Die Münchner Skyline – Frauenkirche, Olympiaturm, Theatinerkirche, Maximilianeum – wird als **reduzierte Outline-Grafik (SVG)** eingesetzt. Kein illustrativer, dekorativer Stil – sondern architektonisch präzise, minimalistisch, auf Linie reduziert.

**Einsatzmöglichkeiten:**

| Position | Verwendung | Stil |
|----------|------------|------|
| Hero-Bereich | Als horizontale Silhouette am unteren Bildrand | Weiss/transparent auf dunklem Overlay |
| Section-Trenner | Subtile Skyline-Linie als Divider | `--color-border` oder `--color-primary` mit sehr niedriger Opacity |
| Über-uns-Seite | Grossformatig, historisch codiert (1922 → heute) | Kombination mit Jahreszahl-Typografie |
| Footer | Schmal, als dekoratives Element | Weiss auf `--color-dark` |

**Stilregel:** Die Skyline ist immer **Linie, nie Fläche** – `stroke`, kein `fill`. Dünn, präzise, zurückhaltend. Sie unterstreicht, sie dominiert nicht.

```
Frauenkirche  Theatiner  Maximilianeum  Olympiaturm  …
    ╱╲              ╱\        ┌──┐          │
   ╱  ╲            ╱  \       │  │          │
──╱────╲──────────╱────\──────┤  ├──────────┼──────────
```

---

### Lokaler Bezug: Stadtteile

Rudolf Schäfer KG kennt jeden Münchner Stadtteil – das ist ein konkreter Wettbewerbsvorteil. Das Design macht ihn sichtbar:

- **Stadtteil-Seiten** (SEO-Cluster) haben je ein authentisches Motiv des Stadtteils – kein Stock-Photo, sondern erkennbare Architektur
- **Referenz-Objekte** werden mit Stadtteil-Kontext verknüpft (Schwabing, Maxvorstadt, Bogenhausen, Haidhausen …)
- **Kartografische Elemente** sind möglich: eine reduzierte München-Karte als interaktives Element auf der Über-uns-Seite, das die verwalteten Stadtteile zeigt

---

### Geschichte als Design-Substanz

Das Unternehmen hat München in seinen prägenden Jahrzehnten begleitet. Das darf sichtbar werden – als Substanz, nicht als Nostalgie:

- **Timeline-Element** auf der Über-uns-Seite: 1922 – Kriegsjahre – Wiederaufbau – Wirtschaftswunder – Gegenwart
- **Historische Fotografie** (wenn vorhanden): schwarz-weiss, als Kontrast zu heutigen Aufnahmen
- **Jahreszahlen typografisch** gross eingesetzt (`--font-display`, Playfair Display) als gestalterisches Mittel
- **„Seit 1922"** nicht als Floskel, sondern als wiederkehrendes visuelles Ankerelement

---

## Design-Grundprinzipien (technisch)

Die neue Website übernimmt das bestehende Farbsystem der Rudolf Schäfer KG – kein Bruch mit der Markenidentität, sondern technisch saubere Weiterentwicklung als CSS Design-Tokens.

- **Mobile First** – alle Designs zuerst für Mobile konzipieren
- **Performance-Design** – Animationen ausschliesslich über `transform` + `opacity`, kein Layout-Thrashing
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

## Offene Design-Fragen

- [ ] Logo: SVG-Dateien in allen Varianten vorhanden? (Quer hell/dunkel, Hoch hell/dunkel)
- [ ] Corporate Design Manual vorhanden?
- [ ] Foto-Shooting: Stil-Briefing abstimmen
- [ ] Kalligraphie-Schrift des Logos identifizieren (ggf. für Headline-Akzente)
