# Usability heuristics & interaction design

Based on Nielsen's 10 heuristics plus interaction fundamentals. Rules: `USAB-*`.

## Nielsen's 10, applied

1. **Visibility of system status** — always show what's happening: loading
   spinners/skeletons, success/error toasts, disabled vs active, hover/active/
   focus states. Never leave the user wondering if a click registered.
2. **Match the real world** — speak the user's language, not system jargon.
   Natural order, familiar metaphors.
3. **User control & freedom** — clear exits, back, undo/redo. Confirm destructive
   actions; let users escape modals/flows easily.
4. **Consistency & standards** — follow platform and web conventions: logo links
   home, underlined links, magnifier = search, primary button placement. Internal
   consistency too: the same thing looks/behaves the same everywhere.
5. **Error prevention** — better than good error messages. Constrain inputs, use
   sensible defaults, disable invalid actions, confirm the irreversible.
6. **Recognition over recall** — keep options and info visible; don't force users
   to remember things across screens. Show, don't make them recall.
7. **Flexibility & efficiency** — accelerators for experts (shortcuts, saved
   state) without burdening novices. Make the common path short.
8. **Aesthetic & minimalist design** — every extra element competes for
   attention. Remove the non-essential; signal-to-noise matters.
9. **Help users recognize, diagnose, recover from errors** — plain-language
   errors that say what went wrong and how to fix it; no error codes alone.
10. **Help & documentation** — when needed, it's searchable, task-focused, and
    close to where it's needed (inline hints, empty-state guidance).

## Interaction states (the checklist of states)

Every interactive element should define: **default · hover · focus · active ·
disabled · loading · error**. Missing states are a top source of "feels broken."

## Empty, loading, and error states

Design the unhappy paths. An empty list should explain what goes there and how to
add the first item. A failed load should offer retry. A good 404 routes back.

## Navigation & orientation

Users should always know **where they are** (active nav state, page title,
breadcrumbs when deep), **where they can go**, and **how to get back**. Don't trap
users; don't hide the primary navigation.

## Forms (where usability lives or dies)

Logical field order, grouped sections, only truly-required fields marked, inline
validation on blur (not just on submit), preserve input on error, clear single
primary action, and tell users what happens after submit.
