# Base44 Dev Environment

## Project Overview
"Lords of Castles" — a medieval settlement game prototype. The repo contains standalone HTML files (UI mockups/prototypes) and C++ files (Unreal Engine game logic headers/sources). There is no build system, no backend, and no npm dependencies.

## Running the App
- Served as static files via `nginx:alpine` on port 3000.
- The main entry point is the file `visable` (an HTML file titled "Medieval Settlement HUD"), configured as the nginx index.
- All other HTML files are accessible by their filename (e.g. `/Main%20menu`, `/Building%20menu`).

## Key Details
- File and directory names contain spaces; nginx handles URL-encoding automatically.
- The repo root directory has restrictive permissions (`drwx------`), so nginx must run as `user root;` (configured in `nginx.base44.conf`, mounted as `/etc/nginx/nginx.conf`).
- The healthcheck must use `127.0.0.1` (not `localhost`) because nginx only listens on IPv4.

## Verification
```bash
docker compose -f docker-compose.base44.yml up -d
curl -s http://localhost:3000/ | head -5   # should show <!DOCTYPE html>
docker compose -f docker-compose.base44.yml ps  # should show healthy
```

## No Secrets Required
This is a purely static project with no external service dependencies.
