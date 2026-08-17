# Painting Check-In

A single-file check-in / check-out kiosk for an iPad at the painting studio door. Tap your paddle
to check in, tap it again to check out. An admin console behind a passcode holds the records.

Colour, type and styling follow [edmondfinearts.com](https://www.edmondfinearts.com/). This is the
painting-studio companion to `studio-checkin`; the two keep entirely separate databases even when
hosted on the same GitHub Pages domain (distinct storage keys, IndexedDB name and cache name).

## Running it

**Hosted (GitHub Pages)** — open the site on the iPad in Safari, then Share → **Add to Home
Screen**. It installs as a standalone app, and a service worker keeps it running when the wifi
drops. No sign-in.

**Offline / no network at all** — `index.html` is fully self-contained. Copy it to the iPad and
open it in a kiosk browser app. See [SETUP.md](SETUP.md).

## Admin

Gear icon, bottom right. Default passcode `1986`, changeable in Database → Security.

| Tab | What's there |
|---|---|
| Records | Search by user, direction, date range or free text; session lengths; delete rows; CSV + JSON export |
| Users | Add and remove people; removals move that history to the archive |
| Database | Storage health, archive controls, full export / import, passcode, danger zone |

## How records are stored

Everything lives in the browser on the device running the kiosk — there is no server and no
account. Each change is written to **localStorage and IndexedDB both**; on launch the app loads
whichever copy is newer and repairs the other, so one store being cleared doesn't lose the day's
records. Database → **Storage health** reports which backends are live and what the last launch
restored from.

Because the data is per-device, opening this site somewhere else gives you an empty kiosk, not
this studio's records.

**Back it up.** Database → Export full DB (JSON), monthly. The panel warns once a backup is more
than 14 days old. Import DB restores onto a replacement iPad.

## Retention

A record is archived one year after last access: entries more than 12 months older than that
person's most recent activity move to the archive, and anyone dormant over a year has their whole
history moved. Archived records stay searchable and exportable until purged by hand.

## Files

| | |
|---|---|
| `index.html` | The entire app — markup, styles, logic, seed roster |
| `sw.js` | Service worker; caches the shell for offline use |
| `manifest.webmanifest` | Makes Add to Home Screen install it standalone |
| `SETUP.md` | iPad deployment, kiosk browsers, Guided Access lockdown |
