# freecomputation.org

The website of the **Free Computation Foundation**.

*Computation should be free* — run on your own machine, offline, verifiably,
without rent, accounts, or permission. The site presents the mission, the
Foundation's three tests for dependent computing, the Four Freedoms of
Computation, its programs, and its projects - idem, Umiak, and Siuti,
listed now that they are real: working, documented, and checkable.

## What this is

A static site with no build step and no external requests:

- `index.html` — the whole site: a static page with no JavaScript at all,
  in the old-school manner — white page, black text, plain links, minimal
  self-contained CSS. No buttons, no header bar, no logo mark.
- `robots.txt`, `sitemap.xml`, `llms.txt` — the discovery pack
- `_headers` — security headers (HSTS, CSP, frame denial, nosniff, referrer
  policy); honored by Cloudflare Pages-style hosts, ignored by GitHub Pages
- `CNAME` — `freecomputation.org`, the GitHub Pages custom-domain binding

Home on GitHub: [github.com/freecomputation](https://github.com/freecomputation)

## Wiring (live)

This repo — `freecomputation/freecomputation.org` — is the live route:
GitHub Pages serves `main` / root, and the domain was verified to the
`freecomputation` account by DNS challenge. In Cloudflare DNS, `@` carries
the four GitHub Pages A records and `www` a CNAME to
`freecomputation.github.io`, both DNS-only (unproxied, so GitHub can issue
the HTTPS certificate). `caravan.freecomputation.org` deliberately stays on
its Cloudflare Tunnel — it rejoins when its origin machine returns. The
repo's AGPL-3.0 LICENSE sits alongside these files; do not overwrite it.

Verify after any deploy by probing the live addresses for the current
markers — the line "Computation should be free." and the heading "The Four
Freedoms of Computation" — on `/`, plus `/robots.txt`, `/sitemap.xml`,
and `/llms.txt`. A 200 without the markers is a stale artifact, not this
site.

## License

Site content: CC BY 4.0.
