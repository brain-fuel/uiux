# UI/UX Principles

The philosophy behind the `/uiux` command. The measurable rules live in
[`checklist.md`](./checklist.md); the topic files go deeper on the *why*:

- [`usability.md`](./usability.md) — Nielsen's heuristics & interaction design
- [`accessibility.md`](./accessibility.md) — WCAG 2.2 AA, in practice
- [`visual.md`](./visual.md) — hierarchy, typography, color, spacing
- [`responsive.md`](./responsive.md) — adaptable, cross-device layouts
- [`content.md`](./content.md) — clarity, microcopy, information architecture
- [`performance.md`](./performance.md) — speed as a UX feature

## North star

**Good UI/UX is invisible.** The interface gets out of the way so the user
accomplishes their goal with minimum friction, confusion, or exclusion. Every
rule here serves one of four user needs:

1. **Can I perceive it?** (contrast, size, legibility) → accessibility + visual
2. **Can I understand it?** (hierarchy, labels, copy) → visual + content
3. **Can I operate it?** (keyboard, touch, feedback, error recovery) → usability + responsive
4. **Will it respect my time and context?** (speed, device, motion, attention) → performance + responsive

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

## Severity, briefly

`blocker` → some users literally cannot complete a core task. `major` → real
friction or exclusion for many. `minor` → noticeable rough edge. `polish` →
refinement. Always fix blockers; batch the rest by leverage.
