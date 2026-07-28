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

## Ship it

The spec and architecture were already decided with the driver — opening and landing the PR is
execution of that decision, not a new one. Once every scenario is green, keep going:

1. **Open the PR** — push the branch and `gh pr create`, summarizing what changed and why, tied
   back to the scenarios it satisfies.
2. **Feedback is asynchronous — do not poll as if it were not.** A push doesn't make a bot
   review, CI, or Sonar results appear instantly; they take real time (typically minutes). Wait
   an interval matched to that before checking, don't busy-loop. This is exactly the shape a
   background **Agent** handles well — it can wait this out without occupying the driver.
3. **Resolve *bot and CI* feedback in a loop, not once** — fetch comments (`gh pr view
   --comments`, inline review comments via `gh api repos/<owner>/<repo>/pulls/<n>/comments`).
   For each finding **from a bot** (CodeRabbit or similar): verify it against the *current* code
   (a bot's finding can be stale or wrong — confirm, don't assume), fix it or state plainly why
   it does not apply, push, and re-fetch. Repeat until nothing actionable remains — bots respond
   to your fixes, so one pass is never enough.
4. **A comment from the driver — or any human reviewer — is not the same thing.** That's a
   decision, not a finding to mechanically resolve. Stop the autonomous loop, surface it, and
   wait for their actual direction; don't try to satisfy it on your own the way you would a bot.
5. **Get the PR green, GitHub and SonarQube both** — check `gh pr checks`. Resolve the PR's
   SonarQube project/key (`mcp__sonarqube__list_pull_requests`), then its quality gate
   (`mcp__sonarqube__get_project_quality_gate_status` with `pullRequest`, not `branch`) and its
   issues (`mcp__sonarqube__search_sonar_issues_in_projects` with `pullRequest`). Fix what's
   reported — bugs, vulnerabilities, code smells blocking the gate — push, and recheck both.
   Repeat until GitHub checks and the Sonar quality gate are both green.

## Done when

The **runner reports** every scenario in the spec green (or explicitly pending), the suite
passes, the implementation is the minimum that satisfies it — no speculative code — the PR is
open, every review comment has been addressed, and both GitHub checks and the SonarQube quality
gate are green.
