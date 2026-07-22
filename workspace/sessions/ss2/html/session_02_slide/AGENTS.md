# AGENTS.md — Session 02 HSSF deck

Thin deck on **hssf-slides@0.5.0**. Follow HSSF charter: preferred blocks only, minimal `deck.css`.

## Runtime

```bash
npx serve .
```

```js
window.HSSF.init(document.querySelector("[data-hssf-canvas]"));
```

CDN pin: `hssf-slides@0.5.0` (never `@latest`).

## Rules

- **Layout:** Tailwind utilities inside `.hssf-slide__inner` (`flex gap-6`, `flex-1`, …). Preflight off.
- **Do not** use `hssf-columns` / `hssf-grid` for page layout on this deck.
- **Brand blocks:** header, list, callout, compare, steps, code, agenda, defs, figure, term
- Fragments: bullets/steps + **callouts** (tip/warning/danger = reveal last). Compare cards: `hold`
- Architecture: `hssf-figure` + asset — not flow topology
- `styles/deck.css`: tokens only
- Footer: `© 2026 By Rikkei Academy - Rikkei Education - All rights reserved.`
