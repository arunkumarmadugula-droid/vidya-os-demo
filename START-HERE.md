# Vidya OS — final tested mobile PWA package

This package contains the latest tested Vidya build from
`outputs/vidhya-os-demo`, repackaged on August 10, 2026.

## Open it locally

From PowerShell, run:

```powershell
cd "C:\Users\arunk\Documents\Codex\2026-08-06\as\outputs\Vidya-OS-FINAL"
py -m http.server 4181 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:4181/index.html
```

## Publish it on GitHub Pages

Upload these files at the root of a clean GitHub repository:

- `.nojekyll`
- `index.html`
- `styles.css`
- `app.js`
- `config.js`
- `manifest.json`
- `sw.js`
- `icon-180.png`
- `icon-192.png`
- `icon-512.png`

Do not upload API secrets or private work documents. The `Documentation`
folder is for your reference and is not required by the running app.

## Current capability boundary

The app works without an API key for its local Brief, Today, Coach, Library,
Search, Subjects, tags, memories, themes and offline shell. Optional Gemini
testing is available for non-sensitive personal experimentation. Secure user
accounts, cross-device synchronization, production AI, confidential document
handling and reliable closed-app reminders still require the Supabase/Gemini
production implementation described in `Documentation`.

