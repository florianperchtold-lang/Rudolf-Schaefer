# 00_ROADMAP — Projektfahrplan
<!-- Rudolf Schäfer KG | Website-Relaunch 2026 -->
<!-- Letzte Aktualisierung: April 2026 -->

---

## Projektübersicht

| | |
|--|--|
| **Projekt** | Website-Relaunch rudolfschaefer.de |
| **Auftraggeber** | Rudolf Schäfer KG, München |
| **Agentur** | perchtold.studio |
| **SEO** | Robert Eberhard, cult consult |
| **Ziel** | Kompletter Neubau – SEO/GEO-Dominanz München |
| **Stack** | WordPress + Bricks Builder + ACF + Claude Code |

---

## Offene Entscheidungen (zuerst klären)

Diese Fragen müssen beantwortet sein bevor Phase 2 starten kann:

- [ ] **Builder-Lizenz:** Bricks Builder Lifetime kaufen – oder Breakdance/Oxygen als günstigere Alternative?
- [ ] **ACF:** Free oder Pro? (Repeater-Felder benötigt → vermutlich Pro)
- [ ] **Mehrsprachigkeit:** WPML oder Polylang?
- [ ] **Mietangebote:** OnOffice API verfügbar? Oder Immobilie1 API direkt?
- [ ] **Newsletter-System:** Welche Plattform aktuell? 5.921 Abonnenten exportierbar?
- [ ] **Hosting:** Plesk-Plan prüfen – Node.js verfügbar? PHP 8.1+ mit Imagick/AVIF?
- [ ] **Fairrank:** Vertrag kündigen / Übergabe an Robert Eberhard koordinieren
- [ ] **Logo:** SVG-Dateien in allen Varianten beschaffen
- [ ] **Partnerschaften:** Welche Partner sollen auf der Website erscheinen?

---

## Phase 1 – Planung & Vorbereitung
**Status: läuft**

| Aufgabe | Verantwortlich | Status |
|---------|---------------|--------|
| SEO IST-Analyse | Robert Eberhard | ✅ fertig |
| Projektdokumentation (01–07, 08) | perchtold.studio | ✅ fertig |
| Stack-Entscheidung WordPress + Bricks + ACF | perchtold.studio | ✅ entschieden |
| GitHub Repository einrichten | perchtold.studio | ✅ fertig |
| Offene Entscheidungen klären (siehe oben) | Kunde + Agentur | ⏳ offen |
| Content-Briefings je Seite schreiben | perchtold.studio + Eberhard | ⏳ offen |
| Keyword-Recherche vollständig | Robert Eberhard | ⏳ offen |
| Foto-Shooting terminieren (25 Portraits + Büro) | Kunde | ⏳ offen |
| Logo SVG-Dateien beschaffen | Kunde | ⏳ offen |
| Partnerschaften klären | Kunde | ⏳ offen |

---

## Phase 2 – Design (Google Stitch)
**Status: noch nicht gestartet**

| Aufgabe | Verantwortlich | Status |
|---------|---------------|--------|
| Design-Referenzen sammeln (Dribbble, awwwards) | perchtold.studio | ⏳ |
| Stitch-Prompts je Seite erstellen | perchtold.studio + Claude | ⏳ |
| Startseite designen | perchtold.studio | ⏳ |
| Unterseiten designen (Hausverwaltung, Vermietung, Verkauf) | perchtold.studio | ⏳ |
| Design-Review mit Kunde | Kunde + Agentur | ⏳ |
| Design freigeben | Kunde (Julie / Martin Schäfer) | ⏳ |

---

## Phase 3 – Lokale Entwicklung
**Status: noch nicht gestartet**

| Aufgabe | Verantwortlich | Status |
|---------|---------------|--------|
| Local by Flywheel einrichten | perchtold.studio | ⏳ |
| WordPress + Bricks + ACF installieren | perchtold.studio | ⏳ |
| `.claude/skills/` einrichten (WP Skills) | perchtold.studio | ⏳ |
| MCP einrichten (Novamira o.ä.) | perchtold.studio | ⏳ |
| design-tokens.css erstellen | Claude Code | ⏳ |
| Globale Komponenten (Header, Footer, Nav) | Claude Code | ⏳ |
| Bricks-Templates je Block-Typ | Claude Code | ⏳ |
| ACF-Feldgruppen definieren | Claude Code | ⏳ |
| Custom Post Types (Team, Immobilien, News) | Claude Code | ⏳ |
| Seiten-Templates | Claude Code | ⏳ |
| Kontaktformular (eigener Code) | Claude Code | ⏳ |
| Klaro.js Cookie-Banner | Claude Code | ⏳ |
| Leaflet.js Karte | Claude Code | ⏳ |
| Schema.org automatisch aus ACF | Claude Code | ⏳ |

---

## Phase 4 – Bild-Workflow
**Status: noch nicht gestartet**

| Aufgabe | Verantwortlich | Status |
|---------|---------------|--------|
| Foto-Shooting durchführen | Kunde | ⏳ |
| Originale in Ordner sortieren (team/objekte/buero) | perchtold.studio | ⏳ |
| Node.js Bild-Skript ausführen (sharp + Claude API) | perchtold.studio | ⏳ |
| KI-Metadaten (Alt-Texte, Titel) QS + korrigieren | perchtold.studio | ⏳ |
| Bilder per WP-CLI in WordPress importieren | perchtold.studio | ⏳ |

---

## Phase 5 – Content
**Status: noch nicht gestartet**

| Aufgabe | Verantwortlich | Status |
|---------|---------------|--------|
| ACF Settings-Singleton befüllen (Firmendaten) | perchtold.studio | ⏳ |
| SEO-Texte schreiben (alle Seiten nach Briefings) | perchtold.studio + Eberhard | ⏳ |
| Stadtteiltexte (8 Seiten à 500–700 Wörter) | perchtold.studio | ⏳ |
| Team-Daten einpflegen (25 Personen) | perchtold.studio | ⏳ |
| FAQ einpflegen (Mieter + Eigentümer) | perchtold.studio | ⏳ |
| Testimonials einpflegen | perchtold.studio | ⏳ |
| Timeline (15 Meilensteine) einpflegen | perchtold.studio | ⏳ |
| Mietangebote-Integration einrichten | perchtold.studio | ⏳ |
| EN-Übersetzung aller Seiten | perchtold.studio | ⏳ |
| Impressum + Datenschutz aktualisieren | Rechtsanwalt | ⏳ |

---

## Phase 6 – Staging & QA
**Status: noch nicht gestartet**

| Aufgabe | Verantwortlich | Status |
|---------|---------------|--------|
| Local → Staging pushen (staging.rudolfschaefer.de) | perchtold.studio | ⏳ |
| Lighthouse messen – Ziel: Desktop > 90, Mobile > 80 | perchtold.studio | ⏳ |
| Core Web Vitals – alle grün | perchtold.studio | ⏳ |
| Mobile Testing (iPhone + Android) | perchtold.studio + Kunde | ⏳ |
| Barrierefreiheit prüfen (WCAG 2.1 AA) | perchtold.studio | ⏳ |
| Security-Check (Wordfence + Headers) | perchtold.studio | ⏳ |
| Schema.org validieren | perchtold.studio | ⏳ |
| hreflang + Redirects testen | perchtold.studio | ⏳ |
| Alle EN-Links prüfen | perchtold.studio | ⏳ |
| Notion MCP Checklist durcharbeiten | perchtold.studio | ⏳ |
| Finale Freigabe | Kunde (Julie / Martin Schäfer) | ⏳ |

---

## Phase 7 – Go-Live
**Status: noch nicht gestartet**

| Aufgabe | Verantwortlich | Status |
|---------|---------------|--------|
| 301 Redirect-Map aktivieren und testen | perchtold.studio | ⏳ |
| robots.txt: Staging sperren, Prod freigeben | perchtold.studio | ⏳ |
| Staging → rudolfschaefer.de deployen | perchtold.studio | ⏳ |
| Google Search Console verbinden | Robert Eberhard | ⏳ |
| Sitemap einreichen | perchtold.studio | ⏳ |
| Google Business Profile URL aktualisieren | Robert Eberhard & Rudolf Schäfer KG | ⏳ |
| Analytics einrichten + testen (Matomo oder Google Analytics – Entscheidung Robert Eberhard) | Robert Eberhard | ⏳ |
| Verzeichnisse aktualisieren (muenchen.de, IVD etc.) | Robert Eberhard | ⏳ |
| Robert Eberhard: Post-Launch SEO-Monitoring | Robert Eberhard | ⏳ |

---

## Kontakte

| Person | Rolle | Kontakt |
|--------|-------|---------|
| Martin Schäfer | Komplementär, Auftraggeber | m.schaefer@rudolfschaefer.de |
| Julie Schäfer | Ansprechpartnerin Website | juliekoessler@yahoo.de |
| Florian Perchtold | Agentur perchtold.studio | post@perchtold.studio |
| Robert Eberhard | SEO, cult consult | robert.eberhard@cult-consult.com |

---

## Dokumente

| Datei | Inhalt |
|-------|--------|
| `00_ROADMAP.md` | Dieser Fahrplan |
| `01_BRIEF.md` | Strategie, USPs, Zielgruppen, Tone of Voice |
| `02_DESIGN.md` | Farben, Typografie, Komponenten |
| `03_TECHSPEC.md` | Stack, Workflow, Plugin-Philosophie, Security |
| `04_CONTENT.md` | Alle Seiteninhalte, CPT-Struktur, News-Strategie |
| `05_SEO.md` | Pillar-Cluster, Keywords, Redirects, Eberhard-Strategie |
| `06_ASSETS.md` | Logos, Fotos, Icons, Schriften, Naming |
| `07_ARCHITEKTUR.md` | Kein Hardcoding, Bild-Workflow, Token-Effizienz |
