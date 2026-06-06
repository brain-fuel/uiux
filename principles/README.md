# UI/UX Principles

The philosophy behind the `/uiux` command. The measurable rules live in
[`checklist.md`](./checklist.md); the topic files go deeper on the *why*:

- [`usability.md`](./usability.md) — Nielsen's heuristics & interaction design
- [`accessibility.md`](./accessibility.md) — WCAG 2.2 AA, in practice
- [`visual.md`](./visual.md) — hierarchy, typography, color, spacing
- [`responsive.md`](./responsive.md) — adaptable, cross-device layouts
- [`content.md`](./content.md) — clarity, microcopy, information architecture
- [`performance.md`](./performance.md) — speed as a UX feature
- [`value.md`](./value.md) — make value visible, reduce cognitive load (Give Good UX)

## North star

**Good UI/UX is invisible.** The interface gets out of the way so the user
accomplishes their goal with minimum friction, confusion, or exclusion. Put
another way (Joe Natoli's *Give Good UX*): **the UI is a means to an end** — every
element either illuminates the path to the user's goal or obstructs it. Every rule
here serves one of four user needs:

1. **Can I perceive it?** (contrast, size, legibility) → accessibility + visual
2. **Can I understand it?** (hierarchy, labels, copy) → visual + content
3. **Can I operate it?** (keyboard, touch, feedback, error recovery) → usability + responsive
4. **Will it respect my time and context?** (speed, device, motion, attention) → performance + responsive

Cutting across all four: **is the value visible, and is the cognitive load as low
as it can be?** → `GGUX-*` ([`value.md`](./value.md)).

## How to weigh tradeoffs

- **Accessibility is not optional.** A `blocker` a11y failure (no keyboard access,
  failing contrast, unlabeled form) outranks any aesthetic preference. Fix it.
- **Consistency beats local cleverness.** A slightly worse-but-consistent pattern
  usually beats a novel one. Match existing conventions unless they're broken.
- **Systemic over cosmetic.** Fix the design token / shared component, not 40 copies.
- **Don't redesign on a `fix`.** Improve within the existing visual language unless
  the user explicitly asks for a redesign. Preserve brand and intent.
- **Evidence over taste.** Findings cite measurements and a checklist ID. "I don't
  like it" is not a finding; "body text is 3.1:1, fails A11Y-CONTRAST" is.

## Form follows function (the older lineage)

Make the structure legible; let function dictate form; measure before you theorize.
Five centuries before "form follows function" was a slogan, Leonardo derived it from
nature — every form exists to serve a function, and anything that serves none comes
out ("nothing lacking, nothing superfluous"). That is exactly `GGUX-EARN-PLACE`: the
UI is a means to an end, so each element either advances the task or is removed. His
method was *experience before reasoning* — run the experiment, measure, then reason
from what you measured — which is precisely how this auditor works: compute the
contrast, inspect the DOM, read the CSS, never assert PASS from taste. And his maps,
exploded views, and elevation drawings make the point that **representation matters**
(`GGUX-OVERVIEW`, `GGUX-CHART`, `CONTENT-FIGCAPTION`): the value of a complex system
lives in how understandably you present it. Good information design is not
decoration; it is the function.

## Lineage / sources

The rules here distill several bodies of work into one auditable checklist:

- **Nielsen's heuristics** + **WCAG 2.2 AA** — the `USAB-*` and `A11Y-*` baseline.
- **Refactoring UI** (Schoger & Wathan) — much of `VIS-*`, incl. borders, width,
  de-emphasis, personality, tracking, defaults, depth.
- **Give Good UX** (Joe Natoli) — `GGUX-*`: value made visible, cognitive load,
  progressive disclosure, icons & labels, the mobile mistakes (see [`value.md`](./value.md)).
- **Make It Clear** (Patrick Winston) — `CONTENT-POINTFIRST`, `CONTENT-SIGNPOST`,
  `CONTENT-FIGCAPTION`: lead with the point, signposting, standalone figures.
- **Leonardo da Vinci's design method** — the "form follows function" lineage above.

## Severity, briefly

`blocker` → some users literally cannot complete a core task. `major` → real
friction or exclusion for many. `minor` → noticeable rough edge. `polish` →
refinement. Always fix blockers; batch the rest by leverage.
