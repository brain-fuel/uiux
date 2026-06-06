# Visual design & hierarchy

How the eye is guided. Rules: `VIS-*`.

## Hierarchy

- **One focal point per view.** Decide what the user should see first, then make
  it dominant (size, weight, color, space, position). Everything else is secondary.
- **The primary action is visually distinct** from secondary/tertiary actions
  (solid vs outline vs text button). Don't show five equal-weight buttons.
- Establish hierarchy with **size, weight, color, contrast, and spacing** — in
  that rough order of strength.

## Typography

- **Type scale:** a small, consistent set of steps (≈5–7), e.g. a modular scale.
  Don't use a dozen arbitrary sizes.
- **Body ≥ 16px**, line-height 1.4–1.7. Headings can be tighter (1.1–1.3).
- **Measure (line length):** 45–85 characters for body text; cap container width.
- **Limit families** (1–2) and weights. Pair a display/heading face with a
  readable body face, or use one well-chosen family.
- Align to a baseline rhythm; avoid justified text on the web (rivers, bad wraps).
- **Letter-spacing by size & case (`VIS-TRACKING`):** tighten large headings
  (slight negative tracking, or a tighter display face); add tracking to all-caps
  and small-caps runs so they don't crowd. Leave body at default.
- **De-emphasize with contrast and weight, not size (`VIS-DEEMPHASIS`):** make
  secondary text (labels, metadata) recede by lowering contrast or dropping weight
  rather than shrinking it into illegibility. Build emphasis with color + weight —
  pushing hierarchy on size alone yields oversized primaries and tiny secondaries.

## Color

- **Restrained palette with roles:** brand, accent (use sparingly for emphasis/
  CTAs), neutrals (most of the UI), and semantic (success/warning/error/info).
- **60-30-10** as a rough split: dominant neutral, secondary, accent.
- Define the palette as **tokens** and use them consistently. Accent loses meaning
  if everything is accent-colored.
- Always check color choices against `A11Y-CONTRAST`.

## Spacing & layout

- **Spacing scale** (e.g. 4/8px multiples). Consistent gaps read as intentional.
- **Proximity:** group related items, separate unrelated ones — spacing is the
  cheapest, strongest grouping cue.
- **Alignment:** everything aligns to a grid/edge. Misalignment reads as sloppy.
- **Whitespace is not wasted space** — it creates focus and grouping. Avoid
  cramped, wall-to-wall density and walls of text.
- **Space, background, shadow before borders (`VIS-BORDERS`):** borders multiply
  fast and box everything into a grid of cages. Group with proximity or a shared
  background instead; use at most one border treatment per region.
- **Don't fill the whole screen (`VIS-WIDTH`):** give sidebars, forms, and cards a
  fixed, content-appropriate width and keep margins at the page edges. Nothing has
  to be full-bleed just because the nav bar is; full-bleed should be deliberate.

## Grouping (Gestalt) — `GGUX-GROUPING`

The eye perceives relationships *before* it reads. Natoli's *Value Made Visible*
leans on the Gestalt laws to make structure obvious without borders or labels:

- **Proximity** — near = related. The default, strongest grouping tool.
- **Similarity** — shared color/shape/size reads as the same kind of thing
  (all destructive actions red, all links one style).
- **Enclosure / common region** — a shared background, card, or border binds items
  into one group; use it *instead of* heavy borders, not on top of them.
- **Continuation** — the eye follows lines and alignment; arrange items so the
  gaze flows along the intended path.
- **Closure** — the mind completes implied shapes, so partial cues can suggest
  grouping without drawing every box.
- **Figure-ground** — keep foreground (content/actions) clearly separated from
  background; ambiguous figure-ground is what makes a UI feel noisy.

Reach for space and grouping before you reach for lines — see clutter
(`GGUX-EARN-PLACE`).

## Imagery & icons

- Correct resolution and **aspect ratio** (never stretch/squash); use the right
  asset for the slot (don't shrink a huge stacked logo into a tiny square).
- Consistent icon style (stroke vs fill, weight, size) and consistent image
  treatment (corners, shadows, ratios).

## Consistency

Repeated components — buttons, cards, inputs, badges — should be visually and
behaviorally identical. Inconsistency taxes the user and signals low quality.
A component/token system enforces this by construction.

## Personality & depth

From *Refactoring UI*:

- **Pick one personality and commit (`VIS-PERSONALITY`).** Font character,
  border-radius, color temperature, and copy tone should pull the same direction
  (elegant / playful / neutral). A sharp formal serif beside fat rounded buttons
  reads as accidental.
- **Supercharge the defaults (`VIS-DEFAULTS`).** Restyle the raw browser elements
  that show up in real content — list markers, blockquotes, links, form controls.
  Defaults signal "unfinished."
- **Build depth deliberately (`VIS-DEPTH`).** Draw shadows from a defined scale
  (small = buttons, medium = dropdowns, large = modals). For richer elevation,
  layer two shadows (a tight dark one + a larger diffuse one) or reach for accent
  borders and overlapping elements rather than one flat ad-hoc drop shadow.

## Keep prose rules out of layout — `VIS-PROSE-SCOPE`

Prose typography (paragraph rhythm, list-item margins, line spacing) belongs to
**content containers**, not to global element selectors. A global rule like
`li + li { margin-block-start: 0.35em }` leaks into every layout list — nav menus,
card grids, breadcrumbs, tag lists — pushing every item but the first out of line.
(Real bug: a horizontal nav where every item except "Worship" sat 0.35em low.)

Detection:

- Grep the CSS for global `li`, `li + li`, `p + p`, or bare `ul/ol` margin rules
  not scoped under a content class.
- Inspect the computed `margin-block-start` on a nav/card `<li>`. Any nonzero value
  inherited from a prose rule = fail.

Fix — scope the prose rules, or reset on layout lists:

```css
/* scope */
.prose li + li { margin-block-start: 0.35em }
/* or reset where layout lists live */
.site-nav li + li, .cards li + li { margin-block-start: 0 }
```

## Separating a sticky header from content

Don't fence a fixed header off with a heavy brand-color border — it reads as a
stray page element, especially on mobile. Instead:

- A **hairline** divider at rest, plus a **soft shadow that appears only once
  content scrolls beneath** (elevation-on-scroll; toggle an `is-elevated` class).
- Express brand color as a **thin accent strip at the very top edge** of the page,
  not as a thick rule under the header.

See `STICKY-*` in [`responsive.md`](./responsive.md) for the behavior rules.
