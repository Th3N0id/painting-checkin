# Painting Check-In — iPad kiosk setup

Everything runs from one file. No server, no internet, no sign-in.

## 1. Get the file onto the iPad

`index.html` is the whole app. Move it across by whichever is easiest:

- AirDrop it to the iPad, choose **Save to Files**
- or drop it in iCloud Drive / Google Drive and download it on the iPad
- or connect the iPad by cable and copy it into the kiosk app's folder in Finder / iTunes File Sharing

Save it somewhere you can find again — **On My iPad → (kiosk app folder)** is ideal.

## 2. Install a kiosk browser

Safari cannot open a local `.html` file, which is why a kiosk browser is needed. Any of these
load local files and run offline:

| App | Notes |
|---|---|
| [Kiosk Pro Basic](https://apps.apple.com/us/app/kiosk-pro-basic/id409918026) | Free. Point it at a local file in its Documents folder. |
| [Flow Kiosk](https://apps.apple.com/us/app/flow-kiosk-offline-ipad-kiosk/id1410522304) | Stores content locally, built-in Guided Access check. |
| [Offline Kiosk](https://apps.apple.com/pt/app/offline-kiosk/id1085540867?l=en) | Caches everything to local storage. |

In the app's settings, set the home page / start file to `index.html`.

**Turn OFF any "clear cache on exit" or "reset on idle" option.** Those wipe the database.

## 3. Verify it actually keeps records — do this before going live

1. Open the app, tap a paddle or two.
2. Gear (bottom right) → passcode `1986` → **Database** tab → read **Storage health**.
   Both backends should say *working*.
3. Fully quit the kiosk app from the app switcher, reopen it, return to that panel.
4. It should report a restore and the same record count.

If it says *nothing found — started from a fresh roster*, that app is discarding web data.
Change its cache settings, or try one of the other apps above.

## 4. Lock the iPad down

**Settings → Accessibility → Guided Access → On**, set a passcode.
Open the kiosk app, then triple-click the side/home button to start Guided Access.
The iPad is now pinned to that one app until someone enters the Guided Access passcode.

Also worth setting: **Settings → Display & Brightness → Auto-Lock → Never**, and leave it on power.

## Admin

Gear icon, bottom right. Passcode **1986** — change it in Database → Security.

- **Records** — search by user, direction, date range, or free text; delete rows; export CSV/JSON
- **Users** — add and remove people; removing someone moves their history to the archive
- **Database** — storage health, archive controls, full export/import, passcode, danger zone

## Backups

Records live only on this iPad. Once a month, open **Database → Export full DB (JSON)** and
keep the file somewhere else. The panel nags in gold once a backup is more than 14 days old.
**Import DB** restores from one of those files onto a replacement iPad.

## Retention

A record is archived one year after last access: entries more than 12 months older than that
person's most recent activity move to the archive, and anyone dormant for over a year has their
whole history moved. Archived records stay searchable and exportable until purged by hand.
