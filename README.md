# Blocked BH-P IDs — standalone lookup

A single static page that checks whether a BH-P registration number is on the
Pharmacy Council of India blocked list (PCI Circular IT-11/3/2026-IT,
19 Nov 2026, Annexure-1).

No build step, no framework, no dependencies. Works offline after first load.

## Files

- `index.html` — the page (HTML + CSS + JS in one file)
- `data/blocked-bhp-2026-11-19.json` — the 44,730 blocked IDs (756 KB, 154 KB brotli)

## Run locally

```sh
python3 -m http.server 8000
# open http://localhost:8000
```

(or any static server; `file://` won't work because of `fetch`)

## Host for free

- **GitHub Pages** — push this folder to a public repo, enable Pages
- **Cloudflare Pages** — drag-and-drop the folder
- **Netlify** — drag-and-drop
- **R2** — upload as static assets

## Update when PCI publishes a new list

1. Regenerate `data/blocked-bhp-YYYY-MM-DD.json`
2. Update `DATA_URL` in `index.html`
3. Update the circular link and the count in the subtitle
4. Redeploy

## Source

Pharmacy Council of India, Circular IT-11/3/2026-IT (19-11-2026), Annexure-1.
Unofficial reference data — verify against the official circular.
