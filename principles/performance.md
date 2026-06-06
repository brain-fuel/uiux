# Performance (speed is a UX feature)

Slow is a usability failure: users abandon, perceive low quality, and (on mobile/
slow networks) get excluded. Rules: `PERF-*`.

## Core Web Vitals (the user-centric targets)

- **LCP — Largest Contentful Paint < 2.5s.** How fast the main content appears.
  Usually gated by the hero image/font/render-blocking resources.
- **CLS — Cumulative Layout Shift < 0.1.** Visual stability. Reserve space for
  images/ads/embeds (set `width`/`height` or `aspect-ratio`); don't inject content
  above existing content; preload fonts to avoid swap-driven shifts.
- **INP — Interaction to Next Paint < 200ms.** Responsiveness to taps/clicks/keys.
  Keep the main thread free; break up long JS tasks.

## Images (usually the biggest win)

- Compress; use **modern formats** (AVIF/WebP) with fallbacks.
- Size to display dimensions; serve responsive `srcset`/`sizes`.
- **Lazy-load** below-the-fold images; eager-load the LCP image.
- Always set dimensions / aspect-ratio to prevent shift.

## Fonts

- Subset to needed glyphs; limit families and weights.
- `font-display: swap` (or `optional`) so text isn't invisible while loading.
- `preconnect`/`preload` key fonts; prefer system fonts when appropriate.

## Render path

- Eliminate/minimize render-blocking CSS and JS; inline critical CSS, defer the
  rest; `defer`/`async` non-critical scripts.
- Ship less: remove unused CSS/JS, minify, tree-shake, split bundles.
- Cache static assets aggressively; use a CDN.

## Perceived performance

Even when work is unavoidable, *feel* fast: skeleton screens, optimistic UI,
instant feedback on interaction, and progressive rendering. Perceived speed often
matters more than raw numbers.

## How to measure

Prefer real tooling (Lighthouse, WebPageTest, CrUX field data) when available; for
a static read, flag obvious offenders: huge unoptimized images, many
render-blocking resources, missing dimensions, heavy third-party scripts, no
caching/minification.
