---
name: developer
description: Implement a change test-first — red → green → refactor — turning the spec's scenarios into passing tests. Use when building a feature whose behaviour is specified.
---

# Developer

**In:** the Gherkin spec (`docs/requirements/<epic>/<feature>.feature`) + the C4 model (`docs/architecture/current/`).
**Out:** **working code** for the feature slice.

**Prove it right** — write the test **first**, so you author the proof of correctness instead of
auditing generated code.

1. **Pick the next scenario** from the spec.
2. **Write the test, run it → RED** — confirm it fails for the *right* reason (behaviour missing,
   not a typo).
3. **Minimal implementation → GREEN** — only enough to pass.
4. **Refactor** with the test green — clean up, remove duplication.
5. **Repeat** until every scenario passes (or is left pending).

**What to test** — the spec's scenarios (acceptance), plus unit tests for pure functions worth
verifying in isolation. Not everything, and never external code (libraries, frameworks, third-party APIs).

**Follow the project's test setup** (`CLAUDE.md` / existing tests) for how tests are written and run.

**Code explains itself** — prefer clear names and structure over comments; document only where the
*intention* is genuinely hard to grasp, never what the code already says.

## Done when

Every scenario in the spec is green (or explicitly pending), the suite passes, and the
implementation is the minimum that satisfies it — no speculative code.
