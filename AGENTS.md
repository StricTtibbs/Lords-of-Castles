# AGENTS.md — Lords of Castles

## Project Overview
"Lord of Castles / Kingdoms of the Medieval Age" — a medieval settlement builder game.
The repo is a collection of standalone source files **without file extensions**:

- **Self-contained HTML pages** (inline CSS + JS, runnable in a browser):
  `visable`, `Placement`, `Structure Rotation`, `Building menu`,
  `Construction logic C++ and HTML`, `Calendar and Seasons`, `AI Adverseries`,
  `Backyard Extensions HTML`, `Militia Requirements`, `3D creation`, `Menu display Html`
- **Standalone JS** (companion scripts, not linked into any page yet):
  `Game logic`, `Medieval people logic and 3D animation`
- **Unreal Engine C++** (not runnable in browser): `3D`, `Menu Display C++`,
  `main menu C++`, `Bushes and Shrubs C++`, `backyard extension C++`,
  `Building panel`, `Realism Terrain`, `Trees Detail`
- **Python pygame** (not runnable in browser): `Main menu python`
- **Data/config snippets**: `Starting game`, `Starting food`, `Food itself`,
  `Consume food and food storage`, `New Families`, `People detail`
- **Audio snippet**: `Medieval soundtrack 1` (references a missing `medieval-soundtrack.mp3`)

## How It Runs
Static files served by **nginx** (nginx:alpine) via `docker-compose.base44.yml`.
- `index.html` is a landing page linking to all HTML game modules.
- `nginx.conf` sets `default_type text/html` so extensionless files render as HTML.
- nginx runs as `user root` because the repo directory has 700 permissions.
- Port 3000 is mapped to the preview.

## Running
```sh
docker compose -f docker-compose.base44.yml up -d
```
Verify: `curl -s -o /dev/null -w '%{http_code}' http://localhost:3000/` → 200

## Editing
These are static files — edits appear on browser refresh (call `reload_preview`
after changes). No build step, no live-reload server needed.
