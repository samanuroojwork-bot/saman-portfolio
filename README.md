# Saman's Portfolio

A single-page static portfolio site. Deployed as plain static files — **no build step required**.

Live domain: **samanurooj.com** (once DNS is connected)

## What this is

The page was authored in [Claude Design](https://claude.ai/design). It uses Claude Design's
lightweight client-side runtime (`support.js`) rather than a framework build. On load, `support.js`:

1. Ensures React 18 is available (we vendor it locally under `vendor/` so the page has **no
   external CDN dependency** at load time), then
2. Parses the `<x-dc>` template + the `<script type="text/x-dc">` component logic in `index.html`
   and mounts it into `#dc-root`.

Everything renders client-side. There is nothing to compile.

## File structure

```
index.html      The page: template + component logic (was "SAMAN Portfolio.dc.html")
support.js       Claude Design runtime (parses <x-dc>, mounts React). Do not edit by hand.
vendor/          React 18 UMD builds, vendored so no CDN is needed at runtime
uploads/         Local media (category cover videos, logo, comic still)  ← see "Media" below
assets/          Local posters (AMARRIS coffee-table-book poster)        ← see "Media" below
```

## Media — IMPORTANT

Most of the portfolio's media is **not** in this repo. It is loaded at runtime from
**Google Drive** — 321 files total:

- ~160 video clips (Video Editing section), played via `drive.google.com/file/d/<id>/preview` iframes
- ~140 still images (Graphic Design, Motion Graphics), shown via `drive.google.com/thumbnail?id=<id>`
- ~20 packaging / comic / coffee-table items

Only a small set of local assets live in the repo (`uploads/`, `assets/`): the header/footer logo,
the 9 category cover videos, one comic still (`7.png`), and the AMARRIS poster.

**Reliability note:** Google Drive is not a CDN. At this scale it can rate-limit, and its `/preview`
video player carries Drive's own UI. Migrating videos to a real video host (e.g. Bunny Stream or
Cloudflare Stream) and committing the images into this repo is recommended for long-term reliability.
See the deploy notes shared alongside this project.

## Local preview

```bash
python3 -m http.server 8099
# then open http://localhost:8099
```

## Deploy

Static hosting, no build command, output directory = repo root. Works on Cloudflare Pages,
Netlify, or Vercel with default static settings.
