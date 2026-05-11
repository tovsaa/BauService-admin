# BauService Admin Panel

Admin panel for managing banners and projects displayed on
[bauservice-esw.de](https://bauservice-esw.de/).

Live at: **https://admin.bauservice-esw.de/**

## Tech

- Single static HTML file (`index.html`) deployed to GitHub Pages
- Talks to Supabase (`oevqnbgqxlczpyawdchw.supabase.co`) for data + auth
- Auth: Supabase email/password — RLS on `banners` and `projects` tables
  restricts writes to authenticated users
- Self-hosted Montserrat + Manrope fonts in `/fonts`
- No build step

## Deploy

Push to `main` → GitHub Pages auto-deploys.

The custom domain `admin.bauservice-esw.de` is configured via:
- `CNAME` file in repo root (tells GH Pages which domain)
- DNS record at Porkbun: `admin` → `<github-username>.github.io`
