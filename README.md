# Master Microstructure Decode Format — publish package

This folder is a ready-to-publish package for Brijesh Kapuriya's *Master
Microstructure Decode Format*. It has not been pushed anywhere yet — nothing
here is public until you say go.

## What's inside

| Path | Purpose |
|---|---|
| `docs/index.html` | The full article as a self-contained, SEO/AEO/GEO-optimized HTML page (JSON-LD `TechArticle` + `FAQPage` schema, Open Graph, Twitter Card, semantic headings, table of contents). GitHub Pages serves this folder directly. |
| `docs/sitemap.xml`, `docs/robots.txt` | Standard discovery files. `robots.txt` explicitly allows GPTBot, ChatGPT-User, OAI-SearchBot, PerplexityBot, ClaudeBot, Google-Extended, CCBot, and Bingbot — the crawlers that actually feed AI-answer engines (this is the real lever for GEO/AEO, more than any "trick"). |
| `docs/<key>.txt` | IndexNow verification key (free, no-login protocol Bing/Yandex/Seznam/Naver use for near-instant re-crawl pings). |
| `.github/workflows/geo-aeo-seo-watchdog.yml` | The 5-hourly automation (see below). |
| `cross-post/*.md,*.txt` | Ready-to-paste versions for Dev.to, Hashnode, Medium, LinkedIn, Reddit, Hacker News, and X/Twitter — each already links back to the canonical GitHub Pages URL as `canonical_url` so you don't get hit with duplicate-content penalties. |
| `status/latest.md` | Auto-updated log the watchdog writes to on every run. |

## What the 5-hourly agent actually does (honest version)

Every 5 hours, `geo-aeo-seo-watchdog.yml` runs on GitHub's own infrastructure
(free for public repos) and:

1. **Checks the page is live** (5 retries with backoff).
2. **Pings IndexNow** — a free, key-based protocol that tells Bing, Yandex,
   Seznam, and Naver "this URL changed, re-crawl it now" instead of waiting
   for their normal crawl cycle.
3. **Pings Bing's sitemap endpoint** (best-effort; search engines change
   these endpoints without much notice, so this step is allowed to fail
   silently and the run continues).
4. **Refreshes a visible freshness stamp** on the page itself and commits it
   — freshness/recency is a real, documented ranking and AI-citation signal.
5. **Opens a GitHub Issue automatically** if the site goes down, so you get
   notified instead of silently losing traffic.
6. **Optionally checks real Google ranking position** — but only if you add
   a `SERPAPI_KEY` repository secret (see below). Without it, this step logs
   "skipped" rather than faking a number.

This is a real, continuously-running optimization loop. It is **not** a
ranking guarantee — see the section below on why no one can promise that.

## What you still need to do yourself

I deliberately did not (and cannot) do these — they either require your own
login credentials, cost money, or are irreversible publishing actions:

1. **Google Search Console** — verify `universalherbalcare-bk.github.io` (or
   your custom domain) and submit `sitemap.xml`. This is the single biggest
   lever for actual Google visibility and I cannot log into your Google
   account to do it. Takes ~5 minutes: https://search.google.com/search-console
2. **Bing Webmaster Tools** — same idea, https://www.bing.com/webmasters
   (can auto-import from Search Console).
3. **Real rank tracking (optional, paid)** — sign up for SerpApi or
   DataForSEO, then add the key as a GitHub Actions secret named
   `SERPAPI_KEY` (repo → Settings → Secrets and variables → Actions). The
   watchdog will start reporting your actual Google position automatically
   once that secret exists — no code changes needed.
4. **Cross-posting to Dev.to / Hashnode / Medium / LinkedIn / Reddit / Hacker
   News / X** — the content is ready in `cross-post/`, but I won't create
   accounts or post on your behalf. Paste-and-publish takes a few minutes
   per platform. (Dev.to and Hashnode both have simple personal-API-key
   publishing — if you want that automated too, generate a key from your own
   account settings and tell me; I'll wire it in and ask you to confirm
   before the first live post.)
5. **Custom domain (optional)** — see `docs/CNAME.example`.

## Why "#1, always, without failing a single time" isn't a real deliverable

Rankings on Google, Bing, and AI answer engines are decided by those
companies' own algorithms, which factor in thousands of signals including
ones no external party controls (competing pages, backlink profiles built
over months/years, evolving model behavior, personalization). Anyone selling
a guarantee of permanent #1 placement is either wrong or dishonest. What
*is* real and repeatable: clean technical SEO, correct structured data,
crawler access for AI bots, freshness signals, and genuine backlinks/citations
— all of which this package sets up and keeps maintaining automatically.

## Next step

Nothing is public yet. To go live I need your explicit go-ahead to:
1. Create a public GitHub repository under your account
   (`universalherbalcare-bk`) and push this content.
2. Enable GitHub Pages on it (serves `docs/index.html` publicly).
3. Enable the scheduled workflow (starts the 5-hourly runs).

Say the word and I'll do all three.
