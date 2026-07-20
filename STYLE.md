# Pages Style Guide

Technical-memo aesthetic: ink on paper, high contrast, two typographic voices — serif for reasoning, monospace for data. Think LessWrong essay × printed RFC, not a dashboard. Hierarchy comes from weight, size, and rules. Never from color.

## Tokens

```css
:root {
  --paper:    #FBFAF7;  /* page bg — warm, never pure white */
  --ink:      #1A1A17;  /* text, heavy rules, the only "color" */
  --graphite: #4C4942;  /* secondary text — keep ≥7:1 on paper */
  --hairline: #E3E0D8;  /* light rules, table lines */
  --serif: Charter, "Bitstream Charter", "Source Serif 4", Georgia, serif;
  --mono: ui-monospace, "SF Mono", "JetBrains Mono", Menlo, monospace;
  color-scheme: light;
}
:root[data-theme="dark"] {
  --paper:#151412; --ink:#EBE9E3; --graphite:#AEAAA0; --hairline:#2E2C28;
  color-scheme: dark;
}
```

## Theme

- Light is the default identity. Dark is a token swap only — same rules, same weights, nothing redesigned. Because inverted blocks use `var(--ink)` bg + `var(--paper)` text, inversion semantics survive the swap automatically.
- Every page carries the switcher: `<button class="theme">` top-right (absolute, scrolls away), mono 10px uppercase, `◐` prefix, label shows the target theme. Persisted as `localStorage['pages-theme']`; a one-line script in `<head>` right after `<title>` applies it pre-render (no flash). Copy all three pieces (head snippet, button, toggle JS) from `ribbon-voice-pipeline/index.html`.

## Type

- Prose: serif, 16–17px / 1.6+, measure ≤ 680px.
- Headings: serif 700, tight tracking (−0.02em). h1 `clamp(36px, 5.5vw, 56px)`.
- Data voice: mono 10.5–13px. Labels uppercase with 0.1em+ tracking. Numbers `tabular-nums`.
- Emphasis is weight, never slant. `em { font-style: normal; font-weight: 600 }` globally.
- Inline code: bare mono at 0.85em, ink. No background pill, no border.

## Color

- Monochrome only: ink + graphite + hairline on paper. No accent hue — no blue, no green/red/yellow status colors.
- Status semantics via mono glyphs + weight: `+` pass, `×` fail, `~` hold.
- **Inversion marks terminal states.** A conclusive block (final state, closing verdict) may run reversed — paper text on solid ink. This is the only loud element on a page; use it once or twice, always for the same meaning.
- Selection: ink background, paper text.

## Layout

- Single column, 960px container. Prose blocks ≤ 680px; data blocks (tables, diagrams, grids) run full width. Narrow = reasoning, wide = data.
- Sections open with a 2px ink top rule + mono index + serif h2. Everything else uses 1px hairlines.
- Tables are open (FT-style): 2px ink head rule, hairline row rules, no outer box.
- Grids of items: hairline top rule per item + whitespace gaps. No panel backgrounds, no 1px-gap mosaic grids.

## Components

- **Pull paragraph / quote**: larger serif (~19px) with a short 2px ink rule above (~40px wide). Never a colored left border.
- **Stat row**: 2px ink rule on top, hairline column separators, mono numbers ~27px, uppercase mono labels below.
- **Flow / diagram rails**: 2px ink line, 9px square ink markers (paper ring to lift off the rail). Steps are typographic blocks — mono tag + bold serif title + graphite serif body. No card boxes.
- **State chains**: plain mono words joined by `→`; terminal state inverted (ink block, paper text).
- **Links**: ink with underline (graphite decoration color, 3px offset); hover thickens the underline. No link color.
- **TOC rail** (pages with 3+ sections): LessWrong-style fixed left nav, mono 11px, entries = page title (uppercase, bold) + numbered sections. Inactive: graphite with 1px hairline left border; active: ink, bold, 2px ink border. Hidden below 1400px. Scrollspy via the small vanilla-JS block in `ribbon-voice-pipeline/index.html` — copy it, change only ids/titles. Sections get `id="s01"…` and `scroll-margin-top`.

## Mobile

Every page must render at 390px wide with zero horizontal scroll (test: `document.documentElement.scrollWidth <= innerWidth`).

- Multi-column grids collapse via media queries (breakpoints in use: 720/680/640/560/420).
- Long mono runs (payload lines, footers) get `overflow-wrap:anywhere`.
- `<pre>` and wide tables scroll inside their own `overflow-x:auto` box — never the page.
- Section headers `flex-wrap` so right-aligned notes drop to a second line.
- Tighten `main` padding at ≤560px (48px 20px 72px).
- TOC rail and theme button must never overlap content: TOC hides <1400px; the button is absolute, not fixed.

## JS policy

Static pages, but two sanctioned scripts (copy from the reference page): TOC scrollspy and the theme toggle. Nothing else without a real reason.

## Never

- The default-AI look: dot grid backgrounds + blue accent (`#5b9dff` and family).
- Colored badges/chips, colored left-border quotes, italics, emoji in page content.
- Border-radius, shadows, gradients, glow/pulse animations.
- A designed-from-scratch dark mode — dark is only ever the token swap above.
- Muted low-contrast body text; secondary text stays high-contrast (graphite tokens).

Motion: effectively none. If any, one deliberate moment, and honor `prefers-reduced-motion`.
