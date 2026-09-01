# CLAUDE.md

Standing policy for this repository. Read it before making any change here.

## What this repo is

A Cloudflare Workers static-assets site. Everything served lives in `public/`
and there is no build step - the files in that directory are the site. The repo
is connected to Cloudflare Workers Builds, so **every push to `main` deploys to
production**.

```
public/            everything served
  index.html       the new one-page site
  offer/           the offer page
  fonts/           self-hosted Plus Jakarta Sans (@fontsource)
  404.html
  _headers         security + caching headers
  robots.txt       disallow all — pitch demo, never indexed
wrangler.jsonc     assets-only config, no Worker script
package.json       wrangler devDependency + dev/deploy scripts
work/brief.json    the sourced brief every on-page fact traces to
```

## Local development

```bash
npm install
npm run dev          # wrangler dev
```

## Verification - before every push to main

1. `npx wrangler deploy --dry-run`
2. Serve `public/`, render it with headless Chromium, and inspect the
   screenshots: styles applied, fonts loaded, layout intact.
3. This repo also carries the site-pitch layout gate — run
   `verify-layout.js` (site-pitch skill) on `/,/offer/` with
   `--fonts "Plus Jakarta Sans" --original-host glent.com`. Single pass:
   since the current-site tab was removed (2026-09-01), nothing served may
   reference glent.com.

Never leave pushed work unverified or half-finished. Work in small, complete
batches: implement, verify, commit, push.

## Git and release workflow

- Before committing: `git config user.name "Fid" && git config user.email "fid_kk@proton.me"`
- Develop on the working branch and push there first. Release verified work by
  fast-forwarding `main` onto it and pushing `main`.
- Every push to `main` is a release. Versions are an ascending `vMAJOR.MINOR`
  sequence starting at `v1.0`; every push bumps the minor regardless of size. A
  major bump is reserved for a ground-up overhaul.
- With every push to `main`, provide release-tag text in the reply, in exactly
  this shape. The owner creates the GitHub release manually - **never push tags**:

  ```
  Tag: v<next>  —  Title: <five to nine words, plain and evocative>
  Description: <one to three sentences of editorial prose describing what changed
  from the owner's point of view — outcomes, not implementation. No bullet lists,
  no jargon, no file names.>
  ```

- Append the release line to the ledger below as part of the same push.
- Commit messages: descriptive imperative first line (what the change does, not
  "update X"), then a short prose body; dash bullets are fine there. One commit
  per coherent piece of work; several may share a push, but each push gets
  exactly one version entry.
- Never include model names, AI attribution trailers, session links, or other
  tooling identifiers in commit messages, titles, or code.

## The page itself

Content, design, and behaviour are as supplied by the owner. Do not tidy markup,
rename classes, rewrite copy, or modernise CSS unless asked - changes to the
design are their own release, requested deliberately.

Facts on the new site trace to `work/brief.json`; the TO CONFIRM chip on the
Danish phone number is deliberate (glent.com lists a +44 number there) — do not
remove it without the client's answer.

The offer page carries no prices — removed at the owner's instruction on
2026-08-28. Do not reintroduce the fee sheet without being asked.

The HSEQ section on the new site carries owner-supplied copy (2026-09-01). Its
four NQA marks are inline-SVG recreations — the badge images arrived as chat
pastes that never reached disk. When the owner supplies the official files,
swap them in; do not redraw or restyle the recreations.

Photography is owner-supplied from their saved copy of the glent.com homepage
(2026-09-01); optimised derivatives live in `public/assets/img/`. The homepage
projects video is not in the repo — the page-save held only its CDN link, and
the host is blocked from this environment — so ask for the video files before
adding it.

The contact form is demo-wired: submitting shows a confirmation and delivers
nothing, because the enquiry inbox is unconfirmed (glent.com obfuscates its
email addresses). Wire it to the confirmed inbox or a Worker endpoint on
go-live, and keep its TO CONFIRM chip until that lands.

The team section's names and roles came from public-profile aggregators
(2026-09-01); only Alan Ferguson is multi-source confirmed. Do not add,
remove or retitle people without the client's answer. The placeholder
portraits and the /technology/ placeholder page are deliberate until real
assets and content arrive.

## Release ledger

| Version | Title | Description |
| --- | --- | --- |
| v1.0 | The Glent pitch demo, three tabs, verified | New one-page site for Glent Group built from their own facts, their live site framed alongside it, and the offer page carrying the standard numbers. Layout verified 320–1920 with self-hosted fonts. |
| v1.1 | Dressed in the real brand, priced in silence | The demo now wears Glent's actual identity — their petrol teal, their orange, their logo and typeface — and the offer page drops every number to sell the improvements alone. |
| v1.2 | The demo moves into its own home | The pitch demo now lives in its own GitHub repository, wired for Cloudflare hosting so every change pushed to main goes straight to the live site. The pages themselves are untouched — this release is the ground under them. |
| v1.3 | The safety credentials take their place | The new site now tells the health, safety, environment and quality story — the injury-free goal, the certified integrated management system and its intended outcomes, and the NQA marks for ISO 9001, 14001 and 45001 — set in the same clean style as the rest of the page. |
| v1.4 | The demo drops the framed original | The pitch is now two tabs — the new site and the offer. The framed view of the current glent.com no longer ships with the demo; it stays in the project's history if it is ever wanted back. |
| v1.5 | The real sites step into the picture | The demo now shows Glent's own photographs — the Frankfurt flagship from the air beside the headline, two live sites backing the project register, and a Glent crew at work alongside the safety story, which now closes the page. The homepage film waits on its file. |
| v1.6 | Ways to get in touch, always in reach | The new site now takes enquiries: a proper contact form sits with the offices, and call and enquiry buttons stay in the corner of the screen wherever the page is scrolled. Until the receiving inbox is confirmed, the form is a working preview rather than a live letterbox. |
| v1.7 | A proper face for shared links | When the demo's address is sent by message or posted anywhere, it now unfurls as its own card — the Frankfurt flagship from the air behind the Glent mark and the one-line pitch — instead of a bare link. |
| v1.8 | The people step forward, contact closes the page | The demo now introduces the group's leadership in a sliding row of profiles — names, roles and ways to reach each of them, portraits to follow — adds a technology section with its own showcase page held by a placeholder, and moves the enquiry desk to the very end, so the page finishes where a conversation starts. |
| v1.9 | The team row turns its own pages | On a computer the team now moves by arrow buttons at either side instead of a scroller; on a phone it stays a sideways swipe. Same people, same cards — just a cleaner way to leaf through them. |
| v1.10 | The certificates line up in the middle | The four NQA marks now sit centred beneath the safety story instead of hugging the left edge — a small straightening of the page's closing section. |
