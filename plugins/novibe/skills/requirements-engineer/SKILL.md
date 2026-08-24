---
name: requirements-engineer
description: Turn a rough idea into a Gherkin requirements spec for one small vertical slice.
---

# Requirements Engineer

**In:** a rough idea.
**Out:** a **Gherkin** spec at `features/<epic>/<feature>.feature`.

**Build the right thing** — what gets built is what's actually needed, before anyone builds it
*right*. **Requirements come from the user — elicit them, don't invent them.** Work top-down,
just-in-time; never specify the whole world.

1. **Get the epic** — the higher-level *why*: read `features/<epic>/epic.md` if it
   exists, else sketch it *good enough* with the user.
2. **Pick one feature** — a small **vertical slice** that advances the epic; detail only this.
3. **Write the scenarios** — business outcomes, not mechanism (*"refused as unauthenticated"*, not
   *"returns 401"*); `As a … I want … so that …`; a `Scenario` per case; `Scenario Outline` +
   `Examples` when data varies. The spec executes verbatim through a BDD runner, so keep steps
   declarative yet concrete enough to bind.

   **One scenario per choice — and one for every choice.** A scenario earns its place when someone
   could have decided it differently: that search reaches every page, that a category is a place
   rather than a filter. Anything that follows *necessarily* from a scenario already written is
   not a second scenario, it is the same decision restated — cut it, or the spec reads as ceremony
   and the driver stops reading it. The rule runs the other way too, and that half is easier to
   miss: **if something a user will notice has no scenario, that is a missing requirement, not a
   detail to settle in code.** Both failures look like judgement in the moment; together they make
   the spec's size arbitrary, which is worse than either.
4. **Open the feature branch and its draft PR** — create `feat/<slug>`, commit the spec, push,
   and open a **draft PR** (`gh pr create --draft`) titled for the slice. The draft is the slice's
   container from minute one: the spec is a reviewable diff immediately, later steps push the same
   branch, and the PR stays draft until the developer step proves the slice.

**Layout** — specs live in `features/` at the **repo root**, next to `src/` — not under `docs/`.
They are executable source, not prose; the BDD runners of every ecosystem look there by convention.
One feature = one `.feature` in the epic's folder (`features/<epic>/`); the **filename is a
kebab-case slug** — the feature's stable handle. Features belong to the epic **by folder** (no
cross-refs); `epic.md` holds the *why*.

**No internal planning docs** — the spec is the sharable, living artifact, not a `.claude/plan`.

## Done when

The driver agrees the Gherkin scenarios capture the intended behaviour for one small vertical slice.
