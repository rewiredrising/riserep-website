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

## Localization (translations of posts)
The site is translated into the locales in `_i18n/config.json` (es, pt-BR, de, zh-Hans, ja, ar). Translated pages live at `/<code>/...`, e.g. `/de/blog/<slug>/`. See `_i18n/README.md`.

After the English post is finished and validated (before committing):
1. Run `python3 _i18n/i18n.py`. This refreshes the language switcher / hreflang blocks (a post copied from an older post otherwise keeps that post's alternates) and the `I18N` block in `sitemap.xml`. A new English post without translations is fine: it simply has no switcher yet.

After the English post is live (separate commit, so a translation problem never blocks the English post):
2. For each locale code in `_i18n/config.json` (except en): copy `blog/<slug>/index.html` to `<code>/blog/<slug>/index.html` and translate the copy in place: title, meta description, og/twitter tags, alt text, every visible string, TOC, FAQ and the FAQPage/BlogPosting/Breadcrumb JSON-LD text (the visible FAQ must still match the JSON-LD). Write natural, native SEO copy for that market (local search phrasing in title/H1/description), not a literal translation. Do NOT change markup, ids, hrefs, or anything between `<!-- i18n:... -->` markers; the script localizes links itself. Keep product names (RiseReps, App Store, iPhone) and all facts, numbers and citations unchanged; keep the non-diagnostic sleep wording.
3. Add the post card at the top of the `POSTS:START` block in each `<code>/blog/index.html` (translated, same markup as the English card, date in local format).
4. Run `python3 _i18n/i18n.py --stamp <code>` for each locale, then `python3 _i18n/i18n.py --check` (must end without `WARN missing`; `STALE` lines for the edited older posts / blog index are expected unless you also updated their translations).
5. If older English posts got a new internal link this run, either add the same link to their translations or leave them (they'll show as STALE, which is harmless).
6. Commit as "Blog i18n: <slug>" (stage `*/blog/<slug>/`, `*/blog/index.html`, the root `blog/` files the script touched and `sitemap.xml`) and push. If translation can't be completed, skip it, leave no uncommitted files behind (`git checkout`/remove the partial copies), and say so in the report — the English post stays published.

Never edit or remove the `I18N:START … I18N:END` block in `sitemap.xml` by hand.
