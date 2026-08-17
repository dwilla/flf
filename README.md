# Fourth Light Farm Website

The website for [Fourth Light Farm](https://fourthlightfarm.com), a sustainable agriculture and soil health nonprofit.

It's a simple, static website — just HTML and CSS, no build step, no server. That makes it easy to edit, including with an AI coding agent, even if you don't know how to code.

## Making changes with an AI agent (no coding experience needed)

You can update this site by describing what you want in plain English to [Claude Code](https://claude.com/claude-code) (or a similar AI coding assistant) and letting it make the edit for you.

1. **Open Claude Code in this project folder.** If you don't have it installed, see https://claude.com/claude-code for setup instructions. Once installed, open a terminal, navigate to this folder, and run `claude`.
2. **Say what you want changed, in plain language.** For example:
   - "Change the phone number in the Contact section to 603-555-0199."
   - "Add a new card to the 'How We Can Help' section about our composting program."
   - "Change the main green color used across the site to a deeper forest green."
   - "Update the Instagram link to our new handle."
3. **Review what it changed.** Claude Code will show you a diff (a before/after) of the file(s) it edited. You don't need to understand code — just read the section it changed and check that it looks right. Ask it to preview the page in a browser if you want to see it visually before finishing.
4. **Ask it to save and publish the change.** Say something like "commit this change and push it." Once pushed to the `main` branch on GitHub, the live site at fourthlightfarm.com updates automatically within a few minutes — there's no separate deploy step.

The file [`AGENTS.md`](./AGENTS.md) in this repo has more details for the agent about how this site is put together, its known placeholders, and things to be careful about. You don't need to read it yourself — the agent will use it automatically.

### Tips
- Make one change at a time and check the result before moving to the next.
- If something looks wrong after a change, just tell the agent what's wrong ("the button is now the wrong color") and it can fix it.
- You can always undo a change by asking the agent to revert the last commit, as long as it hasn't been pushed yet — or ask a technical friend to help revert a pushed change via `git revert`.

## What's in this repo

- `index.html` — the entire site (all sections: home, about, how we help, newsletter signup, donate, contact)
- `theme.css` — colors, fonts, and styling
- `logo.svg` — the farm logo
- `CNAME` — the custom domain configuration (fourthlightfarm.com)

## Previewing locally

No build step or install is required. Just open `index.html` in a browser, or serve the folder locally:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.

## Deployment

This site is hosted on GitHub Pages directly from the `main` branch. Any change pushed to `main` goes live automatically — there is no build or CI step in between.
