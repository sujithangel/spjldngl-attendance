# Live multi-device sync with Firebase Firestore (free, no card)

This makes every device share the **same live data** — a mark on one phone appears on all others
within ~1 second. Access is protected by **one shared workspace password**. Firestore's free
(Spark) plan needs **no credit card**.

You'll (A) create a free Firebase project, (B) paste its details into the app on each device.

---

## A) Create the Firebase project — one time

1. Go to **https://console.firebase.google.com** → **Add project**.
   - Name it `SPJ Attendance` → Continue.
   - Google Analytics: you can **turn it off** (not needed) → **Create project**.

2. **Build → Firestore Database → Create database**:
   - **Start in production mode** → Next.
   - **Location:** pick one near you — for SPJ London choose a **Europe** region (e.g. `europe-west2`). *(This can't be changed later.)* → Enable.

3. **Firestore → Rules** tab → replace everything with this, then **Publish**:
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if request.auth != null;
       }
     }
   }
   ```
   *(This means only someone signed in with your shared workspace account can read/write — not the public.)*

4. **Build → Authentication → Get started → Sign-in method** → enable **Email/Password** → Save.

5. **Authentication → Users → Add user**: create your **shared workspace account**:
   - Email: anything you'll remember, e.g. `workspace@spjldngl.com` (it does **not** need to be a real inbox).
   - Password: a **strong** shared password — this is the "workspace password" everyone will type.
   - Add user.

6. **Project settings** (gear icon) **→ General → Your apps →** click the **Web** icon `</>`:
   - Nickname `SPJ Web` → Register app.
   - It shows a `firebaseConfig` block. Copy these three values:
     - **apiKey** (`AIza…`)
     - **projectId**
     - **appId** (`1:…:web:…`)

---

## B) Connect the app (on each device)

1. Open your app URL: `https://sujithangel.github.io/spjldngl-attendance/`
2. Sign in to the app → **More → Settings → Live Sync (Firestore)**.
3. Fill in:
   - **API key** = apiKey
   - **Project ID** = projectId
   - **App ID** = appId
   - **Workspace email** = the shared email from step A5
   - **Workspace password** = the shared password from step A5
4. **Save & connect** → you should see **"Live sync connected."**
5. Do the same on every other phone/laptop (same values + password). They all now share live data.

Tip: after the first device connects, its data uploads automatically; the next device you connect will pull that same data.

---

## Backups / restore points
Under the same **Live Sync** section:
- **Save Restore Point** → stores a timestamped snapshot in Firestore.
- **Restore Points** → roll the whole workspace back to any snapshot (applies to all devices).

Google Drive still works separately for saving report **files** (PDF/Excel).

---

## Security notes
- Data is encrypted in transit and at rest by Google; the rules above keep it private to holders of the workspace password.
- The apiKey/projectId in the page are **public by design** — they only name the project; the password + rules are what protect the data.
- Treat the **workspace password** like a key. If it leaks, change it in **Authentication → Users** (reset password) and re-enter the new one on each device.
- Choosing a **Europe** region keeps data in the EU/UK for GDPR comfort.

## Limits (free tier)
50,000 reads + 20,000 writes per day, 1 GiB storage — far more than a school's attendance needs.
