# CLAUDE.md

Guidance for Claude Code when working in this repository.

## Project

China Sourcing Intelligence Hub — a single-file interactive dashboard helping
Nigerian buyers (in-country and diaspora) source products from China. Seven
buyer-journey tabs: Categories, Platforms, Agents & Payment, Logistics &
Canton Fair, Import Process, Tools & Glossary, Safety & Disputes.

True north: anyone using this tool should be able to transact end-to-end
without needing outside help. Every feature decision should serve that goal
— inform, don't confuse.

## Stack & constraints

- Single static HTML file (`index.html`). No build step, no npm dependencies,
  no backend, no API calls.
- This is intentional. Keep it a single file unless explicitly asked to
  modularize. Zero-setup hosting (drag-and-drop to any static host) is a
  core requirement, not an accident.
- Vanilla JS only. No frameworks.
- Hosted on Cloudflare Pages via Git integration — every push to `main`
  auto-deploys, live within ~60 seconds.

## Architecture

- CSS lives in one `<style>` block. Uses CSS custom properties
  (`--variable-name`) for all colors — dark mode is default, `body.light`
  overrides the variables for light mode. Never hardcode a color outside
  the variable system.
- All content data lives as JS objects/arrays near the bottom of the
  `<script>` block: `CATS` (23 categories), `PLATS`, `LEAD_TIMES`,
  `RETAIL_GUIDE`, `GLOSSARY`, `TEMPLATES`, `CAL_2026`.
- Each of the 7 tabs has a `render*()` function called lazily on first
  visit, tracked via a `rendered{}` state object. Don't re-render a tab
  that's already been rendered.
- Card expand/collapse uses unique per-card IDs (`cx-${id}`) with
  `element.style.display` set directly in JS, not CSS classes. Deliberate
  — see gotcha #1 below.

## Known gotchas — do not reintroduce these

1. **Never add `!important` to `.cx { display: none }` or similar
   collapse/expand rules.** Inline styles set by JS
   (`element.style.display = 'block'`) lose to `!important` in a
   stylesheet, which silently breaks every expand/collapse interaction.
   This happened once already — keep `.cx { display: none }` plain, no
   `!important`.

2. **Never override a function by reassigning to the same name with an
   "_orig" capture pattern**, e.g.:
   ```js
   const _origRenderX = renderX;
   function renderX(){ _origRenderX(); /* ... */ }
   ```
   JS hoists all `function` declarations before sequential code runs, so
   the *second* declaration is what gets hoisted — `_origRenderX` ends up
   pointing at itself, causing silent infinite recursion. If you need to
   extend a render function, give the addition its own distinct name
   (e.g. `addContainerPlanner()`) and call it explicitly after the
   original — e.g. via `setTimeout(addX, 0)` in the tab-switch handler.

3. **CSS Grid stretches every cell in a row to match the tallest one.** If
   a card's expanded content makes it taller than its row siblings, the
   siblings visually appear to "open" too because their grid cells
   stretch. Fix is `align-self: start` on the card class (`.cc`) — don't
   remove it.

## Conventions

- IDs and classes: short, lowercase, abbreviated (`.cc`, `.cx`, `.ipnl`,
  `.tc`) — matches the existing dense naming style. Match it rather than
  introducing a new, more verbose pattern.
- Colour, spacing, radius values: always reference existing CSS variables
  (`var(--gold)`, `var(--bd)`, `var(--rsm)`, etc.) rather than new literals.
- New data entries (new category, new glossary term, etc.): follow the
  exact shape of an existing sibling entry before adding one.
- Commit messages: Conventional Commits — `feat:`, `fix:`, `docs:`,
  `chore:`, `style:`, `refactor:` prefixes.
- Update `CHANGELOG.md` for any user-facing change.

## Workflow

```bash
git add -A
git commit -m "feat: describe the change"
git push
```
Cloudflare Pages picks up the push automatically. No build command, output
directory is `/`.
