# glent-web

Site-pitch demo for **Glent Group** (glent.com) — a three-tab pitch wired by a demo bar:

| Route | Page |
|---|---|
| `/` | The new one-page site — self-delivered CSA packages, Data Centres & Pharma, Europe |
| `/original/` | Their live site shown in a frame (see note below) |
| `/offer/` | The offer — tale of the tape, the improvements, terms (no prices, by instruction) |

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
- Everything else is local: fonts are self-hosted in `public/fonts/` (Plus Jakarta Sans 400/600/700 from npm `@fontsource`), no CDN fonts, no trackers, no third-party requests on `/` or `/offer/`.

## Facts and integrity

Every fact on the new site traces to `work/brief.json` (source + date seen, all read from glent.com on 2026-08-28). Known flags carried onto the page deliberately:

- The Danish office is listed on glent.com with a **+44 London number** (identical to the UK office's) — reproduced with a visible **TO CONFIRM** chip rather than silently repeated or silently "fixed".
- "Götenborg" on their contact page is corrected to **Göteborg** (postcode 411 04 is unambiguous) — flagged in the brief's conflicts.
- Brand colours (`#0F3D4B` petrol, `#FE5000` orange) are sampled from the owner-supplied header screenshot and logo file; the logo lockup and favicon come from that file. The typeface is **Plus Jakarta Sans, identified by eye** from the screenshot — confirm and swap if their CSS says otherwise.
- No photography is used (none supplied) — the page is typography-led. Ask for a photo pack if imagery is wanted.
- `/offer/` carries **no prices** at the owner's instruction — it sells the improvements; commercials are discussed off-page.

Open questions for the client are listed in `work/brief.json → questions`.
