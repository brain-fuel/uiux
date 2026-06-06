# Responsive & cross-device design

The same content, usable on a 320px phone and a 1440px+ desktop. Rules: `RESP-*`.

## Foundations

- **Viewport meta** is mandatory: `<meta name="viewport" content="width=device-width, initial-scale=1">`. Without it, mobile rendering is broken.
- **Fluid by default:** use flexbox/grid, percentage/`fr`/`min()`/`max()`/`clamp()`
  and relative units (`rem`). Fixed-px layouts don't adapt.
- **Mobile-first** is a good discipline: start with the small-screen layout and
  enhance upward; it forces prioritization.

## Breakpoints

- Choose breakpoints where **the content breaks**, not by chasing specific device
  widths. Test the continuum, not just 3 magic numbers.
- Common ranges to sanity-check: 320, 375, 768, 1024, 1440px.

## No horizontal scroll

Unintended horizontal scrolling (overflowing elements, fixed widths, oversized
images) is a frequent, easy-to-catch failure. `img, video { max-width: 100% }`,
watch for `width:` in px on containers, and `min-width` on flex children.

## Touch & input

- **Hover is not guaranteed.** Anything revealed on hover (menus, tooltips) needs a
  touch/focus equivalent. Don't hide essential actions behind hover.
- Tap targets and spacing per `A11Y-TARGET`.

## Navigation

Desktop nav bars must become a usable small-screen pattern — an accessible menu
toggle (proper `button`, `aria-expanded`, keyboard-operable), not a horizontal bar
that overflows or wraps awkwardly. Verify the menu opens, traps focus sensibly,
and closes.

## Images & media

Serve appropriately-sized images per viewport (`srcset`/`sizes`, or CSS fluid
sizing) so phones don't download desktop-sized assets. Reserve space (width/height
or aspect-ratio) to avoid layout shift (`PERF-CLS`).

## Verify

Resize from 320→1440 and watch for: horizontal scroll, overlapping/clipped
content, unreadable shrinking text, broken nav, and tap targets that collide.
