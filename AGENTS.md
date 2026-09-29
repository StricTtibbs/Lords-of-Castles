# AGENTS.md — Lords of Castles

## What this project is
A medieval settlement/kingdom builder ("Lords of Castles"). The repo is a **flat collection of standalone source files** with spaces in their names and **no file extensions**. There is no build system, no framework, no package manager deps (`package-lock.json` is an empty stub), and no backend.

File kinds (identified by content, not extension):
- **Self-contained HTML pages** (HTML+CSS+JS in one file) — the playable prototypes: `Terrain generation HTML`, `Backyard Extensions HTML`, `Building menu`, `Placement`, `Structure Rotation`, `Calendar and Seasons`, `Militia Requirements`, `AI Adverseries`, `Construction logic C++ and HTML`, `visable` (settlement HUD).
- **Python** — `Main menu python` (pygame).
- **C++ headers/snippets** — `3D`, `People detail`, `Starting food`, `Starting game`, `Terrain Generation C++`, `backyard extension C++`, `calendar and Season C++`, `main menu C++`.
- **JS snippets** — `Game logic`, `Consume food and food storage`, `Food itself`, `Realism Terrain`, `Trees Detail`, `New Families`.

## How it runs here
Served as static files by `nginx:alpine` on host port 3000 (`docker-compose.base44.yml`). A custom `nginx.base44.conf` runs nginx as **root** so it can read the bind-mounted source regardless of directory permissions (the repo dir clones as mode 700). `index.html` (added by Base44) links to every playable HTML page.

There is no live-reload dev server (static HTML); edits appear on browser refresh. Call `reload_preview` after changes so the user sees them.

## Verifying it works
```
docker compose -f docker-compose.base44.yml up -d
curl -s -o /dev/null -w "%{http_code}\n" http://localhost:3000/          # 200
curl -s -o /dev/null -w "%{http_code}\n" "http://localhost:3000/visable" # 200
```

## Secrets
None required. No external services.
