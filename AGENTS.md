# AGENTS.md — Lords of Castles

## What this is
A set of standalone static HTML/CSS/JS prototype screens for a medieval settlement game
("Lords of Castles"). There is no build step, no package manager, no backend, and no
dependencies. Each top-level file (e.g. `Main menu`, `Placement`) is a complete
`<!DOCTYPE html>` document with inline `<style>` and `<script>` blocks.

## File naming quirk
The source files have **spaces in their names** (`Main menu`, `Building menu`,
`Structure Rotation`, etc.). To open one in a browser, URL-encode the space as `%20`,
e.g. `/Main%20menu`. The pages do **not** link to each other — each is an independent
screen prototype.

## Running it
Served as static files by nginx via `docker-compose.base44.yml`:

```
docker compose -f docker-compose.base44.yml up -d
```

- nginx (alpine) bind-mounts the repo root read-only at `/usr/share/nginx/html`
  and exposes host port **3000**.
- A custom `nginx.conf` is mounted at `/etc/nginx/conf.d/default.conf`. It serves the
  `Main menu` file at `/` via a `302` redirect to `/Main%20menu` (the space can't be a
  literal nginx `index`/`try_files` argument). `absolute_redirect off` keeps the
  redirect relative so it works behind the preview proxy.
- `index.html` at the repo root is a leftover meta-refresh fallback; nginx's 302 takes
  precedence. Editing a game screen means editing its named file, not `index.html`.

## Permission gotcha
The repo root directory was mode `700`. nginx's worker (`nginx` user) could not
traverse it, causing `403 Forbidden`. The fix was `chmod 755 .` on the repo root. If a
fresh checkout shows 403s, re-run that.

## Healthcheck
Probes `http://127.0.0.1/Main%20menu` (IPv4 literal — nginx only listens on IPv4, and
`localhost` resolves to IPv6 first inside the container, which caused a spurious
"connection refused" / unhealthy state).

## Verifying
- `curl -sL http://localhost:3000/ | grep <title>` → `Lords of Castles`
- All six pages return 200: `Main menu`, `Banner`, `Building menu`, `Placement`,
  `Structure Rotation`, `visable`.
- No secrets or external services are required.
