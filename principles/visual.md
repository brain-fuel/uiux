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

## Imagery & icons

- Correct resolution and **aspect ratio** (never stretch/squash); use the right
  asset for the slot (don't shrink a huge stacked logo into a tiny square).
- Consistent icon style (stroke vs fill, weight, size) and consistent image
  treatment (corners, shadows, ratios).

## Consistency

Repeated components — buttons, cards, inputs, badges — should be visually and
behaviorally identical. Inconsistency taxes the user and signals low quality.
A component/token system enforces this by construction.
