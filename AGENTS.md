# Base44 Dev Environment

## Project Overview
"Lords of Castles" — a static HTML/CSS/JS medieval settlement game prototype. No build system, no backend, no package manager, no external dependencies. Each file is a standalone HTML page (popups and transitions are handled with inline JS); pages do not link to one another.

## File Layout Quirks
- Content files have **spaces in their names and no `.html` extension** (e.g. `Main menu`, `Building menu`).
- `Main menu` is the entry point (title "Lords of Castles").
- Pages reference PNG image assets (e.g. `wide_cinematic_video_game_main_menu_scene_dim_med.png`, `map.png`) that are **not committed** — backgrounds will appear broken until those images are added to the repo root.

## Running
```
docker compose -f docker-compose.base44.yml up -d
```
Serves the repo root via `nginx:alpine` on host port 3000. `nginx.base44.conf` sets `index "Main menu"` and `default_type text/html` so the extensionless files render as HTML.

## Gotchas
- The repo root directory must be world-traversable (mode 755) because the nginx worker runs as a non-root user. If you see `403 Forbidden`, run `chmod 755 .` on the host.
- There is no live-reload dev server (plain static files). Edits appear on browser refresh; call `reload_preview` after changes that should show in the preview without a manual refresh.

## Verification
- `curl -s -o /dev/null -w "%{http_code}" http://localhost:3000/` → `200`
- All pages reachable: `http://localhost:3000/Banner`, `http://localhost:3000/Building%20menu`, etc.
