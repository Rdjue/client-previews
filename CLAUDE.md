# Project Context: Client Previews

This repository hosts client website prototypes for **蓋婭科技 (Tellustek)**, served via GitHub Pages. Each subfolder is one client's standalone HTML prototype.

## Repository purpose

A centralized hub for sharing interactive HTML prototypes with clients during pre-proposal stages. Clients get a public URL to view and interact with the prototype on any device. Each project is self-contained (single `index.html` with inline CSS/JS, plus optional CDN assets).

## Structure

```
client-previews/
├── README.md              # Dashboard / project index (also user-facing)
├── CLAUDE.md              # This file
├── .gitignore
├── shenhe/                # Each client = one subfolder
│   ├── index.html         # The prototype (required filename)
│   └── notes.md           # Internal project notes (client info, version log)
└── _archive/              # (Optional) Finished/dormant projects moved here
    └── <code>/
```

## Conventions

- **Folder names** (案子代號): short, lowercase English, no spaces, no Chinese. e.g. `shenhe`, `acme`, `xinhua`.
- **Entry file**: must be exactly `index.html` (GitHub Pages serves this as the default route).
- **Self-contained HTML**: each `index.html` is one file with inline `<style>` and `<script>`. External resources allowed only from common CDNs (Google Fonts, jsDelivr, cdnjs).
- **Browser storage forbidden**: never use `localStorage` / `sessionStorage` inside prototypes — they may break across hosts.
- **Notes file**: each project folder has a `notes.md` with client info, version history, and todo. See `shenhe/notes.md` as the format reference.

## Hosting setup (GitHub Pages)

- **Repo**: this directory pushed to a public GitHub repo named `client-previews` under the user's personal account (not the `tellustek` organization).
- **Pages config**: Settings → Pages → Source: "Deploy from a branch" → Branch: `main` → Folder: `/ (root)` → Save.
- **URL pattern**: `https://<GITHUB-USERNAME>.github.io/client-previews/<案子代號>/`
- **Privacy**: public repo required for free Pages. URLs are not actively indexed but are not secret.

## Common tasks

### Add a new client project
1. Create folder `<code>/` (lowercase English code).
2. Add `<code>/index.html` (the prototype HTML).
3. Add `<code>/notes.md` (copy structure from `shenhe/notes.md`).
4. Update the project index table in `README.md`.
5. Commit & push.

### Update an existing prototype
1. Replace `<code>/index.html` with the new version.
2. Bump version log in `<code>/notes.md`.
3. (Optional) Keep older versions under `<code>/archive/v1-YYYYMMDD.html`.
4. Update version + date columns in `README.md`.
5. Commit & push. Live URL unchanged.

### Archive a finished project
1. Move folder to `_archive/<code>/`.
2. Update status in `README.md` (or remove the row, document in commit message).
3. Commit & push.

### Verify a deployment after push
- Wait 30–90 seconds after push.
- Visit the URL. If 404, check Settings → Pages for build status / errors.

## Initial setup (one-time, if not yet done)

```bash
# In the repo folder
git init
git branch -M main
git add .
git commit -m "Initial commit: client-previews scaffold + shenhe v2"

# Create GitHub repo and push (using GitHub CLI)
gh repo create client-previews --public --source=. --remote=origin --push

# Enable Pages (cannot be done via gh; use the web UI)
# Settings → Pages → Deploy from a branch → main / (root) → Save
```

If `gh` CLI is not installed, create the repo manually on github.com first, then:

```bash
git remote add origin git@github.com:<USERNAME>/client-previews.git
git push -u origin main
```

## Placeholders to fill in

- `<GITHUB-USERNAME>` in `README.md`: replace with the user's actual GitHub username before pushing (used in the URL column of the index table).

## Current projects

See `README.md` for the up-to-date project list. As of scaffold creation: only `shenhe` (深河出版).
