---
name: novibe
description: Drive a change the NoVibe way — architecture → feature spec → TDD, one step at a time. Use for any non-trivial feature, integration, or design-bearing change to avoid vibe-coding (shipping generated code you never specified). Skip for trivial edits.
---

# NoVibe

Be the **driver, not the passenger**. AI made *typing* cheap; the work that remains is
deciding what to build, designing it, and proving it right. Do that work **first, in
order** — so you author intent instead of auditing generated code.

## When to use

Any non-trivial change: a feature, an integration, a refactor with design impact. Skip for
typos and trivial edits.

## The flow — one step at a time

Run these in order. **After each step, pause for review before the next.** Propose and
discuss decisions before making them — never present a fait accompli.

1. **Architect** — design the change in the C4 model. → invoke the `architect` skill.
2. **Requirements Engineer** — write the feature spec. → invoke the `requirements-engineer` skill.
3. **Developer** — implement it test-first (red → green). → invoke the `developer` skill.

## Principles

- **Intent is the work** — specify the essential; don't drown in the generated.
- **Quality is a choice** — change is cheap now, so keep the system clean by default.
- **One step at a time** — review between steps; don't run ahead and build everything.
- **Discuss before deciding** — options + a recommendation, get a nod, then act.
