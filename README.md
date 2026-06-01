# surat-townplan-tiles

Public static map tiles for the Surat town-planning app
([IIIAmigoes/surat-townplan](https://github.com/IIIAmigoes/surat-townplan), private).

This repo holds **only open-data-derived map assets** — no application code, no
secrets. It exists so the tiles can be served from a **public** GitHub Pages site
(the app repo is private) without exposing the app.

## Assets

| File | Description | Public URL |
|------|-------------|------------|
| `buildings-surat.pmtiles` | Surat building footprints (Overture Maps), z12–18 | https://iiiamigoes.github.io/surat-townplan-tiles/buildings-surat.pmtiles |

## Why GitHub Pages

The PMTiles client fetches tiles via HTTP **range requests** and needs **CORS**.
GitHub Pages serves static files with `Access-Control-Allow-Origin: *` and
`Accept-Ranges: bytes`, so it works as a zero-cost, zero-account PMTiles host.
This replaced an earlier Cloudflare R2 plan (COD-132) that was blocked on
human-gated account provisioning; the frontend reads a host-agnostic URL env var,
so swapping back to R2/a CDN later is a one-line change.

## Refresh

The PMTiles is rebuilt from Overture Maps (public S3, no auth) by
[`.github/workflows/publish-buildings.yml`](.github/workflows/publish-buildings.yml).
Run it via the Actions tab → "Build & publish buildings PMTiles" → Run workflow,
or:

```bash
gh workflow run publish-buildings.yml --repo IIIAmigoes/surat-townplan-tiles
```
