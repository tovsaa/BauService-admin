# BauService Admin Panel

Admin panel for managing portfolio projects displayed on
[bauservice-esw.de](https://bauservice-esw.de/).

**Live:** https://admin.bauservice-esw.de/

## Features

- **Projekte tab** — full CRUD for portfolio projects with drag-and-drop
  photo reordering and multi-file upload (stored in Supabase Storage)
- **Banner tab** (dev) — manage promotional banner content (use case still
  pending, kept for future use)
- Email/password authentication via Supabase
- Indexing disabled (`<meta name="robots" content="noindex, nofollow">`)

## Tech

- Single static HTML file (`index.html`) — no bundler, no build step
- Self-hosted Montserrat + Manrope fonts (DSGVO-clean, no Google Fonts CDN)
- Supabase (`oevqnbgqxlczpyawdchw.supabase.co`) for data, storage, and auth
- Deployed via GitHub Pages on `main`

## Security model

Only the **anon (publishable) key** is embedded in `index.html`. Write
access is protected by:

1. Supabase **email/password auth** — admin must sign in
2. **Row-Level Security policies** on `banners` and `projects` tables:
   - `anon` role: `SELECT` only on rows where `active = true`
   - `authenticated` role: full CRUD

The service-role key is **never** in this repository. It is kept only in
the project owner's password manager.

## Local development

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

The page talks to the live Supabase backend; no local setup needed.

## Deploy

Push to `main` → GitHub Pages auto-deploys in ~30-60 seconds.

GitHub Pages settings:
- Source: deploy from a branch
- Branch: `main`, folder: `/` (root)
- Custom domain: `admin.bauservice-esw.de`
- Enforce HTTPS: ✓

DNS (Porkbun): CNAME record `admin` → `tovsaa.github.io`.

## Related repositories

- **Main site:** [`tovsaa/BauService`](https://github.com/tovsaa/BauService)
  — live at https://bauservice-esw.de/

## License

Proprietary. See [`LICENSE`](./LICENSE).
