# SPJ Attendance — hosted web version with OneDrive sign-in

This version runs in any browser (including **iPhone Safari**) and connects to your
**personal OneDrive** with an in-browser Microsoft sign-in (MSAL.js). No app install, no admin.

Two steps: **(1)** host the file, **(2)** register a Microsoft app and paste the Client ID.

---

## 1) Host the file (pick one — all free, all HTTPS)

You only need to publish the single `index.html` from this folder.

### Cloudflare Pages (recommended, drag-and-drop)
1. Go to **https://pages.cloudflare.com** → sign up / log in → **Create a project** → **Direct Upload**.
2. Give it a name (e.g. `spj-attendance`) → drag this folder (with `index.html`) in → **Deploy**.
3. You get a URL like `https://spj-attendance.pages.dev`. That's your app.

### Netlify (also drag-and-drop)
- Go to **https://app.netlify.com/drop** → drag the folder in → you get `https://…netlify.app`.

### GitHub Pages
- New repo → upload `index.html` → **Settings → Pages** → Source = main / root → get `https://<you>.github.io/<repo>/`.

> Copy your final URL — you'll need it exactly in step 2. To update the app later, re-upload `index.html` to the same place.

---

## 2) Register the Microsoft app (personal account, no admin)

1. Go to **https://entra.microsoft.com** and sign in with your **personal** Microsoft account
   (outlook.com / hotmail / live). Open **App registrations → + New registration**.
2. **Name:** `SPJ Attendance Web`
   **Supported account types:** **Personal Microsoft accounts only**.
   **Redirect URI:** platform **"Single-page application (SPA)"**, and enter your hosted URL **exactly**, e.g.:
   ```
   https://spj-attendance.pages.dev/
   ```
   (Use the real page URL. If your file sits at `/index.html`, use the folder URL ending in `/`.)
   Click **Register**.
3. **Overview** → copy the **Application (client) ID**.
4. **API permissions → + Add a permission → Microsoft Graph → Delegated permissions** → add
   `Files.ReadWrite` and `User.Read` → **Add permissions**. (Personal account = you consent yourself at sign-in; no admin.)

> The **SPA** platform is important — it enables the browser sign-in (PKCE + CORS) so no server or secret is needed.

---

## 3) Use it

1. Open your hosted URL (on iPhone: open in Safari; you can **Share → Add to Home Screen** for an app-like icon).
2. Sign in to the app (Admin / admin@123, then change it).
3. **More → Settings → OneDrive (Microsoft 365)** → **OneDrive Account** → paste the **Client ID** → **Save** → **Sign in to OneDrive** (a Microsoft page opens; approve).
4. Choose your **Backup folder** and **Report folder**, then use **Restore from OneDrive** anytime.

Backups, reports and auto-backup now save straight into your OneDrive folder and can be read back on any device that opens the same URL and signs in.

---

## Notes
- **iPhone Safari:** the sign-in uses a full-page redirect (works within Safari's privacy rules). If Safari ever signs you out sooner than expected, just tap Sign in again.
- **Data** is still stored locally in each browser; OneDrive is the shared copy. Use **Restore from OneDrive** to load your data on a new device/browser.
- The app also keeps working offline for day-to-day marking; OneDrive actions need a connection.
- This is separate from the Android app — you can use either or both against the same OneDrive folder.
