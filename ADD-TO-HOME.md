# Install SPJ Attendance as a full-screen app (Add to Home Screen)

The hosted app is now an installable PWA — it launches full-screen (no browser bars) with the
SPJ icon. Make sure these files are all in the same folder on GitHub Pages:
`index.html`, `manifest.webmanifest`, `service-worker.js`, `icon-192.png`, `icon-512.png`, `icon-512-maskable.png`.

Open the site once over https first: `https://sujithangel.github.io/spjldngl-attendance/`

## Android (Chrome)
1. Open the URL in **Chrome**.
2. Tap the **⋮ menu → Install app** (or **Add to Home screen**).
3. Confirm. It appears on your home screen with the SPJ icon and opens **full-screen, like a native app**.

## iPhone / iPad (Safari)
1. Open the URL in **Safari**.
2. Tap **Share → Add to Home Screen → Add**.
3. It appears with the SPJ icon and opens full-screen.

## Notes
- Do the first Google/Firebase **sign-in in a normal browser tab** if any provider blocks the embedded view; after that the installed app works normally.
- Updating the app: re-upload `index.html`. The app fetches the latest each time it's online (the service worker uses network-first), so installed copies update automatically.
- If the icon doesn't update after a change, remove the home-screen icon and add it again.
