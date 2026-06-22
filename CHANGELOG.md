# Changelog

All notable changes to this project are documented here. Format follows
[Keep a Changelog](https://keepachangelog.com/), versioning follows
[Semantic Versioning](https://semver.org/).

## [Unreleased]

### Added
- "Want This Handled For You?" sourcing consultation CTA card, now on
  the bottom of all 7 tabs (not just Import Process) so it's visible
  regardless of which part of the dashboard someone is browsing
- The CTA is gated: clicking it reveals a 5-question intake form
  (import category, budget, prior experience, urgency, preferred
  contact method) reusing the onboarding wizard's exact question/
  option styling. The WhatsApp link only activates once all 5 are
  answered, and the answers are packed into a pre-filled WhatsApp
  message so the brief arrives with the booking request — filtering
  for buyers serious enough to answer, and giving full context
  upfront instead of a cold "hi"

### Changed
- Category cards now show only the cheapest pricing tier on the face,
  with a "+N more pricing tiers" hint, instead of all 3 tiers always
  expanded — cuts default card height substantially (~12 cards fit
  in the same viewport that previously fit ~9) without removing any
  data; full tier breakdown is unchanged in the expanded detail view
- Filter bar collapsed: Region/Tier/Compliance pills and the Sort
  dropdown are now hidden behind a single "Filters" toggle button
  instead of always visible, cutting the bar down to one compact row
  (search + Filters + result count). The button shows a gold badge
  with the active-filter count even while collapsed, so an applied
  filter is never invisible. No filtering behaviour changed.

### Fixed
- Onboarding wizard "Edit profile" button referenced a nonexistent
  element ID and silently failed to reopen the wizard or reset filters
- Wizard form stayed visible after submitting a personalised plan
- Switching tabs no longer preserves scroll position from the previous
  tab — now resets to top
- Agent-vetting and import-document checklist progress is now saved to
  `localStorage` and restored on reload
- Fixed a CSS Grid bug where two/three-column layouts (Logistics,
  Tools, Agents, Import Process, Safety & Disputes) could grow wider
  than the viewport on mobile instead of collapsing to one column,
  causing horizontal scroll/clipped content on phones
- Glossary term accordions and import-checklist stage headers were
  mouse-only (no `tabindex`, no keydown handler) — keyboard users
  couldn't focus or toggle them. Added Enter/Space activation and
  synced `aria-expanded` state
- Filter result count ("X / Y shown") now has `aria-live="polite"` so
  screen readers announce changes when filtering categories
- `--t3` (tertiary text color, used for category descriptions, market
  names, platform URLs, and shipping notes) failed WCAG AA contrast in
  both themes (as low as 1.7:1 against card backgrounds). Replaced
  with values verified to pass 4.5:1+ against every background it
  renders on
- `--t2` (secondary text color, used for most body copy) also fell
  below AA on dark-theme card backgrounds (3.9–4.3:1). Adjusted to
  pass 6:1+ everywhere while staying visibly brighter than the fixed
  `--t3`, preserving the text/t2/t3 hierarchy
- Container Volume Planner's "Calculate" button silently did nothing
  if a dimension field was empty — now shows an inline message
  instead of no feedback
- Light/dark theme preference is now saved to `localStorage` and
  restored on reload instead of always resetting to dark

### Removed
- Dead CSS: an unused dispute-phase accordion component, an unused
  "Typical timeline" row variant superseded by `.bank-row`, and an
  unused nav "NEW" badge style — none were ever applied in markup

## [1.0.0] - 2026-06-20

### Added
- Seven-tab buyer journey: Categories, Platforms, Agents & Payment,
  Logistics & Canton Fair, Import Process, Tools & Glossary, Safety &
  Disputes
- 23 product category cards with tier pricing, compliance flags, lead
  times, and quick-quote integration
- Landed Cost Calculator and Container Volume Planner
- 21-term trade glossary and 5 supplier communication templates
- Chinese Business Calendar 2026
- 26-item import document checklist with progress tracking
- Nigeria port clearing step-by-step guide
- Retail viability guide with per-category margin calculator
- 72-hour dispute and arrival action plan
- Guided onboarding wizard for first-time buyers
- Light/dark theme, mobile bottom navigation, full keyboard accessibility
