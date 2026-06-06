# UI/UX Operational Checklist

The measurable rules `/uiux` audits and fixes against. Each has a stable **ID**, a
**threshold** (so PASS/FAIL is objective), and a **default severity**. Severity may
rise if the violation blocks a core task.

Severity scale: `blocker` (task impossible / inaccessible) · `major` (significant
friction) · `minor` (noticeable) · `polish` (refinement).

---

## A11Y — Accessibility (WCAG 2.2 AA baseline)

| ID | Rule | Threshold | Default |
|----|------|-----------|---------|
| A11Y-CONTRAST | Text vs background contrast | ≥ 4.5:1 normal, ≥ 3:1 for ≥24px or ≥18.66px-bold; UI/graphics ≥ 3:1 | blocker |
| A11Y-ALT | Informative images have meaningful `alt`; decorative images `alt=""` | 100% of `<img>` | major |
| A11Y-LABEL | Every form control has a programmatic label (`<label for>`, `aria-label`, or `aria-labelledby`) | 100% | blocker |
| A11Y-HEADINGS | Exactly one `<h1>`; heading levels don't skip (h1→h2→h3) | per page | major |
| A11Y-LANDMARKS | Page uses semantic landmarks: `header`, `nav`, `main` (one), `footer` | present | major |
| A11Y-FOCUS | All interactive elements are keyboard-focusable with a visible focus indicator (never `outline:none` without a replacement) | 100% | blocker |
| A11Y-TABORDER | DOM/tab order matches visual order; no positive `tabindex` | per page | major |
| A11Y-NAME | Buttons/links have a discernible accessible name (icon-only needs `aria-label`/sr-only text) | 100% | major |
| A11Y-TARGET | Tap targets ≥ 24×24px (WCAG 2.2); aim 44×44 for primary touch actions | ≥ 24px | major |
| A11Y-MOTION | Honor `prefers-reduced-motion`; no essential info conveyed by motion alone | respected | minor |
| A11Y-COLORONLY | Meaning never conveyed by color alone (links underlined or otherwise distinct; states have text/icon) | always | major |
| A11Y-LANG | `<html lang>` set; direction correct | present | minor |
| A11Y-ALTTEXT-SVG | Inline SVGs are `aria-hidden` when decorative, or have `<title>`/`role="img"` + name when meaningful | 100% | minor |
| A11Y-FORMERR | Form errors are announced, tied to the field, and describe how to fix | per form | major |
| A11Y-ZOOM | Content reflows and stays usable at 200% zoom / 320px width; no horizontal scroll for text | passes | major |

## VIS — Visual design & hierarchy

| ID | Rule | Threshold | Default |
|----|------|-----------|---------|
| VIS-HIERARCHY | Clear visual hierarchy: one dominant focal point per view; primary action visually distinct | per view | major |
| VIS-TYPESCALE | Limited, consistent type scale (≈5–7 steps); body ≥ 16px; line-height 1.4–1.7 for body | conforms | major |
| VIS-MEASURE | Line length 45–85 characters for body text | within range | minor |
| VIS-SPACING | Consistent spacing scale (e.g. 4/8px rhythm); related items grouped, unrelated separated (proximity) | conforms | minor |
| VIS-ALIGN | Elements share alignment to a grid; intentional, not arbitrary | conforms | minor |
| VIS-PALETTE | Restrained palette with defined roles (brand, accent, neutral, semantic); consistent usage | conforms | minor |
| VIS-CONSISTENCY | Repeated elements (buttons, cards, inputs) look and behave consistently | consistent | major |
| VIS-DENSITY | Adequate whitespace; content not cramped or wall-of-text | balanced | minor |
| VIS-IMAGERY | Images sharp (correct resolution, no stretching/wrong aspect ratio), consistent treatment | correct | minor |

## USAB — Usability heuristics (Nielsen) & interaction

| ID | Rule | Threshold | Default |
|----|------|-----------|---------|
| USAB-FEEDBACK | System status is visible: loading, success, error, disabled, hover/active states | present | major |
| USAB-AFFORD | Interactive things look interactive; non-interactive things don't (cursor, styling) | clear | minor |
| USAB-NAV | User always knows where they are (active nav state, title, breadcrumbs where deep) | clear | major |
| USAB-CONSISTENCY | Conventions honored (logo → home, underlined links, standard icon meanings) | honored | minor |
| USAB-ERRORPREV | Prevent errors (constraints, confirmations for destructive acts, sensible defaults) | present | major |
| USAB-RECOVERY | Easy undo/back; clear exits from any state; helpful empty + error states | present | major |
| USAB-RECOGNITION | Options visible rather than requiring recall; minimize memory load | conforms | minor |
| USAB-EFFICIENCY | Common tasks are short; primary action reachable without hunting | conforms | minor |
| USAB-404 | Helpful 404/error pages with a route back | present | minor |
| USAB-FORMS | Forms: logical order, grouped fields, inline validation, no needless required fields | conforms | major |

## RESP — Responsive & cross-device

| ID | Rule | Threshold | Default |
|----|------|-----------|---------|
| RESP-VIEWPORT | `<meta name="viewport" content="width=device-width, initial-scale=1">` present | present | blocker |
| RESP-NOHSCROLL | No unintended horizontal scrolling at 320–1440px | passes | major |
| RESP-FLUID | Layout adapts (flex/grid, fluid units); breakpoints chosen by content, not devices | conforms | major |
| RESP-TOUCH | Hover-only interactions have touch/focus equivalents | present | major |
| RESP-IMG | Responsive images (`srcset`/sizes or fluid `max-width:100%`); no oversized downloads on mobile | conforms | minor |
| RESP-NAV | Navigation works on small screens (accessible menu toggle, not a desktop bar overflowing) | works | major |

## CONTENT — Content & microcopy

| ID | Rule | Threshold | Default |
|----|------|-----------|---------|
| CONTENT-CLARITY | Plain, concise language; jargon defined; scannable (headings, lists, short paras) | conforms | minor |
| CONTENT-CTA | CTAs are specific and action-oriented ("Start free trial", not "Submit"/"Click here") | conforms | minor |
| CONTENT-TITLE | Unique, descriptive `<title>` and meta description per page | present | minor |
| CONTENT-VALUEPROP | Above the fold communicates what this is and why it matters within seconds | present | major |
| CONTENT-LINKTEXT | Link text is descriptive out of context (no bare "here"/"read more" ambiguity) | conforms | minor |
| CONTENT-TONE | Consistent voice/tone and terminology across the site | consistent | polish |

## PERF — Performance (UX-affecting)

| ID | Rule | Threshold | Default |
|----|------|-----------|---------|
| PERF-LCP | Largest Contentful Paint | < 2.5s (good) | major |
| PERF-CLS | Cumulative Layout Shift (set width/height on media, reserve space) | < 0.1 | major |
| PERF-INP | Interaction to Next Paint responsiveness | < 200ms | minor |
| PERF-IMG | Images compressed, modern formats (AVIF/WebP), sized to display, lazy-loaded below the fold | conforms | minor |
| PERF-FONTS | Web fonts subset + `font-display: swap`; limited families/weights; preconnect | conforms | minor |
| PERF-RENDER | No render-blocking that delays first paint; critical CSS prioritized; defer non-critical JS | conforms | minor |
| PERF-ASSETS | No giant unused CSS/JS shipped; assets minified | conforms | polish |

---

## How to apply

1. Measure, don't guess — compute contrast, inspect the DOM, read the CSS.
2. Cite the **ID** in every finding and fix.
3. When fixing a `site`, prefer the most systemic locus (tokens, shared layout,
   global CSS) so one change fixes many instances.
4. If a rule can't be verified with available info, mark it **unverified** — never
   assert PASS without evidence.
