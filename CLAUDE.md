# CLAUDE.md – buero-desk-booking-landing

## Verbindlicher Arbeitsablauf

Der vollständige Arbeitsablauf (Sprache, Startup-Routine, Arbeit im Projekt, Session-End-Routine)
steht **ausschließlich** in `dev-notes/STANDARDS.md` §1–§4 — automatisch per `@`-Import geladen
(siehe „Automatisch geladene Dateien" unten), hier nicht redundant wiederholen. Die Abschnitte
unten enthalten nur **projektspezifische Ergänzungen und Fakten**.

**Downstream-Klon von [`oeme-github/websitetemplate`](https://github.com/oeme-github/websitetemplate)**
(`git remote template`, periodisch per `git merge template/main` nachgezogen). Architektur,
Security-Model, Code-Standards, Testing-Aufbau, Dependencies und generisches Lokal-Setup sind
identisch mit dem Template und stehen **ausschließlich dort** (`dev-notes/STANDARDS.md` §3,
„Single Source of Truth" — Kategorie Code-Template-Ableitungen). Fehler/Verbesserungen an diesen
Themen als Issue/PR bei `websitetemplate` einreichen, nicht hier reparieren.

## Entwicklungsumgebung

Gemeinsame Devbox-Umgebung: siehe `dev-notes/REPOS.md` („Speicherorte"). Generisches Lokal-Setup
(Apache/Mailpit/Abhängigkeiten): siehe `websitetemplate`s `CLAUDE.md`.

- **Projektpfad (Devbox):** `~/git_repos/buero-desk-booking-landing`
- **Versionskontrolle:** Git, Remote `origin` = `github.com/oeme-github/buero-desk-booking-landing`,
  Remote `template` = `github.com/oeme-github/websitetemplate`
- **Web root:** `public/` — Apache-Vhost: `setup/apache/buero-desk-booking-landing.conf`
  (`setup/apache/websitetemplate.conf` in diesem Repo ist ein ungenutzter Rest vom Template-Klon,
  siehe `buero-desk-booking-landing_D02`)
- **Zweck dieser Instanz:** Landing Page für `buero-desk-booking.de`

### Startup-Routine — projektspezifische Ergänzungen
Generischer Kern: siehe `dev-notes/STANDARDS.md` §2. Keine zusätzlichen Schritte für dieses
Projekt.

---

## Session-End-Routine — projektspezifische Ergänzungen
Generischer Kern: siehe `dev-notes/STANDARDS.md` §4. Keine zusätzlichen Schritte für dieses
Projekt (der frühere Windows-Mirror-Sync-Schritt ist seit der WSL-Ablösung 2026-09-02
gegenstandslos und entfällt).

## Automatisch geladene Dateien (via `@`-Import)
- @BACKLOG.md — **zuerst lesen**: enthält letzten Stand und wo weitermachen
- @README.md — Projektübersicht und Setup
- @CHANGELOG.md — Versionshistorie und aktuelle Änderungen
- @~/git_repos/dev-notes/STANDARDS.md — verbindlicher, projektübergreifender Arbeitsablauf
  (Hub-Regelwerk; externer Import außerhalb dieses Projekts — Claude Code zeigt beim allerersten
  Laden einen einmaligen Genehmigungsdialog, danach automatisch)

---

## Doku-Check (alle 4 Wochen)
Dedizierte Session zur Synchronisierung der Dokumentation mit dem tatsächlichen Projektstand:
- `CLAUDE.md` — nur noch instanzspezifische Fakten hier; ist seit dem letzten `git merge
  template/main` noch alles mit `websitetemplate`s Stand konsistent?
- `README.md` — ist sie noch die generische Template-Beschreibung, oder repo-spezifisch
  angepasst? (siehe `buero-desk-booking-landing_D02`)
- `BACKLOG.md` — erledigte Einträge bereinigen, neue Erkenntnisse ergänzen; IDs auf
  `<repo>_<ID>`-Konvention prüfen (siehe `dev-notes/STANDARDS.md`) — inkl. Querverweise in
  `dev-notes/PROJECTS.md`/`dev-notes/projects/buero-desk-booking-landing.md`

Nächster Doku-Check: **2026-10-03**

---

## Verwandte Repositories

| Repo | Zweck |
|------|-------|
| `oeme-github/dev-notes` | PM-Hub, Projektübersicht |
| `oeme-github/websitetemplate` | Template-Ursprung — Architektur/Setup/Bugs dort, nicht hier |
| `oeme-github/friendsofthehawks` | Anderer Downstream-Klon desselben Templates |
