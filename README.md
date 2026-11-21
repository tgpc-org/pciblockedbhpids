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

## How the check works

The annexure prints IDs as `BH-P-YY-NNNN` where the number after the dash is
**3 to 10 digits and leading zeros are significant** (3,865 IDs start with `0`,
mostly the 10-digit 2024 registrations). So:

- `BH-P-` and the decade digit `2` are fixed in the UI; you type the year digit
  (`3`–`6`, i.e. 2023–2026) and then the number.
- Matching is a sorted binary search over normalised IDs — exact match means
  blocked.
- While typing, the result stays at "Keep typing…" as long as some blocked ID
  still starts with what you have entered, so a partial number can never produce
  a "Not on the blocked list" answer.
- If the only close record is the zero-padded form (`BH-P-24-770508730` →
  `BH-P-24-0770508730`) or the same number under another year, that record is
  offered instead of a false "clear".

## Update when PCI publishes a new list

1. Regenerate `data/blocked-bhp-YYYY-MM-DD.json`
2. Update `DATA_URL` in `index.html`
3. Update the circular link, the format hint and the year counts in the footer
4. Redeploy

## Source

Pharmacy Council of India, Circular IT-11/3/2026-IT (19-11-2026), Annexure-1.
Unofficial reference data — verify against the official circular.
