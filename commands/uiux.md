---
description: Audit, fix, or scaffold web UI/UX against built-in principles. Point at a URL or a repo.
argument-hint: <new|audit|fix> <page|site> <url | path | repo>
allowed-tools: Read, Write, Edit, MultiEdit, Bash, Glob, Grep, WebFetch, WebSearch, Agent, TodoWrite
---

# /uiux — principled UI/UX for the web

You are operating the **uiux** command. The user invoked:

```
/uiux $ARGUMENTS
```

Parse `$ARGUMENTS` as: `<action> <scope> <target...>`

- **action** — `new` | `audit` | `fix`
- **scope** — `page` | `site`
- **target** — a URL (`https://…`), a local path, or a Git repo (`owner/name`, an
  SSH/HTTPS git URL, or a local checkout). May be empty for `new` (you'll gather
  requirements) or default to the current working directory for repo actions.

If `action` or `scope` is missing or unrecognized, briefly show the six valid
forms and ask the user which they meant. Do not guess destructively.

## Step 0 — Load the principles (always, first)

Before doing anything else, read the principles library bundled with this plugin:

```
${CLAUDE_PLUGIN_ROOT}/principles/checklist.md      ← the operational, measurable rules
${CLAUDE_PLUGIN_ROOT}/principles/README.md         ← philosophy + how to weigh tradeoffs
```

Then read the topic files relevant to the findings as you go:
`usability.md`, `accessibility.md`, `visual.md`, `responsive.md`, `content.md`,
`performance.md`, `value.md` (all under `${CLAUDE_PLUGIN_ROOT}/principles/`).

Every finding, fix, and design decision MUST cite a principle ID from
`checklist.md` (e.g. `A11Y-CONTRAST`, `VIS-HIERARCHY`, `GGUX-VALUE-VISIBLE`). No
citation → not a finding. This keeps the tool objective and reviewable.

Treat `value.md` (Give Good UX) as the lens over everything else: the UI is a
means to an end, so beyond per-rule PASS/FAIL, ask whether the value is visible
and the cognitive load is as low as it can be.

## Step 1 — Resolve the target

- **URL** (`http://` / `https://`): a *live* target.
  - Fetch the rendered HTML/CSS with `WebFetch`. For `site` scope, also discover
    routes (sitemap.xml, robots.txt, in-page nav links) and sample the key
    templates/pages (home, a content page, a form, an error page) — cap at a
    sensible number and **state which pages you covered and which you skipped**.
  - You cannot edit a live URL. For `fix` on a URL, see Step 3's note.
- **Local path / repo**: a *source* target.
  - If it's `owner/name` or a git URL not already local, `git clone` it into a
    temp dir (ask first if it will write outside the cwd).
  - Detect the stack: look for `hugo.toml`/`config.toml` (Hugo), `next.config.*`
    (Next.js), `package.json` deps (React/Vue/Svelte/Astro/Tailwind), plain
    `*.html`, etc. Adapt edits to the detected framework and its conventions.
  - Identify the UI surface: templates/layouts, components, global CSS/design
    tokens, content. For `site` scope, treat shared layout/partials/tokens as
    high-leverage (one fix propagates).

## Step 2 — Run the audit (all actions begin here)

Evaluate the target against `checklist.md`. Produce findings, each with:

| field | meaning |
|-------|---------|
| **id** | principle ID from the checklist |
| **severity** | `blocker` (unusable/inaccessible) · `major` · `minor` · `polish` |
| **where** | URL + selector, or `file:line` |
| **observed** | what's wrong, concretely (include measured values: contrast ratio, px, etc.) |
| **expected** | the principle's threshold |
| **fix** | the specific change |

Be measurable. Examples: compute text/background **contrast ratios** and compare
to 4.5:1 (normal) / 3:1 (large); check tap-target sizes vs 24×24 (WCAG 2.2) /
44×44 (comfortable); check for one `<h1>`, logical heading order, `alt` on
images, labels on inputs, visible focus styles, reduced-motion handling,
viewport meta, etc.

Write the report to `UIUX-AUDIT.md` at the target root (for URLs, the cwd),
grouped by severity then area, with a short summary table at the top
(counts per severity) and a "coverage" note (what was and wasn't inspected).

## Step 3 — Act on the action

### `audit page` / `audit site`
Stop after Step 2. Present the summary inline and point to `UIUX-AUDIT.md`.
**Make no changes.** Offer to run the matching `fix` next.

### `fix page` / `fix site`
1. Do Step 2.
2. Use `TodoWrite` to track findings as a worklist.
3. Apply fixes in severity order (blocker → polish). Prefer **systemic** fixes
   (design tokens, shared layout/component, global CSS) over per-instance patches
   when scope is `site`.
4. Preserve the existing design language and stack conventions — improve, don't
   re-skin, unless the user asked for a redesign.
5. After edits, **verify**: run the project's build/lint/format if present; for a
   detectable dev server, sanity-check the changed pages. Re-measure anything you
   claimed to fix (e.g. recompute contrast).
6. Summarize: what changed, per finding, with `file:line`; what you deliberately
   left (and why); anything needing human judgment. Do not commit or push unless
   asked.
7. **URL-only fix** (a live URL, no repo given): you can't edit it. Locate the
   source repo (ask the user) and operate there; if unavailable, emit a concrete
   patch/diff and the exact changes so they can apply them. Say so plainly.

### `new page` / `new site`
1. If requirements are thin, ask 2–4 sharp questions: purpose/goal, audience,
   brand/visual direction (or an existing site to match), key content/sections,
   and the target stack (default to the repo's stack, or ask if greenfield).
2. Scaffold against the principles **by construction**: semantic landmarks, one
   `<h1>`, labeled accessible forms, visible focus, responsive/fluid layout,
   adequate contrast from the chosen palette, sensible type scale and spacing
   rhythm, reduced-motion support, performance-conscious assets, and clear
   primary actions.
3. `page`: add one well-structured page into the existing project. `site`: lay
   down a coherent multi-page baseline (nav, footer, home + representative pages,
   shared layout + design tokens, 404).
4. Then run an `audit` pass over what you generated and fix anything that slipped
   — hand over something that already passes its own checklist.

## Operating notes

- Scale effort to scope: `page` is focused; `site` warrants breadth — for large
  sites, consider spawning parallel `Agent` audits per section/route and merging.
- Honor existing conventions, tokens, and naming. Match the surrounding code.
- Confirm before anything hard to reverse (cloning outside cwd, mass rewrites,
  deleting files, network writes).
- Never fabricate measurements. If you couldn't measure something (e.g. no
  rendered CSS for a URL), say so and mark it "unverified," don't assert a PASS.
- Keep `UIUX-AUDIT.md` as the durable artifact so audits are diffable over time.
