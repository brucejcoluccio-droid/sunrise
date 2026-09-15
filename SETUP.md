# Setup — GitHub Pages

Hosting matters for one reason: HTTPS counts as a **secure context**. That's
what makes Chrome honor the manifest (so it installs standalone, with no
address bar) and enables the real Wake Lock API. A `file://` page gets neither.

Once installed, the service worker caches everything. You can be in a hotel
with no wifi and it still works. Nothing runs in the background.

You can do all of this from the phone — no laptop needed.

---

## 1. Create the repository

1. Sign in at **github.com** (free account is fine).
2. Tap **+** → **New repository**.
3. Name it `sunrise`. Set it **Public** — Pages requires public on free accounts.
4. **Create repository**.

## 2. Upload the files

1. On the new repo page, tap **uploading an existing file**.
2. Unzip the bundle on your phone first, then select **all** of these:
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `.nojekyll`
   - the `icons` folder (all three PNGs)
3. Tap **Commit changes**.

Everything must sit at the **root** of the repo, not inside a `sunrise-pages/`
subfolder. If your file manager unzipped it into a folder, upload the folder's
*contents*, not the folder. Getting this wrong is the most common failure —
the page loads but the icons and service worker 404.

## 3. Turn on Pages

1. Repo → **Settings** → **Pages** (left sidebar; on mobile it's under the
   hamburger menu inside Settings).
2. Under **Source**, choose **Deploy from a branch**.
3. Branch: **main**, folder: **/ (root)**. **Save**.
4. Wait about a minute, then refresh. It will show your URL:

```
https://YOUR-USERNAME.github.io/sunrise/
```

## 4. Install it

1. Open that URL in **Chrome**.
2. The setup screen should look normal. If you see an amber notice saying it's
   running in a browser tab, that's expected at this point.
3. Chrome menu (⋮) → **Install app** (it may say *Add to Home screen*).
4. Launch it from the **new home screen icon**, not from Chrome.
5. The amber notice should now be gone, and there should be no address bar.

## 5. Make it survive the night

- Settings → Apps → **Sunrise** → Battery → **Unrestricted**
- Settings → Display → **Screen timeout** → 10 minutes
- Keep the phone on the charger, face up

## 6. Verify before you trust it

Run the built-in test with a **2-minute** duration and check all four:

| Check | Expected |
|---|---|
| Light | ramps dark red → orange → bright, brightest at the very end |
| Sound | chimes from the first pulse, gets louder |
| Vibration | repeating buzz |
| Stop | requires an 800 ms hold; the fill bar shows progress |

Then tap the screen mid-run. The readout should say **`screen lock held`**.

- `screen held by video fallback` → you're not on HTTPS. Check the URL.
- `NOT fullscreen` → tap the screen again; it retries on every tap.

Keep a normal Clock alarm set for the first few nights regardless.

---

## Updating it later

Edit `index.html` directly on github.com (pencil icon) and commit. Then bump
the cache name in `sw.js` — change `sunrise-v1` to `sunrise-v2` — or the
service worker will keep serving the old cached copy and your change will
appear to do nothing. This trips up almost everyone once.

## If something breaks

| Symptom | Cause |
|---|---|
| 404 at the Pages URL | files are in a subfolder, or Pages not enabled yet |
| No **Install app** in the menu | manifest didn't load — check `manifest.webmanifest` is at the root |
| Generic icon on home screen | `icons/` folder didn't upload |
| Changes don't appear | service worker cache — bump the version in `sw.js` |
| Screen still sleeps | battery optimization, or not launched from the home screen icon |
