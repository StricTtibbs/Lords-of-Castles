# Lords of Castles — Base44 dev notes

## What this project is
A static HTML game prototype ("Lords of Castles"). The repo is a flat collection of
files with **no file extensions** and **spaces in their names**. Most are standalone
HTML pages (each a self-contained screen with inline CSS/JS); the rest are C++ headers
and design notes that are NOT browser-runnable.

## Browser-runnable HTML screens
`Main menu`, `visable`, `Building menu`, `Placement`, `Structure Rotation`,
`Backyard Extensions HTML`, `Terrain generation HTML`, `Calendar and Seasons`,
`Militia Requirements`, `AI Adverseries`, `Construction logic C++ and HTML`.

Non-runnable (C++ / notes): `3D`, `Consume food and food storage`, `Food itself`,
`Game logic`, `New Families`, `People detail`, `Realism Terrain`, `Starting food`,
`Starting game`, `Terrain Generation C++`, `Trees Detail`, `backyard extension C++`,
`calendar and Season C++`.

## How it runs here
No build step, no backend, no package dependencies (`package-lock.json` is empty).
Served as **static files** by `python -m http.server` on port 3000 via
`docker-compose.base44.yml`. An `index.html` at the repo root lists every screen
with URL-encoded links (file names contain spaces → `%20` in URLs).

## Editing
Edits to any HTML file are visible on browser refresh (no live-reload/HMR — these are
plain static files). After editing, call `reload_preview` so the user sees it.

## Verify it works
`docker compose -f docker-compose.base44.yml up -d`, then `curl -I http://localhost:3000/`
(expect 200) and `curl -I 'http://localhost:3000/Main%20menu'` (expect 200).

## Secrets
None — fully static, no external services.
