## [Unreleased]

### Added

#### Session 2026-06-05 — Logos und Favicons

- `public/assets/logo/` — alle 6 Logo-Varianten neu erstellt: `logo_mark`, `logo_mark_white`, `logo_primary`, `logo_primary_white`, `logo_secondary`, `logo_secondary_white`; ersetzen Inkscape-Platzhalter (Baum-SVG); Basis ist das Desk-Booking-Icon (blaues Quadrat, Schreibtisch, Kalender, Häkchen); Wordmark-Varianten mit „Desk Booking" in Inter Bold (zweifarbig: Blau + Dunkelgrau); weiße Varianten für dunkle Hintergründe
- `public/assets/icons/` — `icon.svg` ersetzt (war 61 KB Inkscape-Datei); alle PNG-Favicons (`16×16`, `32×32`, `apple-touch-icon 180px`, `android-chrome 192/512px`) und `favicon.ico` neu aus korrektem SVG gerendert (Inkscape)

### Fixed

#### Session 2026-06-05 — Tippfehler in `.env`

- `.env` — `APP_ULR` → `APP_URL` korrigiert; verhinderte dass `{{APP_URL}}`-Placeholder in `topbar-links.json` ersetzt wurde

---

## v1.6.0 – Section Flags

### Added
- **Section Flags**: Jede Hauptsektion der Startseite ist einzeln über `.env` de-/aktivierbar (`SECTION_HERO`, `SECTION_GALLERY`, `SECTION_STATS`, `SECTION_ABOUT`, `SECTION_CONTACT`)
- `$section()`-Closure in `index.php` — liest `SECTION_*` aus `.env`, Default ist `true` (aktiviert)
- `.env.example` dokumentiert alle fünf Flags

### Design-Entscheidungen
- Default `true`: Deployments ohne explizite Flags verhalten sich unverändert
- Lightbox wird zusammen mit `SECTION_GALLERY` ein-/ausgeblendet (logische Einheit)
- Flags steuern nur Rendering — kein JS, kein CSS-Aufwand für deaktivierte Sections

---

## v1.3.0 – Color Schemes, Cookie Notice, Gallery, Stats & Testing

### Added
- **Color Scheme System**: RGB-basierte CSS Custom Properties mit 3 austauschbaren Schemas (Default, Warm, Nature)
- **FOUC Prevention**: `fouc-prevention.js` verhindert Theme-/Schema-Flash beim Laden
- **Cookie Notice**: DSGVO-konformer Cookie-Hinweis mit Dismiss-Button und localStorage-Persistenz
- **Color Scheme Selector**: `<select data-color-scheme-select>` im Footer, persistent via localStorage
- **Stats Counter**: Count-Up-Animation mit Intersection Observer und `prefers-reduced-motion`-Support
- **Image Gallery + Lightbox**: Vollständige Galerie-Komponente mit Keyboard-Navigation, Focus-Trap und Tabs
- **Gallery Tabs**: Dynamischer Kategoriefilter aus `data-gallery-category` Attributen
- **Content-Management**: Parsedown-Dependency + `$md()` / `$gallery()` Loader in `index.php`; `content/`-Verzeichnis mit Placeholder-Dateien
- **Testing-Infrastruktur**: PHPUnit 10 (48 Tests) + Jest 29 (86 Tests); `phpunit.xml`, `package.json`
- Favicon-Links und LCP-Preloads in `base.php`

### Changed
- **Security Headers**: `headers.php` refaktoriert zu `setBaseSecurityHeaders()`, `setApiSecurityHeaders()`, `setHtmlSecurityHeaders()`
- `index.php`: ruft `setHtmlSecurityHeaders()` als erste Aktion auf
- `send_kontakt.php` / `send_sepa.php`: rufen `setApiSecurityHeaders()` als erste Aktion auf
- `.env.example`: SMTP_* → MAIL_*, neue Variable `MAIL_TO`, Typo-Fixes
- Form-Erfolgsmeldung faded nach 5 Sekunden automatisch aus
- CSS Custom Properties auf RGB-Tupel-System umgestellt (Alpha-Support)

### Quality
- Alle bestehenden Features erhalten (kein Breaking Change für Browser-Nutzer)
- `.env`-Nutzer: `SMTP_*` → `MAIL_*` umbenennen (Breaking)

---

## v1.2.1 – SEPA Form Layout & UX Fixes

### Fixed
- Incorrect desktop layout of SEPA form fields
- Misaligned select fields due to nested label/select markup
- Inconsistent consent checkbox alignment in SEPA form

### Improved
- Unified form field structure between contact and SEPA forms
- Robust grid behavior for desktop view without layout side effects
- Consent checkboxes now stack vertically and behave consistently across viewports

### Quality
- No breaking changes
- No JavaScript changes required
- Accessibility preserved (label wrapping, focus order, click targets)

---

## v1.2.0 – Forms, Security & UX Finalization

### Added
- Optionales **SEPA-Formular** als Alternative zum Kontaktformular
  - Umschaltbar über `.env` (`FORM_TYPE=contact|sepa`)
  - Gemeinsame Formular-Architektur mit austauschbaren Partials
- SEPA-Mailversand mit:
  - serverseitiger Validierung
  - IBAN-Prüfung
  - automatisch generiertem **SEPA-PDF** als E-Mail-Anhang
- Zentrale Environment-Steuerung (DEV / PROD) über `APP_ENV`
- Einheitliche JSON-Response-Architektur für alle Formular-Endpunkte

### Improved
- UX-Feinschliff für Header & Navigation:
  - Header blendet sich beim Scrollen aus/ein (scroll down / up)
  - Mobile Menü schließt zuverlässig bei:
    - Scroll
    - Seitenwechsel
    - Navigation über Logo/Home-Link
- Footer dauerhaft am unteren sichtbaren Rand fixiert
- Formular-UX:
  - konsistentes ARIA-Feedback bei Fehlern & Erfolg
  - robuster AJAX-Flow mit klarer Fehlerbehandlung
- Klarere Trennung von:
  - Routing
  - Layout
  - Formular-Logik
  - Business-Logik (Mail, PDF)

### Security
- Vereinheitlichte Security-Baseline:
  - CSRF-Schutz mit Token-Rotation
  - Honeypot-Mechanismus
  - Whitelist-basiertes Routing
  - konsistente HTTP-Statuscodes
- Globale Error- & Exception-Handler für API-Endpunkte
- Kein Information Leakage in Produktionsumgebung

### Quality
- Stabiler Formular-Flow für Kontakt **und** SEPA
- Alle bekannten Edge-Cases im Mobile-Menü behoben
- Codebasis bereinigt und dokumentiert
- Keine Breaking Changes für bestehende Nutzer

---

**Status:** Stable

---

## v1.1.0 – Legal Pages & Layout Refinement

### Added
- New legal pages: Impressum and Datenschutzerklärung
- Consistent global header and footer across all pages
- Footer redesigned using responsive CSS Grid

### Improved
- Legal content layout with dedicated `.section-legal`
- Removed scroll-snap from legal pages
- Improved mobile readability for long headings
- Reduced footer height on mobile
- Mobile viewport handling using modern `svh/dvh`

### Quality
- Lighthouse: 100 / 100 / 100 / ~98
- No breaking changes

---

## v1.0.0 – Initial Release

Erste stabile Version des One-Pager-Templates.

### Highlights
- Barrierearmer One-Pager mit klarer HTML-Struktur
- Responsive Header mit Desktop- & Mobile-Navigation
- Barrierefreies Mobile-Menü mit korrektem ARIA-State
- Kontaktformular mit:
  - CSRF-Schutz
  - Honeypot gegen Bots
  - serverseitiger Validierung
  - AJAX-Submit mit ARIA-Feedback
- Dark-/Light-Theme über CSS Custom Properties
- Saubere Trennung von HTML, CSS, JavaScript und PHP

### Qualität & Standards
- Lighthouse:
  - Performance: 98
  - Accessibility: 100
  - Best Practices: 100
  - SEO: 100
- Frameworkfreies Setup (Vanilla JS / PHP)
- PHP ≥ 8 mit Composer (PHPMailer)
- Sichere PHP-Endpunkte via `.htaccess`

### Dokumentation
- Vollständige README mit Deployment-Hinweisen
- CONTRIBUTING.md für externe Beiträge
- MIT License

### Hinweise
Dieses Release dient als stabiler Ausgangspunkt.
Anpassungen an Design, Inhalt oder Struktur sollten stets mit einer erneuten Accessibility-Prüfung einhergehen.

---

**Status:** Stable
