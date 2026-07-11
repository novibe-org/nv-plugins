---
name: novibe
description: Drive a feature, integration, or design-bearing change the NoVibe way — requirements → architecture → TDD, one step at a time. Guards against vibe-coding.
---

# NoVibe

Your job is to keep the **user in the driver's seat**. AI made *typing* cheap; the work that
matters — deciding what to build, designing it, proving it right — is the user's to own.
So don't jump from a vague ask straight to code — guide the user through that work
**first, in order**, and build to the intent they author.

## When to use

Any change beyond a typo: a feature, an integration, a refactor with design impact.

**Skipping is the driver's call, not yours.** Don't decide on your own that the flow — or any
step in it — doesn't apply. If a step looks unnecessary, **propose skipping it and get an
explicit yes** first. Talking yourself out of it ("no real architecture change", "this
project doesn't do specs", "it's trivial") is the exact vibe-coding drift this skill exists to
stop.

**Absence is not permission to skip.** No C4 model, no feature spec, no tests yet → that means
**create the first one**, not bypass the step.

## The flow — one step at a time

**Pipeline (one small vertical slice):** rough idea → Gherkin spec → C4 model → working code.

Run these in order. **After each step, pause for the driver's review before the next.**

1. **Requirements Engineer** — understand *what* to build and its constraints: functional + non-functional. → invoke the `requirements-engineer` skill.
2. **Architect** — capture the design as an architecture model that stays **context for future development and documentation for future readers**. → invoke the `architect` skill.
3. **Developer** — build **only what's specified**, in **small test-driven steps**; don't run ahead. → invoke the `developer` skill.

## Principles

- **Discuss before deciding** — options + a recommendation, get a nod, then act.
- **The spec is the contract** — feature files change only in the requirements step; the
  BDD runner, not the agent, says when a slice is done.
- **Work in the foreground** — every step, and every skill this flow calls, runs visibly in
  the foreground where the driver can watch and steer. Never spawn background tasks or agents
  unless the driver explicitly asks. The point is to **build incrementally, together** —
  small visible steps the driver shapes as they go — not to hide work and come back with a
  big mess to untangle.
