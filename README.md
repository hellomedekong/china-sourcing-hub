# China Sourcing Intelligence Hub

A single-file interactive dashboard for Nigerian buyers sourcing products
from China — categories, platforms, agents, logistics, the full import
process, and a retail viability calculator.

## Live site
https://china-sourcing-hub.pages.dev

## Stack
Pure HTML/CSS/JS. No build step, no dependencies, no backend. Everything is
in `index.html`.

## Deploying changes
Connected to Cloudflare Pages via Git integration. Every push to `main`
triggers an automatic rebuild and deploy, live within ~60 seconds.

```bash
git add -A
git commit -m "feat: describe your change"
git push
```

## Working with Claude Code
Open a terminal in this folder and run `claude`. Describe the change you
want, review the diff, and let it commit and push when you're happy. See
`CLAUDE.md` for the project's architecture notes and known gotchas — Claude
Code reads this automatically.

## Structure
```
.
├── CLAUDE.md       # Context for Claude Code
├── CHANGELOG.md    # Version history
├── README.md       # This file
├── .gitignore
└── index.html      # The entire application
```
