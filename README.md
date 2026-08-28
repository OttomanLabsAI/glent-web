# glent-web

Site-pitch demo for **Glent Group** (glent.com) — a three-tab pitch wired by a demo bar:

| Route | Page |
|---|---|
| `/` | The new one-page site — self-delivered CSA packages, Data Centres & Pharma, Europe |
| `/original/` | Their live site shown in a frame (see note below) |
| `/offer/` | The offer — tale of the tape, £500 / £50, terms |

A Cloudflare Workers static-assets site: everything served lives in `public/`, no build step.

## Local development

```bash
npm install
npm run dev          # wrangler dev
npm run check        # wrangler deploy --dry-run
```

## Deployment

Connect the repo in the Cloudflare dashboard (Workers & Pages → Create → Import a repository). Every push to `main` then deploys to production. This is a pitch demo: `robots.txt` disallows all, every page carries `noindex,nofollow`, and `_headers` adds `X-Robots-Tag` — it must never reach a search index.

## The `/original/` tab

A clean local copy of glent.com could not be made from this build environment (the network proxy blocks the host — the capture script returns its block page). `/original/` is therefore the honest frame fallback: the **live** site in an iframe with the reason stated on the strip. If glent.com ever sends `X-Frame-Options`/`frame-ancestors` denying it, the strip's "open in its own tab" link is the remainder. Re-run the capture from an unrestricted environment to upgrade this tab to a true local copy.

## External resources

- `public/original/index.html` frames `https://glent.com/` (by design, see above).
- Everything else is local: fonts are self-hosted in `public/fonts/` (Oswald 500/700, Inter 400/600 from npm `@fontsource`), no CDN fonts, no trackers, no third-party requests on `/` or `/offer/`.

## Facts and integrity

Every fact on the new site traces to `work/brief.json` (source + date seen, all read from glent.com on 2026-08-28). Known flags carried onto the page deliberately:

- The Danish office is listed on glent.com with a **+44 London number** (identical to the UK office's) — reproduced with a visible **TO CONFIRM** chip rather than silently repeated or silently "fixed".
- "Götenborg" on their contact page is corrected to **Göteborg** (postcode 411 04 is unambiguous) — flagged in the brief's conflicts.
- Exact brand hex values and typefaces are **derived** (their CSS is unreachable from this environment): dark ground + white wordmark + orange accent observed; Oswald/Inter are the house defaults standing in until their files arrive.
- No client photography or logo files are used — their CDN is unreachable — so the page is typography-led. Ask for the photo pack and logo files.

Open questions for the client are listed in `work/brief.json → questions`.
