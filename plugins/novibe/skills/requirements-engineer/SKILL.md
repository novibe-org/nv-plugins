---
name: requirements-engineer
description: Capture what to build as an executable feature spec — business scenarios (outcomes, not mechanism) with Examples tables. Use before implementing a feature, to pin intent as acceptance criteria. On its own, or as the spec step of the `novibe` flow.
---

# Requirements Engineer

Intent is the work. Requirements are the most expensive thing to get wrong — the cost to fix
multiplies the later you catch it — and a vague ask becomes generated code that isn't what
you meant. So pin **what to build and why** as an **executable spec** before any code: it is
the source of truth for "done," and it becomes the test.

## Write the feature spec (Gherkin)

- **Standard location**: `tests/behavior/features/<name>.feature` — one feature per file,
  with an `FS-<n>` id.
- **Business outcome, not mechanism.** Say what the user/operator gets, never how it's built
  (no endpoints, status codes, class names). *"It is refused as unauthenticated"*, not
  *"returns 401"*.
- **Frame the why**: a short problem statement + `As a … I want … so that …`.
- **Structure**: `Background` for shared setup; a `Scenario` per acceptance case;
  **`Scenario Outline` + `Examples` tables** when the same behaviour varies by data.
- **One outcome per scenario**, readable by a non-engineer.
- Tag not-yet-automated scenarios `@wip`.

## Done when

You and the driver agree the scenarios capture the intended behaviour — the spec reads as the
contract for "done" in business language, with `Examples` covering the meaningful variations.
