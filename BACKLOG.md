# Backlog – One-Pager Website Template

## Letzter Stand

**Version:** v1.6.1 (gepusht)  
**Zuletzt abgeschlossen:** Issues #7, #8, #13 — Rate Limiting, IBAN DSGVO-Hinweis, update.sh fix

### Abgeschlossen in dieser Session

**Issue #13 — `update.sh`: git pull ohne Tracking-Branch**
- `setup/update.sh` — `git pull` → `git pull origin main`

**Issue #8 — IBAN UX-Verbesserung (DSGVO)**
- `templates/partials/forms/sepa.php` — Hinweistext unter IBAN-Feld (openiban.com)
- `public/assets/css/main.css` — `.form-hint`-Klasse ergänzt
- `content/legal/datenschutz.md` — vollständiger Mustertext mit allen template-spezifischen Abschnitten (Session-Cookie, Kontaktformular, SEPA, openiban.com, Betroffenenrechte)
- `README.md` — Hinweis auf vorausgefüllten Datenschutz-Mustertext

**Issue #7 — Rate Limiting für Formulare**
- Bereits implementiert in `src/http/FormEndpoint.php` — Issue als erledigt geschlossen

---

### Abgeschlossen in vorherigen Sessions

**Issue #12 — `{{VAR_NAME}}`-Platzhalter in `$md()`**
- `public/index.php` — `$md()` führt nach Markdown-Rendering denselben Placeholder-Replace-Pass durch wie `$gallery()`

**Paket D1–D3** — Content-Infrastruktur, A11y, SEPA

**Paket E — Templates/CSS/htaccess**
- `impressum.php` + `datenschutz.php` → `$md()`, LCP-Preload, Footer „Start"-Link
- CSS 600px-Breakpoint (Gallery 1-col, Lightbox nav ausblenden)
- `.htaccess` Gzip + Cache-Control

**Paket F — Hintergrundbilder + CSS-Tokens**
- `body_bg.jpg` Placeholder, `--bg-image-*`, `--color-text-hero`, `--font-display`
- body/section.alt/hero mit Hintergrundbildern + Overlays
- Dark-Mode Overlays für alle Sektionen
- Gallery 900px→2-col Breakpoint, MAIL_FROM_NAME aus .env

**Testzahlen gesamt:**
- PHP Unit: 55 Tests · JS Jest: 101 Tests · Integration: 7 Tests

---

## Offene Issues

Keine repo-eigenen offenen GitHub-Issues. SEPA-Flow (rechtlich) und Logging-Strategie (DEV vs.
PROD) sind Template-Themen und werden ausschließlich in `oeme-github/websitetemplate` als Issues
#1 und #5 getrackt (weiterhin offen dort) — nicht hier duplizieren, siehe `CLAUDE.md`.

- **buero-desk-booking-landing_D03** (neu 2026-09-30, gefunden bei der Impressum-Umstellung TMG → DDG,
  dev-notes-Hub-Session): Der Server-Checkout auf netcup (`/var/www/buero-desk-booking-landing`)
  steht auf `1aadbb4` (Juni) und damit weit hinter `main`. Die Live-Seite zeigte ihr Impressum nur,
  weil die dortige alte `impressum.example.md` noch echte Daten enthielt — im aktuellen Repo ist sie
  (nach Template-Merge) ein Platzhalter, ein `git pull` hätte Platzhalter veröffentlicht. Behoben
  durch serverlokale `content/legal/impressum.md` (Stand wie lokal, „§ 5 DDG“, bewusst nicht
  committet). Offen: Server-Checkout kontrolliert auf `main` bringen (vorher `git status`/Diff
  prüfen, `datenschutz.md` ist ebenfalls serverlokal), Deploy-Weg dokumentieren
  (`DEPLOYMENT.md`), `websitetemplate`-Stand v1.7.0 + DDG-Fix (`6ac1482`) mergen.

- **buero-desk-booking-landing_D04** (neu 2026-10-12, dev-notes-Hub, Prüfung Demo-Modus ↔ Admin-VPN):
  Die Kopfzeile verlinkt „Admin“ auf `admin.buero-desk-booking.de` — seit `euviaio_F70` nur per
  Admin-VPN erreichbar, Besucher landen auf 403. **User-Entscheidung 2026-10-12 (Tendenz A):** Admin
  aus der Demo nehmen — Admin-Link aus der Kopfzeile entfernen, stattdessen den Admin-Teil auf der
  Landingpage mit ein paar Screenshots zeigen (Galerie, `content/home/gallery.json` serverlokal bzw.
  Inhalt, Bilder aus der Demo-Instanz, keine echten Personendaten). Gegenstück in der App:
  `buero-desk-booking_D99` (Demo-Admin-Anmeldung abschalten); Hintergrund `euviaio_F118`. Reihenfolge:
  nach `D03` (Server-Checkout auf `main`). Instanz-Matrix: Landingpage `buero-desk-booking.de`
  (netcup · PROD; kein STAGING/TEST vorhanden — lokal per `php -S` prüfen).

---

## Zurückgestellt

- **Screenreader-Test SEPA-Formular**: manueller Test (NVDA/VoiceOver) — kein Code-Task
- **buero-desk-booking-landing_D01**: CLAUDE.md auf dev-notes-Template umstellen — eigene
  englische Struktur, keine STANDARDS.md-Referenz, WSL2 noch als primäre Umgebung beschrieben
  plus toter Windows-Mirror-Sync-Schritt (`/mnt/f/git_repos/...`, seit WSL-Ablösung 2026-09-02
  nicht mehr funktionsfähig). Gemeinsam mit `friendsofthehawks`/`websitetemplate` zu betrachten
  (gemeinsame `websitetemplate`-Abstammung). Siehe `dev-notes/BACKLOG.md` D08, `dev-notes_F02`.
  **✅ Erledigt (2026-09-05):** Komplett neu geschrieben nach dem neuen „Code-Template-Ableitung"-
  Muster (`dev-notes/STANDARDS.md` §3) — Architektur/Setup/Testing/Dependencies nicht mehr
  dupliziert, nur noch Verweis auf `websitetemplate` + echte instanzspezifische Fakten. Dabei
  entdeckt: `CLAUDE.md` referenzierte durchgehend falsche Pfade/Configs von `websitetemplate`
  selbst statt der eigenen (nie angepasster Copy-Paste-Rest) — jetzt korrigiert.
- **buero-desk-booking-landing_D02** (neu, gefunden bei D01): `README.md` ist noch die
  unveränderte generische Template-Beschreibung („One-Pager Website Template", „Use this
  template"-Anleitung) statt repo-spezifisch angepasst zu sein. Zusätzlich liegt eine ungenutzte
  `setup/apache/websitetemplate.conf` neben der tatsächlich verwendeten
  `buero-desk-booking-landing.conf` — vermutlich derselbe nie aufgeräumte Klon-Rest. Aufräumen
  (README anpassen oder bewusst als Ausnahme dokumentieren, tote Config-Datei entfernen).
