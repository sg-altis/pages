# pages

Standalone static HTML pages, one directory per page (`<slug>/index.html`), linked from root `index.html`. Deployed by pushing to `origin main` (github.com:sg-altis/pages).

- **Read `STYLE.md` before writing or editing any page.** Ink-on-paper monochrome editorial; serif prose + mono data; light default with dark as a token swap; no blue accent, no italics, no colored badges.
- Reference implementation: `ribbon-voice-pipeline/index.html` — copy its theme-switcher (head snippet + button + JS), TOC rail + scrollspy, and token block verbatim rather than re-deriving them.
- Every page: theme switcher; TOC rail when it has 3+ sections; must pass 390px wide with zero horizontal overflow (`scrollWidth <= innerWidth`).
- Pages are self-contained: inline CSS, no external assets. Only sanctioned JS: scrollspy + theme toggle.
- When adding a page, add its row to root `index.html` (title + mono date).
