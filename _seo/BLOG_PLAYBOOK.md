# Blog publishing playbook (used by the 3x/week task)

Site: https://risereps.app (GitHub Pages, branch `main`, repo `rewiredrising/riserep-website`). Pushing to `main` deploys in ~1 min.
App Store URL (every CTA): https://apps.apple.com/us/app/risereps/id6765616023

## Steps per run

1. Read `_seo/content-plan.md`. Pick the first calendar row whose slug is not in the Published log.
2. Optional keyword re-check: Google autocomplete for the primary keyword (via WebSearch or the browser) to confirm it's still a live query. Swap to a confirmed close variant if needed.
3. Research: check the current top results for the keyword (WebSearch) and find what they miss. Gather 2–4 credible sources for any stat. Never invent numbers, studies, quotes, or reviews.
4. Write the post by copying the structure of `blog/alarm-clock-that-makes-you-get-out-of-bed/index.html` exactly (same head tags, nav, CSS, CTA card, final CTA, footer):
   - New folder `blog/<slug>/index.html`. Update title, meta description, canonical, og/twitter tags, dates (ISO, +08:00), BlogPosting / BreadcrumbList / FAQPage JSON-LD.
   - Visible FAQ must match the FAQPage JSON-LD text.
   - Kicker category: one of Wake-up alarms, Snooze & sleep, Morning routine, Morning workouts.
   - Mid-article CTA card + final CTA, both linking to the App Store URL.
   - Internal links: homepage + at least 2 earlier posts (once they exist). Also add a link to the new post from 1–2 relevant older posts where it fits naturally.
   - Related section: 3 cards, preferring real earlier posts over homepage sections.
   - Product facts only from `index.html` / `support.html`. No prices.
   - Voice: direct, warm, a bit punchy. Short paragraphs. Minimal em dashes. No filler intros.
5. Add a card for the post at the top of the `POSTS:START` block in `blog/index.html` (kicker `Category · Mon D, YYYY`).
6. Add the URL at the top of the `BLOG:START` block in `sitemap.xml`; update `lastmod` for `/` and `/blog/`.
7. Append a row to the Published log in `_seo/content-plan.md`.
8. Validate: every JSON-LD block parses; all internal `href`s resolve to files in the repo; title ≤ 60 chars; description ≤ 160 chars; primary keyword appears in title, H1, first paragraph, and one H2.
9. Commit `Blog: <title>` and push to `main`. Wait ~90s and confirm the live URL returns the post (WebFetch).
10. Report: title, live URL, primary keyword, next post in the queue.

## When the calendar runs out

Research 36 more topics (Applyra if reachable, Google autocomplete, competitor blogs, Reddit threads) and append them to the calendar with the same columns before writing.
