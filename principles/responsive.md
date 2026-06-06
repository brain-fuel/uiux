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

## Nav reachability & the sticky-header tax — `USAB-NAV-REACH`, `STICKY-*`

On pages taller than ~2 viewports, a **static** top header forces a scroll-to-top
just to navigate. Make primary nav reachable mid-page (`USAB-NAV-REACH`). Two
patterns:

- **Always-sticky** — simple, but a permanently fixed bar eats ~12% of a phone
  viewport. Costly on mobile.
- **Reveal-on-scroll-up ("headroom")** — hide the header while scrolling down,
  bring it back on any upward scroll. Preferred on mobile; reclaims the space.

A fixed/sticky header brings a tax — audit each `STICKY-*` rule whenever one exists:

- **`STICKY-ANCHORS`** — set `scroll-padding-top` (or `scroll-margin-top` on anchor
  targets) equal to the header height, so `#anchor` jumps and focus don't land
  under the bar.
- **`STICKY-NOHIDE`** — an auto-hiding header must NOT hide while its menu is open
  or while keyboard focus is inside it; gate the hide on `!menuOpen &&
  !header.contains(document.activeElement)` and handle `focusin`.
- **`STICKY-MENUFIT`** — cap the open mobile menu to the viewport
  (`max-height: calc(100dvh - var(--header-h))` + `overflow:auto`) so every item is
  reachable on short/landscape screens.
- **`STICKY-MOTION`** — respect `prefers-reduced-motion`: show/hide instantly, no
  slide.

### Reference implementation (shipped, works)

Sticky header + `transform: translateY(-100%)` toggle; rAF-throttled **passive**
scroll listener; add `is-elevated` once `scrollY > 4`; hide only when
`y > lastY && y > 160 && !menuOpen && !header.contains(document.activeElement)`.
Source: `hopelutheransunbury.org` — `layouts/partials/header.html` +
`assets/css/main.css` (commit `184adb8`).

## Images & media

Serve appropriately-sized images per viewport (`srcset`/`sizes`, or CSS fluid
sizing) so phones don't download desktop-sized assets. Reserve space (width/height
or aspect-ratio) to avoid layout shift (`PERF-CLS`).

## Verify

Resize from 320→1440 and watch for: horizontal scroll, overlapping/clipped
content, unreadable shrinking text, broken nav, and tap targets that collide.
