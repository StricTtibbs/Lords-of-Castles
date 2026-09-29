# Lords of Castles — Base44 Dev Environment

## Project Overview
Vanilla HTML/CSS/JS medieval settlement game. No build step, no backend, no dependencies.
Files have spaces in their names and no file extensions (e.g. "Main menu", "Building menu").
Some files are C++ reference snippets ("People detail", "Realism Terrain", "Starting game") — not part of the web app.

## Entry Point
`index.html` (created by Base44) redirects to `Main menu` via JavaScript.
The main menu page is the game's starting screen.

## Running the App
```
docker compose -f docker-compose.base44.yml up -d
```
Served by nginx:alpine on port 3000. Source is bind-mounted read-only.

## Key Notes
- File names contain spaces; URLs must use `%20` encoding (e.g. `/Main%20menu`).
- The repo root directory needed `chmod 755` so nginx's worker user can traverse it.
- Referenced image assets (e.g. `wide_cinematic_video_game_main_menu_scene_dim_med.png`, `map.png`, `banner1.png`) do not exist in the repo — pages render with broken images.
- No live-reload dev server; nginx serves static files directly. Call `reload_preview` after edits.
- Healthcheck uses `127.0.0.1:3000` (not `localhost`) due to IPv6 resolution in the container.

## Pages
- `Main menu` — main menu (entry point)
- `Building menu` — building selection
- `Militia Requirements` — militia requirements screen
- `Placement` — settlement placement map
- `Structure Rotation` — structure rotation/placement
- `visable` — visibility/visibility-related screen
