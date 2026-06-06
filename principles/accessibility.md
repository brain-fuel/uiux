# Accessibility (WCAG 2.2 AA, in practice)

Accessibility is the floor, not a feature. ~1 in 5 people have a disability, and
accessible design helps everyone (keyboard users, bright sunlight, slow networks,
temporary injuries). Rules: see `A11Y-*` in [`checklist.md`](./checklist.md).

## Perceivable

- **Contrast** — body text ≥ 4.5:1, large text (≥24px, or ≥18.66px bold) ≥ 3:1,
  and UI components/icons/focus rings ≥ 3:1 against adjacent colors. Measure it;
  don't eyeball. Light-text-on-light or dark-on-dark is the most common real bug.
- **Text, not images of text.** Real text scales, translates, and is selectable.
- **Don't rely on color alone.** Links need a non-color cue (underline). Error /
  success states need text or an icon, not just red/green.
- **Images:** informative → concise `alt` describing purpose; decorative → `alt=""`
  (or `aria-hidden`). Don't start with "image of".

## Operable

- **Keyboard:** everything usable without a mouse. Logical tab order (matches
  visual order, no positive `tabindex`). A **visible focus indicator** always —
  removing `outline` without a replacement is a blocker.
- **Tap targets:** ≥ 24×24px (WCAG 2.2 minimum); 44×44 is comfortable for primary
  touch actions. Space them so neighbors aren't mis-tapped.
- **Motion:** respect `prefers-reduced-motion`; never convey essential info by
  motion alone; avoid content that flashes > 3×/sec.
- **Skip link** to `main` for keyboard users on long nav.

## Understandable

- **Labels:** every input has a programmatic label. Placeholder text is NOT a
  label. Group related fields (`fieldset`/`legend`).
- **Errors:** identify the field, describe the problem and the fix, and announce
  it (e.g. `aria-describedby`, `role="alert"`). Don't clear the user's input.
- **Predictable:** consistent navigation and component behavior across pages.
- **`<html lang>`** set so screen readers pronounce correctly.

## Robust

- **Semantic HTML first:** real `<button>`, `<a>`, `<nav>`, `<main>`, `<h1–h6>`,
  lists, tables with headers. ARIA is a patch for when semantics fall short — and
  bad ARIA is worse than none. Landmarks: one `<main>`, plus `header`/`nav`/`footer`.
- **Name, role, value:** custom widgets must expose all three to assistive tech.
- **Reflow:** usable at 200% zoom and 320px width without loss of content or
  horizontal scrolling of text.

## Quick audit moves

Tab through the whole page; navigate by headings; check contrast on every
text/background pair and on focus rings; zoom to 200%; toggle reduced-motion;
inspect forms for labels and error handling.
