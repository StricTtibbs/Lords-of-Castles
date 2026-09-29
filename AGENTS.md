# AGENTS.md — Lords of Castles

## Project Overview
A static HTML/CSS/JS medieval game prototype ("Lords of Castles"). No build system, no backend, no package manager. Files have spaces in their names and no extensions. Some files are C++/Unreal Engine design specs (not web-served).

## Running the App
```
docker compose -f docker-compose.base44.yml up -d
```
Serves on port 3000 via nginx. The entry point is the "Main menu" file.

## Architecture
- **nginx:alpine** serves files from the repo root (bind-mounted at `/app`).
- `nginx.base44.conf` sets `default_type text/html` so extensionless files render as HTML.
- nginx runs as `root` to avoid permission issues with the sandbox's restrictive directory permissions.
- Healthcheck uses `127.0.0.1` (not `localhost`, which resolves to IPv6 in the container).

## Key Files
- `Main menu` — entry point, the game's main menu (standalone HTML)
- `Banner`, `Building menu`, `Militia Requirements`, `Placement`, `Structure Rotation`, `visable` — standalone HTML game screens
- `Game logic` — JavaScript (terrain generation, game state)
- `People detail`, `Realism Terrain`, `Starting game` — C++/Unreal design specs (not web pages)

## Editing
Changes to HTML/JS files are immediately visible on page refresh (static serving, no build step). Use `reload_preview` after edits to force the preview iframe to refresh.

## No Secrets Required
This is a fully static site with no external dependencies or credentials.
