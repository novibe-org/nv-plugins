---
name: novibe
description: Drive a feature, integration, or design-bearing change the NoVibe way — requirements → architecture → TDD, one step at a time. Guards against vibe-coding.
---

# NoVibe

This is **spec-driven development**. AI made *typing* cheap; the work that matters — deciding
what to build, designing it, proving it right — is the user's to own, and that ownership lives
in the **specification phase**: co-create the feature spec first, then the architecture, in that
order, with the driver deciding at every turn. So don't jump from a vague ask straight to code —
guide the user through that work **first, in order**, and build to the intent they author.

Once the spec and the architecture are settled, they are the contract. The **developer** step
executes that contract — and because the hard decisions were already made in the specification
phase, this is the one step that can run **autonomously** (including in the background / auto
mode) without becoming vibe-coding. Autonomy in execution is fine; autonomy in *deciding* is not.

In Claude Code, run the developer step as a background **Agent** (optionally `isolation:
worktree`) rather than inline: it can TDD the slice, open the PR, and wait out asynchronous
bot/CI/Sonar feedback without occupying the driver's session. But the **driver is a reviewer
too** — their own comment on the PR is a decision, not a bot finding, and decisions don't
belong to the developer step. When that happens, the agent stops and reports back rather than
resolving it on its own; the driver picks it up from the orchestrating session, the same seat
they never left during requirements and architecture.

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

Run these in order. **During specification (steps 1–2), pause for the driver's review after
each step** — this is where they decide. Step 3 executes what was decided.

1. **Requirements Engineer** — understand *what* to build and its constraints: functional + non-functional. → invoke the `requirements-engineer` skill.
2. **Architect** — capture the design as an architecture model that stays **context for future development and documentation for future readers**. → invoke the `architect` skill.
3. **Developer** — build **only what's specified**, in **small test-driven steps**, against the approved spec and model; don't run ahead of them. → invoke the `developer` skill.

## Principles

- **Discuss before deciding** — during requirements and architecture, options + a
  recommendation, get a nod, then act. This is where the driver's decisions live.
- **The spec is the contract** — feature files change only in the requirements step; the
  BDD runner, not the agent, says when a slice is done.
- **Specification runs in the foreground; execution does not have to.** Requirements and
  Architecture always run visibly, where the driver can watch and steer at every turn — never
  spawn background tasks or agents for these two steps unless the driver explicitly asks. The
  point there is to **build the spec incrementally, together** — small visible steps the driver
  shapes as they go — not to hide work and come back with a big mess to untangle. The Developer
  step is different: once the spec is approved, it may run autonomously, including in the
  background or auto mode — it has nothing left to decide, only to build correctly.
