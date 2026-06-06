# Give Good UX — value & cognitive clarity

Joe Natoli's *Give Good UX* principles, adapted into auditable rules. Rules:
`GGUX-*`. The measurable thresholds live in [`checklist.md`](./checklist.md); this
file is the *why*.

## North star: the UI is a means to an end

Everything a user sees onscreen does one of two things: it **illuminates the path**
to their goal, or it **obstructs** it. The destination matters more than the
journey, so the designer's job is to light the path and remove everything in the
way. This is the same instinct as *aesthetic & minimalist design*
(`USAB-EFFICIENCY`) and the sibling `good-ui` summary's *design by elimination* —
a different vocabulary for the same discipline.

## Make value visible — `GGUX-VALUE-VISIBLE`, `GGUX-GIVE-FIRST`

Users decide in seconds whether something is worth their effort. So **expose the
value**, don't bury it:

- Show the benefit up front, then keep it visible through the flow.
- In any multi-step process, **signal progress** ("Step 2 of 4") and show what's
  been gained so far — never leave the user guessing how far they've come.
- **Give before you ask.** Don't gate core value behind a signup, paywall, or
  long form *before* the user has experienced anything. Prioritize adoption over
  registration; "asking to receive without giving" is one of the surest ways to
  lose a first-time user.

## Reduce cognitive load — `GGUX-CHOICES`, `GGUX-DISCLOSURE`, `GGUX-EARN-PLACE`

Every element, option, and word costs the user attention. Spend it deliberately:

- **Limit choices (Hick's Law).** The more competing options at a decision point,
  the longer and harder the decision. Surface the few that matter; defer or
  subordinate the rest.
- **Progressive disclosure.** Show only what's needed *now*. Advanced, rare, or
  future options are revealed on demand, not dumped on the first screen.
- **Every element earns its place (clutter).** If something doesn't advance the
  task, it's noise — remove it. Reach for whitespace and Gestalt grouping before
  borders and dividers.

### Progressive-disclosure decision flow

For any element, ask in order — show it now only if the path leads to "show":

```
Do I need this right now?
├─ YES → does it explain/clarify the action I must take right now?
│        ├─ YES → SHOW IT NOW
│        └─ NO  → does it help me understand content I just saw / an action I took?
│                 ├─ YES → SHOW IT NOW
│                 └─ NO  → DEFER (progressive disclosure)
└─ NO  → will I need it to understand or act in the FUTURE?
         ├─ YES → DEFER until that moment
         └─ NO  → CUT IT
```

## Orient before detail — `GGUX-OVERVIEW`

The inverse of progressive disclosure: where complexity is unavoidable (dashboards,
long-form content, multi-section pages), give the user a bird's-eye view *before*
the detail — at-a-glance summary metrics, a table of contents, or a section map
with reading progress. "Overview first, zoom and filter, then details on demand"
(Shneiderman). Orientation to the whole is what lets people drill in without getting
lost. This echoes da Vinci's bird's-eye maps and exploded views — see the lineage
note in [`README.md`](./README.md).

## The timeless principles (Value Made Visible)

These predate the term "UX." Trends churn; fundamentals don't. They're applied
across this library rather than re-listed here:

- **Affordance** — an element's appearance suggests its use (`USAB-AFFORD`).
- **Gestalt grouping** — proximity, similarity, enclosure/common region,
  continuation, closure, figure-ground (`GGUX-GROUPING`, see [`visual.md`](./visual.md)).
- **Consistency** — same thing, same look and behavior (`VIS-CONSISTENCY`,
  `USAB-CONSISTENCY`).
- **Fitts' Law** — time to a target depends on its size and distance; make
  frequent/important targets bigger and closer (`A11Y-TARGET`).
- **Hick's Law** — decision time grows with the number of choices (`GGUX-CHOICES`).
- **Occam's Razor** — the simplest solution that works is the best; don't add what
  you don't need (`GGUX-EARN-PLACE`).
- **Progressive disclosure** — reveal complexity only as needed (`GGUX-DISCLOSURE`).

## Icons & labels — `GGUX-ICONLABEL`

An icon only communicates if the user already recognizes it. Use **icon-only**
controls only when all of these hold; otherwise pair the icon with a text label,
or use a label alone:

```
Is space limited?
├─ NO  → will users understand a text label without an icon? → LABEL ONLY
└─ YES → is the icon an established convention / easily recognizable?
         ├─ NO  → ICON + LABEL
         └─ YES → is it a literal representation of a real-world object?
                  ├─ NO  → ICON + LABEL
                  └─ YES → is it large enough (≈24×24px, 48×48 touch target)?
                           ├─ NO  → ICON + LABEL
                           └─ YES → ICON ONLY is OK
```

This complements `A11Y-NAME`: even a "safe" icon-only control still needs a
programmatic accessible name (`aria-label`/sr-only text) for non-visual users.

## Designed for context — `GGUX-CONTEXT`

Especially on mobile (*Give Good Mobile*): people use interfaces distracted,
interrupted, one-handed, in bright light, on slow connections. Don't make them
work (cognitive load), don't annoy them (friction/focus), and don't leave them
hanging (feedback — `USAB-FEEDBACK`). The core task must be reachable without
unnecessary steps, and the UI must stay glanceable.

## Show data in the right form — `GGUX-CHART`

A chart should answer the question its reader is asking. Match the format to the
question, and don't distort:

| The question | Use |
|---|---|
| Compare values across categories | Bar chart |
| Trend over time | Line chart |
| Part-to-whole | Stacked bar; pie **only** for a few large slices |
| Relationship / correlation between two measures | Scatter plot |
| Distribution of a single measure | Histogram |
| Two-to-four dimensions at once | Bubble chart |

Avoid misleading scales (truncated/zoomed axes), 3-D effects, and "chart junk" —
decoration that obscures the data.

## The 14 mobile mistakes (what `GGUX-*` guards against)

*UX FAIL* catalogues the recurring ways mobile UI fails its users; most map onto
the rules above. In brief: ignoring context of use; not designing for the user's
focus; speaking the system's language instead of the user's; hiding state changes;
poor error messaging; ignoring learned behaviors; placing obstacles in front of
value; failing to expose value or signal progress; unnecessary steps; prioritizing
registration over adoption; asking to receive without giving; sloppy first
impressions; insufficient testing; and serving the business's priorities over the
user's. When you find one, cite the matching `GGUX-*` (or `USAB-*`/`CONTENT-*`) ID.
