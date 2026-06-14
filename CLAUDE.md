# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

A collection of self-contained HTML slide decks built from Google Docs source material. No build step, no dependencies — each file opens directly in a browser.

- `contra-libertarianism.html` — Libertarianism & the Libertarian Party: critical overview (14 slides)
- `prisoners-dilemma.html` — The Prisoner's Dilemma: game theory explainer (11 slides)
- `liberty.html` — Positive & Negative Liberty: Isaiah Berlin's two concepts (13 slides)

## How slides are built

Each HTML file is fully self-contained (inline CSS + JS, SVG art embedded). The structure within each file:

- **`.slide` elements** inside `#deck` — each slide is `position: absolute`, shown/hidden via `.active` / `.exit` classes and CSS transitions.
- **`.art` divs** — absolutely positioned SVG illustrations, always the first child of a slide so they render behind content (`z-index: 0`). Content children use `z-index: 1`.
- **Slide types** have dedicated CSS classes: `.slide-title`, `.slide-section`, `.slide-quote`, `.slide-matrix`, `.slide-close`.
- **Navigation JS** at the bottom counts slides via `querySelectorAll('.slide')` — the counter display (`#counter`) must be updated manually when slides are added or removed.
- **Keyboard navigation**: ← → arrow keys are wired up in each file.

## Color palettes

`contra-libertarianism.html` uses gold as primary accent:
```
--gold: #c9a84c  --dark: #0f1117  --mid: #1c1f2e  --card: #252836
--accent: #e05c3a  --purple: #9b59b6  (self-sovereignty section)
```

`prisoners-dilemma.html` uses teal as primary accent:
```
--teal: #2ec4b6  --dark: #0d1117  --mid: #161b22  --card: #21262d
--red: #e05c3a  --green: #3fb950  --blue: #58a6ff  --yellow: #d29922
```

## Content source

Slides are generated from this Google Doc (must be shared publicly to fetch):
`https://docs.google.com/document/d/19HKmZ6LPjbdT-jPgzHyErqLZH_4u2wHNnItQgdlVRzs/edit`

To fetch updated content, export as plain text via:
`https://docs.google.com/document/d/19HKmZ6LPjbdT-jPgzHyErqLZH_4u2wHNnItQgdlVRzs/export?format=txt`
(This redirects — follow the redirect URL in a second fetch call.)

## Adding a new slide

1. Add the `.slide` div in the correct position within `#deck`.
2. Place the `.art` div as the **first child** if the slide has SVG art.
3. Update the `#counter` initial text (`1 / N`) to reflect the new total — the JS derives the real count dynamically but the initial render uses the hardcoded value.
4. Use the watermark pattern (`opacity: 0.06–0.08`, large size, centered) for section slides with dense card grids; use the prominent pattern (`opacity: 0.3–0.5`, right-aligned) for title/quote/divider slides.
