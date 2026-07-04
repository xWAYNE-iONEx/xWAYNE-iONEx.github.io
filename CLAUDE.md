# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with this repository.

## Repository purpose

This is the source for `xWAYNE-iONEx.github.io`, a GitHub Pages site for **-WAYNE-**, an
independent blockchain/smart-contract security researcher. It's a marketing/portfolio
site advertising audit services (pre-launch audits, live protocol reviews, security
retainers) and showcasing past findings (e.g. the "Sanctum Infinity" audit).

## Tech stack

There is no build system, package manager, or framework. The entire site is hand-written,
self-contained static HTML:

- Plain HTML5 + embedded `<style>` CSS + embedded `<script>` vanilla JS in each page.
- No `package.json`, no bundler, no CSS/JS linting, no test suite, no CI.
- Fonts are loaded from Google Fonts via `<link>` (`Share Tech Mono`, `Syne`, `DM Sans`).
- GitHub Pages serves this repo directly from the default branch root — `index.html` is
  the entry point, and any other `.html` file is reachable at its own path
  (e.g. `/WAYNE-classified.html`).

## File structure

- `index.html` — the main landing page (hero, manifesto/directives, audit portfolio
  ("scan log"), services/capabilities, process steps, CTA, footer). Contains a canvas-based
  particle-sphere animation and a dark/light mode toggle (`data-mode` attribute on `<html>`,
  driven by CSS custom properties in `:root` / `[data-mode="light"]`).
- `WAYNE-classified.html` — a standalone "classified audit report" teaser page with a
  password gate. On correct password it redirects to `WAYNE-sanctum-infinity-audit.html`,
  which **does not currently exist** in the repo — that page needs to be added before this
  link will work.
- `README.md` — effectively empty (just the string `# index.html`); not meaningful docs.

## Conventions used in this codebase

- **Design language**: a "terminal / security-scan" aesthetic — monospace
  (`Share Tech Mono`) for labels/system text, `Syne` (heavy weight) for display headings,
  uppercase letter-spaced micro-labels prefixed with `//` or `SYS://`, amber/gold accent
  color (`#ffd000` / `#f0c000`), near-black surfaces, scanline/vignette/gloss overlay
  layers via pseudo-elements.
- **Theming**: colors are defined as CSS custom properties on `:root` and overridden under
  `[data-mode="light"]`. All themed elements transition via a shared `--transition` var.
  When adding new UI, define new colors as tokens in both blocks rather than hardcoding hex
  values inline.
- **Class naming**: short, terse, abbreviated class names (`.sec-t`, `.mt`, `.svc`, `.ps`,
  `.acard`, `.bdg`) rather than BEM or long descriptive names. Follow the existing
  abbreviation style within a section rather than introducing a new naming scheme.
- **No inline `<script src>` includes** — all JS lives inline at the bottom of the page
  it belongs to (self-contained pages, no shared JS file).
- **Copy/tone**: all body copy is written in a terse "system log" voice
  (`SCAN_RESULT:`, `THREAT_LEVEL: ACTIVE`, `STATUS: PENDING`) — match this voice when
  editing or adding page copy.

## Working with this repo

- There's nothing to install and nothing to build. To preview changes locally, just open
  the HTML file in a browser, or serve the directory (e.g. `python3 -m http.server`) and
  visit `http://localhost:8000/index.html`.
- There is no test suite or linter to run. Verify changes by opening the page in a browser
  and checking both dark and light mode (via the mode toggle button) and at a few
  viewport widths (the layout has a `max-width:600px` breakpoint for mobile).
- Because pages are single self-contained files with large embedded `<style>`/`<script>`
  blocks, use targeted edits (`Edit`, not full rewrites) and search by the existing class
  name or CSS variable rather than rewriting whole sections.

## Security note

`WAYNE-classified.html` implements its "password gate" entirely in client-side
JavaScript, with the plaintext password (`const PASSWORD = 'xWAYNE2026'`) visible in the
page source. This provides no real access control — anyone can read the password from
view-source or bypass the check entirely. Treat it as a UI/marketing gimmick, not a
security boundary, and don't extend this pattern to protect anything that actually needs
to stay private.
