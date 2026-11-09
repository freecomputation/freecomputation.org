# freecomputation.org

The website of the **Free Computation Foundation**.

*Computation should be free.* The free software movement freed the code; this
foundation frees the computing — local, offline, verifiable, unrented. The site
presents the mission, the Four Freedoms of Computation, how the vision differs
from free software's, the foundation's programs, and its projects (CENTL,
Krell, the Erdős–Straus Observatory).

## What this is

A static site with no build step and no external requests:

- `index.html` — the whole site (self-contained CSS, inline SVG favicon, JSON-LD)
- `robots.txt`, `sitemap.xml`, `llms.txt` — the discovery pack
- `_headers` — security headers for Cloudflare Pages (nosuchmachine-grade:
  HSTS, CSP, frame denial, nosniff, referrer policy)
- `CNAME` — `freecomputation.org`, for GitHub Pages if that route is used

Home on GitHub: [github.com/freecomputation](https://github.com/freecomputation)

## Wiring (deploy) — two routes, one decision

The domain's DNS is on Cloudflare. The old site was served from a LibreBoot X200
through a Cloudflare Tunnel (centl-web :8088, caravan :8789); that origin is
offline, so every hostname currently returns Cloudflare 530 / error 1033.

**Route A — Cloudflare Pages (house pattern: krell.cc, anatomica.cc)**
1. Cloudflare dashboard → Workers & Pages → Create → Pages → Upload assets →
   project name `freecomputation-org`, upload this folder (without README.md).
2. Custom domains: add `freecomputation.org` and `www.freecomputation.org`.
   Adding the Pages domain replaces the dead tunnel DNS records for `@`/`www`.
3. Redirect rule: `www` → apex (301), matching the canonical URL.
4. `caravan.freecomputation.org` stays tunnelled — it rejoins when the X200 returns.

**Route B — GitHub Pages on the new account**
1. Create repo `freecomputation/freecomputation.org`, push this folder to `main`.
2. Settings → Pages → deploy from `main` / root. The `CNAME` file binds the domain.
3. In Cloudflare DNS, point `@`/`www` at GitHub Pages (the tunnel records for
   those names must be removed; keep `caravan`).

Either way, verify after deploy by probing the live addresses for the new-version
marker — the hero line “Computation should be free.” and “The four freedoms of
computation” — on `/`, `/robots.txt`, `/sitemap.xml`, and `/llms.txt`.
A 200 without the marker is the old artifact, not this site. (Note: this repo
already exists on the new account as `freecomputation/freecomputation.org`,
created 2026-11-09 with an AGPL-3.0 LICENSE; Route B is therefore the live
route — push these files alongside that LICENSE, do not overwrite it.)

## License

Site content: CC BY 4.0. CENTL software: Apache-2.0.
