# Deploying RouteLog to GitHub Pages

This gets RouteLog live at `https://obscode96.github.io/flex-tracker` (or whatever repo name you use).

## One-time setup

### 1. Create the repo (if you haven't already)
- Go to github.com → New repository
- Name it `flex-tracker` (or whatever you want in the URL)
- Set it to **Public**
- Don't initialize with a README

### 2. Upload the file
- Open your new repo on GitHub
- Click **Add file → Upload files**
- Drag in `routelog.html`
- **Important:** rename it to `index.html` before uploading, or rename it in the repo after — GitHub Pages serves `index.html` as the default page
- Commit the file

### 3. Enable GitHub Pages
- Go to your repo → **Settings → Pages**
- Under "Source", select **Deploy from a branch**
- Branch: `main`, folder: `/ (root)`
- Click **Save**

GitHub will give you a URL — usually takes 1–2 minutes to go live.

---

## Sharing with coworkers

Just send them the URL. They open it in their phone browser, then:

**iPhone:** Tap the Share icon → "Add to Home Screen" → Add  
**Android:** Tap the browser menu (⋮) → "Add to Home Screen" → Install

The app installs like a native app with its own icon. Their data stays on their own device — nothing is shared between users.

---

## Updating the app

When you have a new version:
1. Open your repo on GitHub
2. Click on `index.html`
3. Click the pencil (Edit) icon
4. Paste in the new file contents
5. Commit changes

GitHub Pages redeploys automatically in about 60 seconds.

---

## Notes

- The service worker caches the app for offline use after the first load
- Each person's data is stored only on their own device — completely private
- No backend, no database, no cost — GitHub Pages is free for public repos
