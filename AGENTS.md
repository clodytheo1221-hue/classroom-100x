# Base44 Dev Environment

## Overview
Static HTML site ("Classroom 100x") — a small arcade landing page (`index.html`)
linking to individual game pages (`slope.html`, `retro-bowl.html`). No build step,
no package manager, no backend, no external credentials.

## Running
```
docker compose -f docker-compose.base44.yml up -d
```
Serves the repo root via `nginx:alpine` on host port 3000. Files are bind-mounted
read-only, so edits appear instantly — no reload needed.

## Quirks
- The repo root directory can have `700` permissions, which blocks nginx's
  non-root worker. If you get a 403, run `chmod 755 .` and restart the container.
- Game pages embed external iframes (`googleusercontent.com`); those may be blank
  in sandboxed previews but the site itself renders fine.

## Verification
- `curl -s http://localhost:3000/` should return the `index.html` content.
- Healthcheck: nginx serves `/` with 200.
