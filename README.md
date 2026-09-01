# glent-web

Site-pitch demo for **Glent Group** (glent.com) — a two-tab pitch wired by a demo bar:

| Route | Page |
|---|---|
| `/` | The new one-page site — self-delivered CSA packages, Data Centres & Pharma, Europe |
| `/offer/` | The offer — tale of the tape, the improvements, terms (no prices, by instruction) |

The current-site tab (`/original/`, their live site in a frame) was removed at
the owner's instruction on 2026-09-01; it lives on in git history if wanted back.

A Cloudflare Workers static-assets site: everything served lives in `public/`, no build step.

## Local development

```bash
npm install
npm run dev          # wrangler dev
npm run check        # wrangler deploy --dry-run
```

## Deployment

Connect the repo in the Cloudflare dashboard (Workers & Pages → Create → Import a repository). Every push to `main` then deploys to production. This is a pitch demo: `robots.txt` disallows all, every page carries `noindex,nofollow`, and `_headers` adds `X-Robots-Tag` — it must never reach a search index.

## External resources

None. Everything served is local: fonts are self-hosted in `public/fonts/` (Plus Jakarta Sans 400/600/700 from npm `@fontsource`), no CDN fonts, no trackers, no third-party requests on any route.

## Facts and integrity

Every fact on the new site traces to `work/brief.json` (source + date seen, all read from glent.com on 2026-08-28). Known flags carried onto the page deliberately:

- The Danish office is listed on glent.com with a **+44 London number** (identical to the UK office's) — reproduced with a visible **TO CONFIRM** chip rather than silently repeated or silently "fixed".
- "Götenborg" on their contact page is corrected to **Göteborg** (postcode 411 04 is unambiguous) — flagged in the brief's conflicts.
- Brand colours (`#0F3D4B` petrol, `#FE5000` orange) are sampled from the owner-supplied header screenshot and logo file; the logo lockup and favicon come from that file. The typeface is **Plus Jakarta Sans, identified by eye** from the screenshot — confirm and swap if their CSS says otherwise.
- Photography is owner-supplied (2026-09-01, from a saved copy of glent.com's homepage): the FRA01 aerial on the flagship card, FR10x and EEMS02 on the project register, and the branded-PPE operative shot beside the HSEQ copy — optimised derivatives in `public/assets/img/`. Their homepage projects video was **not** in the page-save (browsers save only a link to it) and its CDN is blocked from this environment — supply the `.mp4`/`.webm` files themselves to add it.
- `/offer/` carries **no prices** at the owner's instruction — it sells the improvements; commercials are discussed off-page.
- The HSEQ section (`/#hseq`, added 2026-09-01) carries the owner-supplied copy of glent.com's Health & Safety page. The four NQA certification marks there are **inline-SVG recreations** of badge images pasted in chat — the pastes never reached the repo as files — so swap in the official artwork when it is supplied.

- The contact form (`/#contact`, added 2026-09-01) is **demo-wired**: submitting shows a confirmation but nothing is delivered — glent.com's enquiry address could not be read (Cloudflare email obfuscation), so the receiving inbox carries a TO CONFIRM chip. Wire it to the confirmed inbox (or a Worker endpoint) on go-live. Call/enquiry shortcuts float bottom-right on every scroll position.

Open questions for the client are listed in `work/brief.json → questions`.
