---
name: architect
description: Design a change in the C4 architecture model before writing code, and record significant decisions as terse ADRs. Use when a change adds or alters components, boundaries, integrations, or cross-cutting decisions — on its own, or as the design step of the `novibe` flow.
---

# Architect

Design before code. The **model is the crucial artifact** — the source of truth that carries
the architecture into the implementation step and into the agent's working context.
**Diagrams are secondary**: generated *from* the model, purely for the humans who later need
to understand the software. That's why we use **LikeC4** — it separates model and view
cleanly, and emits Mermaid that renders directly in Markdown/GitHub. Invest in the model;
treat the views as derived output.

## Model the architecture (LikeC4)

- **Standard location**: `docs/architecture/current/` and `docs/architecture/vision/`, each
  a LikeC4 project (`likec4.config.json` + `model.c4` + `views.c4`).
- **Never hand-edit a generated `VIEWS.md`** — change the model and regenerate.
- **Split files**: `model.c4` (elements + relations) and `views.c4` (views). Across files,
  reference nested elements by full path (e.g. `system.container.component`).
- **`current/` vs `vision/`**: `current/` = what's built (edit it for the increment you're
  building); `vision/` = the target/direction.
- **Extend, don't rewrite** — add only the elements and relations the change introduces.
- **Regenerate only once you and the driver agree on the architecture** — not after every
  edit. Iterate on the `.c4` together; when you both agree it's settled, run the standard
  command `pnpm gen:diagrams` (script: `scripts/gen-diagrams.ts`) to refresh the views.

## ADRs are optional and rare — don't write books

**Default to no ADR.** Most design lives in the model. Write one only for a **crucial,
cross-cutting** decision: a new integration pattern, a security/boundary invariant,
build-vs-reuse, repo structure. **Never package a feature as an ADR** — features belong in a
feature spec, not in decision records.

When one is warranted:

- **MADR-lite**: `Context` (why), `Options` (one line each), `Decision` (bullets),
  `Consequences` (bullets). ~30–40 lines. No long prose, no embedded trees.
- Next number in `docs/adrs/`; one decision per ADR; link related ones.

## Done when

You and the driver agree on the model, the views are regenerated, and an ADR exists **only
if** a crucial cross-cutting decision was actually made — often there is none.
