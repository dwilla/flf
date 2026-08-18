# Agent instructions for this repo

This repo is the marketing/donation website for Fourth Light Farm, a small sustainable-agriculture nonprofit. The person requesting changes is very likely **non-technical** — a farm staffer or board member describing what they want in plain language, not a developer reading a diff. Optimize for making the smallest, safest edit that achieves what they asked for, and explain what you changed in plain terms afterward.

## What this site is

A single static HTML page. No framework, no build step, no package manager, no dependencies to install.

- `index.html` — everything: markup, all page sections, and a small inline `<script>` at the bottom for the mobile nav toggle, smooth scrolling, the newsletter form submission, and donation-return notifications.
- `theme.css` — all custom styling, layered on top of the Bulma CSS framework (loaded from a CDN in `index.html`, not vendored in this repo).
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

- The donate section has six tier buttons: one-time (`#oneTimeDonateBtn5`, `#oneTimeDonateBtn10`, `#oneTimeDonateBtnCustom`) and monthly (`#monthlyDonateBtn5`, `#monthlyDonateBtn10`, `#monthlyDonateBtnCustom`). They link to per-tier placeholders like `YOUR_ONE_TIME_5_PAYMENT_LINK_HERE` and `YOUR_MONTHLY_CUSTOM_PAYMENT_LINK_HERE`. These are unset placeholders, presumably meant for individual Stripe payment links per tier. If the user gives you real payment links, swap them in. If they ask you to "fix the donate buttons" without providing links, ask them for the actual payment URLs rather than inventing them.
- The newsletter form submits to a hardcoded Google Apps Script URL (`SCRIPT_URL` near the bottom of `index.html`). That script lives outside this repo. If the user wants to change what fields the form collects (e.g. add a "zip code" field), the Apps Script itself will also need updating elsewhere — mention this rather than assuming the field will silently start working.

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
