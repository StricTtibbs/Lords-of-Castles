# AGENTS.md — Lords of Castles

## Project Overview
This is a collection of prototype files for a medieval settlement game ("Lords of Castles" / "Kingdoms of the Medieval Age"). There is no framework, build system, or package.json dependencies. The repo contains:
- **Standalone HTML files** (no extensions in filenames) — each is a self-contained UI prototype with inline CSS/JS
- **C++ snippets** — Unreal Engine actor classes and game logic structs
- **Python files** — pygame main menu prototype

## Running the Project
- Served as static files via `python -m http.server` in Docker (see `docker-compose.base44.yml`)
- `index.html` is the landing page linking to all HTML prototypes
- No build step, no dependencies to install, no external credentials needed
- Preview is on port 3000

## Quirks
- Filenames contain spaces and no extensions — URL-encode spaces (`%20`) when linking
- Several HTML files reference `start-game.png` and `map.png` which don't exist in the repo; backgrounds fall back to CSS gradients
- `package-lock.json` exists but has no dependencies — it's a stub
