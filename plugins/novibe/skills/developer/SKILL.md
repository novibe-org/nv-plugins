---
name: developer
description: Implement a change test-first — red → green → refactor — driving the feature spec's business scenarios to passing tests. Use when building a feature whose behaviour is specified. On its own, or as the implementation step of the `novibe` flow.
---

# Developer

Prove it right. Write the test **first** so you author the proof of correctness instead of
auditing generated code. The feature spec's scenarios are the acceptance tests; add plain
unit tests for building blocks.

## The loop (any language)

1. **Pick the next behaviour** — the next scenario from the feature spec, or one unit case.
2. **Write the test, run it → RED.** Confirm it fails for the *right* reason (the behaviour
   is missing, not a typo).
3. **Minimal implementation → GREEN.** Write only enough to pass; nothing speculative.
4. **Refactor** with the test green — clean up, remove duplication.
5. Repeat until every scenario passes (or is tagged `@wip`).

Map **business scenarios** (the Gherkin `.feature`) to step defs that drive the *real*
system; keep them in the feature's language of outcomes, not internals.

**Code explains itself.** Prefer clear names and structure over comments. Add documentation
only where the code's *intention* is genuinely hard to grasp — a gotcha, a non-obvious *why*
— never restate what the code already says.

## Tooling by stack

- **Python** — `pytest` + `pytest-bdd`; features in `tests/behavior/features/`, step defs in
  `tests/behavior/`, unit tests in `tests/unit/`. Run `uv run pytest` (lint `uv run ruff
  check`, types `uv run ty check`).
- **TypeScript** — `vitest` + `@amiceli/vitest-cucumber`; same `tests/behavior/` layout. Run
  `pnpm test`. For a Cloudflare Worker, drive it black-box over HTTP via `wrangler`'s dev API
  (feature files load in Node, not inside `workerd`).

## Done when

Every scenario in the spec is green (or explicitly `@wip`), the suite passes, and the
implementation is the minimum that satisfies it — no speculative code.
