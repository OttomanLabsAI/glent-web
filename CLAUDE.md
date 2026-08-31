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
  original/        their live site, framed (capture blocked — see README)
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
   `verify-layout.js` (site-pitch skill) two-pass: `/,/offer/` with
   `--fonts "Plus Jakarta Sans" --original-host glent.com`, then `/original/`
   alone (its iframe to glent.com is the sanctioned frame fallback).

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

## Release ledger

| Version | Title | Description |
| --- | --- | --- |
| v1.0 | The Glent pitch demo, three tabs, verified | New one-page site for Glent Group built from their own facts, their live site framed alongside it, and the offer page carrying the standard numbers. Layout verified 320–1920 with self-hosted fonts. |
| v1.1 | Dressed in the real brand, priced in silence | The demo now wears Glent's actual identity — their petrol teal, their orange, their logo and typeface — and the offer page drops every number to sell the improvements alone. |
| v1.2 | The demo moves into its own home | The pitch demo now lives in its own GitHub repository, wired for Cloudflare hosting so every change pushed to main goes straight to the live site. The pages themselves are untouched — this release is the ground under them. |
