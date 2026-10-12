# Deployment – buero-desk-booking-landing

Nur was für diese Installation gilt. Generischer Ablauf (Ersteinrichtung, `setup/update.sh`,
Troubleshooting): `DEPLOY.md` aus `websitetemplate`. Auf welchem Server die Seite läuft:
`dev-notes/ops/server-landschaft.md` (netcup; im Host-Manifest `euviaio/installations/_hosts/netcup.yaml`
als `vhosts_fremd`).

## Update auf PROD

Lokal entwickeln, auf `main` pushen, dann auf dem Server (Account `deploy`, Checkout
`/var/www/buero-desk-booking-landing`, Branch `main`):

```bash
cd /var/www/buero-desk-booking-landing
git status --short          # erwartet: nur die serverlokalen Dateien unten
bash setup/update.sh        # git pull + composer install --no-dev
```

Danach von außen prüfen: Startseite, `/impressum`, `/datenschutz`, Urheber-Vermerk im Footer.
Es gibt kein STAGING und keinen TEST — vorher lokal prüfen (`php -S`, siehe `websitetemplate`).

## Serverlokale Dateien (nie committen, nie überschreiben)

| Datei | Inhalt |
|---|---|
| `.env` | Konfiguration der Instanz |
| `content/legal/impressum.md` | Impressum (§ 5 DDG) mit echten Daten |
| `content/legal/copyright.json` | Urheber im Footer |

`content/legal/datenschutz.md` ist committet. Die `*.example.*`-Dateien im Repo sind Platzhalter;
fehlt eine serverlokale Datei, zeigt die Seite den Platzhalter (`buero-desk-booking-landing_D03`).
Vor jedem Umstellen des Checkouts (Branch-Wechsel, Reset) prüfen, dass diese Dateien vorhanden sind.
