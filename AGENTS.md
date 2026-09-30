# Base44 Setup Notes

## Project Overview
This is **Lords of Castles / Kingdoms of the Medieval Age** — a medieval strategy game prototype. It is NOT a standard web application. It is a collection of source files in multiple languages:
- **HTML files** (browser-playable game screens with embedded CSS/JS): `Terrain generation HTML` (main game), `Menu display Html`, `Backyard Extensions HTML`, `visable`
- **Python** (pygame desktop game): `Main menu python`
- **C++** (Unreal Engine widgets/logic): `main menu C++`, `3D`, `Bushes and Shrubs C++`, etc.
- **JavaScript snippets**: `Game logic`, `Medieval soundtrack 1`

## What Runs in the Preview
Only the **HTML game** runs in the browser preview. The main entry point is `Terrain generation HTML` — a self-contained game with a main menu, 5 map selections (canvas-generated terrain), and a gameplay screen with camera controls (WASD/QE/M).

`index.html` at the repo root redirects to `Terrain generation HTML`.

## How It's Served
A `python:3.12-slim` container runs `python -m http.server 3000 --bind 0.0.0.0` with the repo bind-mounted read-only at `/app`. No build step, no backend, no database. Python's http.server serves `index.html` for `/`.

## No External Credentials
This project requires no external secrets or credentials.

## File Naming Quirk
All source files have **spaces in their names** and no file extensions. URLs must encode spaces as `%20` (e.g. `Terrain%20generation%20HTML`).

## Missing Assets
`start-game.png` and `medieval-soundtrack.mp3` are referenced in HTML but not present in the repo. The game works without them (background gradients show instead).

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` → 200
- `curl -s -o /dev/null -w "%{http_code}" "http://localhost:3000/Terrain%20generation%20HTML"` → 200

## Live Reload
Python's http.server has no live reload. After editing HTML files, call `reload_preview` to refresh the preview.
