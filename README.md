# DM Mind Bending — Self-hosted Vercel Deployment

A self-contained deployment of the Fancade game "DM Mind Bending" extracted from a HAR capture.

## Structure

```
public/
  index.html              — Main game page (rewritten for local assets)
  favicon-32x32.png
  touch-icon.png
  images/
    68FADFA66D195DFE.jpg  — Game cover image
    appstore.png
    playstore.png
  webapp/
    fancade_stripped.css  — Game styles
    favicon.ico
    source_min_stripped.js — Patched: fetches game binary locally
    index_stripped.js      — Emscripten loader
    index_stripped.data    — Game data bundle
    index_stripped.wasm    — WebAssembly binary
    games/
      68FADFA66D195DFE    — Game level binary
vercel.json               — WASM MIME types + COOP/COEP headers
```

## Deploy to Vercel

### Option 1: Vercel CLI
```bash
npm i -g vercel
vercel
```

### Option 2: GitHub + Vercel Dashboard
1. Push this repo to GitHub
2. Go to [vercel.com](https://vercel.com) → New Project
3. Import your GitHub repo
4. **Set the Root Directory to `public`** in the Vercel project settings
5. Deploy — no build step needed (static site)

## Notes
- Firebase SDKs are still loaded from Google's CDN (free, no config needed)
- The game binary is served locally from `/webapp/games/68FADFA66D195DFE`
- COOP/COEP headers are required for WebAssembly shared memory to work
