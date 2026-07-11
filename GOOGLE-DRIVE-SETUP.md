# SPJ Attendance — hosted web version with Google Drive

Runs in any browser (incl. iPhone Safari) and saves backups + reports to your **Google Drive**,
in an auto-created **"SPJ Attendance"** folder, with in-browser Google sign-in.
**No card, no admin, no Google verification** (it uses the minimal `drive.file` scope).

Two steps: **(1)** host the file on GitHub Pages, **(2)** create a free Google OAuth Client ID.

---

## 1) Host on GitHub Pages

1. Sign in at github.com → **New repository** → name `spj-attendance`, **Public** → Create.
2. **Add file → Upload files** → drag in `index.html` → **Commit changes**.
3. **Settings → Pages** → Source = **Deploy from a branch**, branch **main**, folder **/ (root)** → Save.
4. After ~1 min you get your permanent URL:
   ```
   https://YOUR-USERNAME.github.io/spj-attendance/
   ```
   Use it **with the trailing slash**. Copy it — you need it in step 2.

---

## 2) Create a Google OAuth Client ID (free, no card)

1. Go to **https://console.cloud.google.com** and sign in with your Google account.
2. Top bar → **Select a project → New Project** → name it `SPJ Attendance` → Create → select it.
3. Left menu → **APIs & Services → Library** → search **Google Drive API** → **Enable**.
4. **APIs & Services → OAuth consent screen**:
   - User type: **External** → Create.
   - App name `SPJ Attendance`, your email in the required fields → Save and continue.
   - **Scopes:** you don't need to add any here (the app requests `drive.file` at sign-in) → Save and continue.
   - **Test users:** click **+ Add users** and add **your own Google email** → Save. (Keep the app in "Testing" — that's fine for personal use and needs no verification.)
5. **APIs & Services → Credentials → + Create credentials → OAuth client ID**:
   - Application type: **Web application**.
   - Name: `SPJ Attendance Web`.
   - **Authorised JavaScript origins → + Add URI:** your site **origin only** (no path):
     ```
     https://YOUR-USERNAME.github.io
     ```
   - (No redirect URI needed for this sign-in type.)
   - **Create** → copy the **Client ID** (ends in `.apps.googleusercontent.com`).

---

## 3) Connect in the app

1. Open your Pages URL (on iPhone: Safari → optionally **Share → Add to Home Screen**).
2. Sign in to the app (Admin / admin@123, then change it).
3. **More → Settings → Google Drive → Google Account** → paste the **Client ID** → **Save** → **Connect Google Drive** → choose your Google account and Allow.
   - You may see an **"unverified app"** notice because it's in Testing mode — since you're the test user, click **Continue**. (No verification needed for personal use.)
4. Now backups, reports and **Auto-backup** save into your Drive's **"SPJ Attendance"** folder.
5. **Restore from Google Drive** lists your backups; tap one to restore on any device that opens the same URL and connects.

---

## Notes
- **`drive.file` scope** means the app can only see the files it created (the SPJ Attendance folder) — it can't read the rest of your Drive. That's why no Google review is required.
- **Sign-in lasts ~1 hour** per session; the app quietly re-authorises when needed. On iPhone Safari you may occasionally get a quick Google prompt — that's normal.
- **Origin must match:** the "Authorised JavaScript origins" value must be your exact site origin (e.g. `https://YOUR-USERNAME.github.io`, no trailing path). If sign-in errors with "origin mismatch", fix that value.
- Data is stored locally in each browser; Drive is the shared/permanent copy. Use **Restore from Google Drive** to load it on a new device.
