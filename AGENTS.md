# AGENTS.md — Lords of Castles (Base44)

## What this project is
A static, front-end-only browser game prototype ("Lords of Castles"). Every
screen is a standalone HTML/CSS/JS file with **no build step, no package.json,
no backend, and no external dependencies**. File names contain spaces and have
no extensions (e.g. `Main menu`, `visable`, `Building menu`).

## Entry point
`Main menu` is the game's main menu. The repo root `index.html` is a Base44 setup
artifact: a **symlink** to `Main menu`, so nginx serves the menu directly at `/`
(no client-side redirect). Edits to `Main menu` are reflected immediately.

## How it runs here
Served by `nginx:alpine` via `docker-compose.base44.yml`, bind-mounting the repo
read-only at `/usr/share/nginx/html` on host port 3000. No image rebuild is
needed for edits — changes to any HTML/CSS/JS file appear on browser refresh.
There is no live-reload/HMR; call `reload_preview` after edits if needed.

## Verification
- `docker compose -f docker-compose.base44.yml up -d --build`
- `curl -sI http://localhost:3000/` → 200, then follow the redirect to `Main menu`.
- The preview should show the Lords of Castles main menu.

## Secrets
None required. The app is fully static with no external services.
