---
name: architect
description: Turn a Gherkin spec into a C4 architecture model for one slice — high-level design and flows. Terse ADR only for a crucial cross-cutting decision.
---

# Architect

**In:** the Gherkin spec at `docs/requirements/<epic>/<feature>.feature`.
**Out:** a **C4 model** at `docs/architecture/current/` (LikeC4).

Design it right — turn the spec into a clear design. The **model is the crucial artifact**: the
source of truth that carries the architecture into implementation and into the agent's context.
**Diagrams are secondary** — generated *from* the model, for the humans who later read it. That's
why we use **LikeC4**: it separates model and view, and emits Mermaid that renders in Markdown/GitHub.

**Never output code** — model/design level only; implementation is the developer's job.
**No internal planning docs** — the design lives in the C4 model, a sharable, living artifact.

1. **Locate the model** — `docs/architecture/current/` (built) + `vision/` (target), each a LikeC4
   project (`likec4.config.json` + `model.c4` + `views.c4`). Reference nested elements across files
   by full path (e.g. `system.container.component`).
2. **Design to the spec** — extend `current/` for the slice: add only the elements and relations it
   introduces. If there's no higher-level architecture yet, sketch the `vision/` HLD *good enough* first.
3. **Agree, regenerate, commit** — iterate on the `.c4` with the driver; when you both agree it's
   settled, run `pnpm gen:diagrams` and commit the model to the `feat/<slug>` branch. Never
   hand-edit a generated `VIEWS.md`.
4. **ADR only if warranted** — a crucial cross-cutting decision (integration pattern,
   security/boundary invariant, build-vs-reuse, repo structure): terse MADR-lite (~30–40 lines),
   next number in `docs/adrs/`. Default to none; never package a feature as an ADR.

## Done when

You and the driver agree the model meets the spec, the views are regenerated, and an ADR exists
only if a crucial decision was actually made — often none.
