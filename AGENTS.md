# Agent instructions for this repo

This repo is the marketing/donation website for Fourth Light Farm, a small sustainable-agriculture nonprofit. The person requesting changes is very likely **non-technical** — a farm staffer or board member describing what they want in plain language, not a developer reading a diff. Optimize for making the smallest, safest edit that achieves what they asked for, and explain what you changed in plain terms afterward.

## What this site is

Static HTML pages. No framework, no build step, no package manager, no dependencies to install.

- `index.html` — the main page: markup, all page sections, and a small inline `<script>` at the bottom for the mobile nav toggle, smooth scrolling, the newsletter form submission, and donation-return notifications.
- `mission.html` — a second page with the farm's mission statement and the recurring scholarship commitment (currently: 4 scholarships of $500 each, every year 2026-2028). Links to `goals.html` for the full year-by-year breakdown.
- `goals.html` — a third page with the farm's three-year goals (2026, 2027, 2028), each as its own card of specific initiatives, plus the same scholarship commitment banner as `mission.html`.

Both `mission.html` and `goals.html` link back to `index.html`'s sections (e.g. `index.html#about`) since those sections only exist on the main page. Keep nav/footer structure in sync across all three files when any one changes.
- `theme.css` — all custom styling, layered on top of the Bulma CSS framework (loaded from a CDN in both HTML files, not vendored in this repo).
- `logo.svg` — the farm logo, used in the hero section.
- `CNAME` — GitHub Pages custom domain file. Only touch this if the user explicitly asks to change the site's domain.

Icons come from Font Awesome, also loaded via CDN. There is no npm/node project here — don't add `package.json`, a bundler, or a frontend framework unless the user explicitly asks for that kind of overhaul.

## Page structure (`index.html`)

Sections are identified by anchor IDs, referenced by the nav bar and footer links:

- `#home` — hero section with logo, tagline, "Get Involved" and "Support Our Mission" buttons
- `#about` — About Us copy
- `#help` — "How We Can Help" — three cards (Community Partnerships, Educational Workshops, Hands-On Learning)
- `#newsletter` — email signup form
- `#donate` — donation section with one-time and monthly buttons
- `#contact` — contact info (website, phone, email, social) and footer

When asked to add a new card, section, or nav item, follow the existing pattern (Bulma `columns`/`column`/`card` classes) rather than introducing new layout systems.

## Known placeholders — flag these, don't silently "fix" them

- The donate section has six tier buttons: one-time (`#oneTimeDonateBtn5`, `#oneTimeDonateBtn10`, `#oneTimeDonateBtnCustom`) and monthly (`#monthlyDonateBtn5`, `#monthlyDonateBtn10`, `#monthlyDonateBtnCustom`). Each links to a real Stripe payment link for that tier. If the user wants a tier's amount or link changed, update the `href` on the matching button id; don't invent a link if they ask for a new tier without providing one.
- The newsletter form submits to a hardcoded Google Apps Script URL (`SCRIPT_URL` near the bottom of `index.html`). That script lives outside this repo. If the user wants to change what fields the form collects (e.g. add a "zip code" field), the Apps Script itself will also need updating elsewhere — mention this rather than assuming the field will silently start working.
- The scholarship commitment ("4 Scholarships — $500 Each", every year 2026-2028) appears on both `mission.html` and `goals.html` and must stay in sync between them. It's a specific figure the user gave directly — don't change the number, years, or wording on either page without the user explicitly providing the new value.
- `goals.html`'s three year-by-year goal lists (2026, 2027, 2028) are specific initiatives the user gave directly — don't add, remove, or reword them without the user's input.
- Three "Apply Here!" buttons (`#scholarshipApplyBtnHome` in `index.html`'s hero, `#scholarshipApplyBtnMission` in `mission.html`, `#scholarshipApplyBtnGoals` in `goals.html`) all link to the scholarship Google Form at `https://forms.gle/4b7SmUfATuS27h1S7`. If the user gives a new form link, update it in all three files.

## Styling conventions

- All brand colors are CSS custom properties defined in `theme.css` under `:root` (e.g. `--flf-sage-green`, `--flf-earth-brown`, `--flf-medium-green`, `--flf-cream`). To re-theme the site (e.g. "make the green more forest-y"), change these variables rather than hunting for hardcoded colors throughout the file — but check for stray inline `style="color: ..."` attributes in `index.html` too, since a few exist.
- Prefer Bulma utility classes already in use (`has-text-centered`, `is-fullwidth`, `section`, etc.) over new custom CSS when possible.
- The site must stay responsive — there's a mobile breakpoint block at the bottom of `theme.css` (`@media screen and (max-width: 768px)`). Check any layout change against narrow viewports.

## Deployment

Hosted on GitHub Pages, serving directly from the `main` branch root — confirmed via the repo's Pages config (`build_type: legacy`, `source: main:/`). There is no CI workflow and no build step. **Any commit pushed to `main` goes live on fourthlightfarm.com automatically**, typically within a few minutes. This means:

- Don't push half-finished or obviously broken changes to `main`.
- There's no staging environment — if the user wants to preview before it's public, preview locally first (open `index.html` directly in a browser, or run `python3 -m http.server` and visit `localhost`) before committing/pushing.
- Only commit and push when the user actually confirms they want the change live — don't push proactively mid-conversation.

## General approach

- Make the smallest edit that satisfies the request. This is a small nonprofit site, not a codebase that needs abstraction or refactors.
- After editing, describe the change in plain, non-technical language (what changed and where on the page), not in terms of diffs or code.
- If a request is ambiguous (e.g. "make it pop more"), ask a clarifying question or make a reasonable interpretation and clearly say what you did, rather than guessing silently on something visual and hard to undo by eye.
