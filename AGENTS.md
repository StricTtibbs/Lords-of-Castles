# Lords of Castles — Base44 Dev Environment

## What this project is
A static HTML/CSS/JS medieval settlement game. No build system, no backend, no package manager. The entire game lives in a single self-contained HTML file: **`Terrain generation HTML`** (note: filename has spaces and no extension).

## How it runs
- Served by **nginx** (`nginx:alpine`) via `docker-compose.base44.yml`.
- The repo root is bind-mounted read-only into the container at `/usr/share/nginx/html`.
- `index.html` is a redirect stub that sends `/` to `Terrain%20generation%20HTML`.
- `nginx.base44.conf` sets `default_type text/html` so the extensionless game file renders in the browser instead of downloading.
- Web entry point is host port **3000**.

## No secrets required
This is a pure static site — no external services, databases, or API keys.

## Verifying it works
```bash
docker compose -f docker-compose.base44.yml up -d --build
curl -s http://localhost:3000/ | head -5   # should show the redirect HTML
curl -s "http://localhost:3000/Terrain%20generation%20HTML" | head -5  # should show the game
```

## Editing
Any edit to the HTML files is immediately live — nginx serves files directly from the mount. Just refresh the preview (no rebuild needed). Call `reload_preview` after changes if the iframe doesn't refresh on its own.

## File notes
- Filenames contain spaces (e.g. `Terrain generation HTML`, `Main menu`). URL-encode spaces as `%20` when curling.
- Some files are C++ headers/snippets (`Starting game`, `People detail`, `Terrain Generation C++`, `backyard extension C++`, `Realism Terrain`) — design notes, not part of the running app.
- The game references `start-game.png` for background images, but no image files exist in the repo. The game works without them (just no background art).
