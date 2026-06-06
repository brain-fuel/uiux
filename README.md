# uiux — principled UI/UX for Claude Code

A Claude Code plugin that **audits, fixes, and scaffolds web UI/UX** against a
bundled library of usability, accessibility, visual-design, responsive, content,
and performance principles. Point it at a **URL** or a **repository** and it works
the whole thing over — every finding and fix cites a specific principle.

## The commands

One command, `/uiux`, with `<action> <scope> <target>`:

| Command | What it does |
|---------|--------------|
| `/uiux new page <path?>` | Scaffold a new, principle-compliant page into a project |
| `/uiux new site <path?>` | Scaffold a coherent multi-page site baseline |
| `/uiux audit page <url\|path>` | Report a single page's issues against the principles (no changes) |
| `/uiux audit site <url\|repo>` | Report across a whole site/repo (no changes) |
| `/uiux fix page <url\|path>` | Audit, then apply fixes to a page |
| `/uiux fix site <url\|repo>` | Audit, then apply fixes across the site (systemic fixes preferred) |

- **Target** can be a live `https://` URL (audited as rendered), a local path, or
  a Git repo (`owner/name` or a git URL — cloned if needed).
- **audit** never edits; it writes `UIUX-AUDIT.md`. **fix** audits first, then
  edits, then verifies. **new** scaffolds against the principles, then self-audits.
- You can't edit a live URL — for `fix` on a URL, point it at the source repo (or
  it'll emit a patch you can apply).

## Install

```text
/plugin marketplace add brain-fuel/uiux
/plugin install uiux@uiux
```

Then restart/reload and run, e.g.:

```text
/uiux audit site https://example.com
/uiux fix site ./my-hugo-site
/uiux new page
```

(Or clone this repo and load it as a local plugin during development.)

## How it works

1. On every run it loads [`principles/checklist.md`](principles/checklist.md) — the
   measurable rules, each with a stable **ID**, a **threshold**, and a **severity**.
2. It resolves the target (fetch a URL's rendered HTML/CSS, or detect the repo's
   stack and read its templates/components/tokens).
3. It audits against the checklist, producing findings with measured values
   (contrast ratios, px sizes, …) and a principle ID each.
4. For `fix`, it applies changes in severity order — preferring systemic fixes
   (design tokens, shared layouts) on `site` scope — then verifies (build/lint,
   re-measure) and summarizes the diff.

Nothing is fabricated: if a rule can't be measured with the available info, it's
marked **unverified**, not passed.

## The principles

| File | Area |
|------|------|
| [`checklist.md`](principles/checklist.md) | The operational, measurable rules (source of truth) |
| [`accessibility.md`](principles/accessibility.md) | WCAG 2.2 AA in practice |
| [`usability.md`](principles/usability.md) | Nielsen's heuristics & interaction |
| [`visual.md`](principles/visual.md) | Hierarchy, type, color, spacing |
| [`responsive.md`](principles/responsive.md) | Cross-device layouts |
| [`content.md`](principles/content.md) | Clarity, microcopy, IA |
| [`performance.md`](principles/performance.md) | Core Web Vitals & speed |
| [`value.md`](principles/value.md) | Make value visible, reduce cognitive load (Joe Natoli's *Give Good UX*) |

Principles are plain Markdown — fork and tune them to your house style; the command
reads whatever is in `principles/`.

## Layout

```text
.claude-plugin/
  plugin.json         plugin manifest
  marketplace.json    lets the repo be added as a marketplace
commands/
  uiux.md             the /uiux command (dispatch + playbook)
principles/           the principles library the command loads at runtime
```

## License

MIT — see [LICENSE](LICENSE).
