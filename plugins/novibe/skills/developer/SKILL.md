---
name: developer
description: Implement a change test-first — red → green → refactor — turning the spec's scenarios into passing tests. Use when building a feature whose behaviour is specified.
---

# Developer

**In:** the Gherkin spec (`docs/requirements/<epic>/<feature>.feature`) + the C4 model (`docs/architecture/current/`).
**Out:** **working code** for the feature slice.

**Prove it right** — the spec itself executes, so the proof of correctness is the runner's
report, not the agent's claim.

**The spec runs through the project's BDD runner** (cucumber-jvm, pytest-bdd, cucumber-js, …
per stack) — the `.feature` file is what executes. Tests merely *inspired by* the spec don't
count. No runner in the project yet? Setting it up is the first task of the first slice.

**Bind to the real system** — scenarios drive the actual built artifact over its real interface
(boot it and call it: HTTP, CLI, library entry), never a stub or a reimplementation of the
behaviour under test. That's what makes green mean something.

1. **Run the spec → RED** — every scenario reports *undefined*: that's the work list.
2. **Pick the next scenario, write its step definitions** — **dumb, scenario-specific,
   disposable**. Glue is machine-maintained output, not a clever reusable step library.
   Run it → the scenario must fail for the *right* reason (behaviour missing, not broken glue).
3. **Minimal implementation → GREEN** — only enough to pass.
4. **Refactor** with the scenario green — clean up, remove duplication.
5. **Repeat** until the runner reports every scenario green (or explicitly pending).

**Keep the backlog visible** — scenarios not yet built, and specs slated for a later slice, stay
in the runner's report as **pending/todo**, never deleted or silently filtered out. An unimplemented
requirement you can see is a backlog; one you've hidden is a lie about coverage.

**The spec is read-only here** — if a scenario turns out wrong or unimplementable, stop and
hand back to the requirements step with the driver; never bend the `.feature` file to make it
pass.

Commit the code to the `feat/<slug>` branch as you go (each green step).

**What to test** — the spec's scenarios (acceptance, via the runner), plus unit tests for pure
functions worth verifying in isolation. Not everything, and never external code (libraries,
frameworks, third-party APIs).

**Follow the project's test setup** (`CLAUDE.md` / existing tests) for how tests are written and run.

**Code explains itself** — prefer clear names and structure over comments; document only where the
*intention* is genuinely hard to grasp, never what the code already says.

## Done when

The **runner reports** every scenario in the spec green (or explicitly pending), the suite
passes, and the implementation is the minimum that satisfies it — no speculative code.
