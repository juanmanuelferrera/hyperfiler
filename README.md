# HyperFiler Pro (gtd-claude)

HyperFiler Pro is a GTD-style task manager built as a PWA: a static front end (`hyperfiler-pro.html` is the app, `index.html` is the website) backed by Cloudflare Workers (Hono, D1, Stripe) with offline support through a service worker.

## Structure

- `hyperfiler-pro.html`, `index.html`, `login.html`, `register.html`, `success.html`, `cancel.html` (plus `-es` variants for some) — app and site pages.
- `js/` — front-end scripts (auth, backup/import, dark mode, keyboard shortcuts, globals, list operations, etc.) and `js/core/`.
- `sw.js`, `manifest.json` — service worker and PWA manifest.
- `hyperfiler-backend/` — backend Worker (`worker.js`, `lists-sync.js`, `migrations/`, `wrangler.toml`).
- `sync-worker.mjs`, `user-sync-do.js`, `wrangler.sync-worker.toml` — sync Worker with a Durable Object.
- `mcp-server/` — MCP server.
- `hyperfiler_elisp/` — Emacs Lisp client (`hyperfiler.el`).
- `email-templates/` — welcome and promo emails.
- `deploy*.sh`, `rollback-to-happy1.sh`, `verify_v2.0.7_deployment.sh` — deployment and rollback scripts.
- Many `*.md` notes: `CHANGELOG.md`, `DEPLOYMENT.md`, `STRIPE_SETUP.md`, `EMAIL_SETUP.md`, `SECURITY_FIXES.md`, restore and backup guides, and `CLAUDE.md` with the deployment rules.

## Usage

```sh
python3 -m http.server 8000     # serve the static front end locally
npm run dev                     # wrangler dev (Worker)
npm run deploy                  # wrangler deploy
npm run db:migrate              # apply D1 migrations (db:migrate:local for local)
npx wrangler pages deploy . --project-name=hyperfiler   # publish the front end
```

Per `CLAUDE.md`, the Pages project is `hyperfiler` (never `hyperfiler-fresh`), and cache-busting version strings in `hyperfiler-pro.html` must be updated when JS files change.

## Status

- Latest commits remove machine-generated output from version control and move the pending ideas from the retired `tasks.org` into `PROGRESS.md` (18-Oct-2026).
- `PROGRESS.md`: no open work; the ideas listed there are not committed tasks.
- An earlier version of this README described a 23-module ES6 refactor under `src/modules/` with 627+ tests; that tree is not present in the repo.
