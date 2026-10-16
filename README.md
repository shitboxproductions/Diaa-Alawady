# لعبة تلبيس ضياء العوضي — Diaa El Awady Dress-Up Game

A single-file browser game (dress-up + chicken-shooting reward minigame). No build step, no dependencies — just HTML/CSS/JS in one file.

## Files

| File | Required? | Notes |
|------|-----------|-------|
| `index.html` | ✅ Yes | The entire game (~160 KB). Renamed from `لعبة-ضياء.html` for a clean URL. |
| `.nojekyll` | Recommended | Tells GitHub Pages to serve files as-is (skips Jekyll processing). |
| `song.mp3` | Optional | Victory song placed next to the game. If missing, a built-in synth tune plays. Users can also drag & drop any mp3 onto the page. |
| `face.png` / `face.jpg` | Optional | Custom face photo for the character. If missing, a drawn placeholder face is used. |

## Deploy on GitHub Pages (free, HTTPS included)

1. Create a **public** repository, e.g. `diaa-game`.
2. Upload **all the files in this folder** to the repo root (GitHub web UI → *Add file → Upload files* — note: hidden `.nojekyll` must be added via *Create new file* and typing the name `.nojekyll`, since the uploader skips dotfiles).
   - Or via git:
     ```bash
     git init && git add -A && git commit -m "diaa game"
     git branch -M main
     git remote add origin https://github.com/<YOUR-USERNAME>/diaa-game.git
     git push -u origin main
     ```
3. Repo → **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main` / `/ (root)` → Save.
4. Wait ~1 minute. The game goes live at:
   ```
   https://<YOUR-USERNAME>.github.io/diaa-game/
   ```

## Storage / progress saves

- The game saves progress (coins, unlocked outfits, stages, guns) to **both** `localStorage` (key `diya-dressup-save`) and a **1-year cookie** (`diyaDressSave`). Both work on GitHub Pages because it serves over **HTTPS** on the `github.io` origin.
- Saves are bound to the **origin** (protocol + domain). Decide your final URL *before* sharing the link: renaming the repo later or moving to a custom domain resets players' progress (the old storage isn't readable from the new URL).
- Incognito / private-browsing windows may not keep progress.
- Optional cached song (~up to 3.8 MB base64) is stored in `localStorage` only; the 5 MB per-origin browser quota applies. If it doesn't fit, the game keeps working — it just re-reads `song.mp3` each time. Progress itself is tiny (< 2 KB) and always saves.

## Alternative hosts

Works anywhere that serves over HTTPS with no server-side logic needed:

- **Netlify Drop** (fastest, no git): drag this folder onto https://app.netlify.com/drop → instant `*.netlify.app` URL.
- **Cloudflare Pages** / **Vercel**: connect the repo or upload directly.

## Cheat sheet

Progress is data, not code — to reset a player's save, run this in the browser console on the game page:

```js
localStorage.removeItem('diya-dressup-save'); document.cookie='diyaDressSave=; max-age=0; path=/'; location.reload();
```
