# Specs

This folder holds one subfolder per feature. Each feature moves through the same stages, and each stage produces a file the owner reviews before the next begins.

| Stage | File | Answers | Reviewed by |
|---|---|---|---|
| 1. Specify | `spec.md` | What should it do, for whom, and why? How do we know it works? | Owner approves |
| 2. Plan | `plan.md` | How will we build it? Which technology and dependencies, and why? | Owner approves dependencies |
| 3. Tasks | `tasks.md` | What are the small, ordered steps, each with its own check? | Owner skims |
| 4. Build | code and tests | Do the acceptance scenarios and success criteria pass? | Automated checks, then owner tries it |

Project-wide rules live in [`../docs/constitution.md`](../docs/constitution.md). Terms are explained in [`../docs/glossary.md`](../docs/glossary.md).

This structure follows GitHub's open-source Spec Kit (constitution, then spec, plan, tasks), used by hand without installing the tool. The review emphasis comes from Microsoft's "Cheap code, precious trust" (October 2026): spend human attention on specs and invariants, and let automated checks cover the rest.

## Roadmap

| # | Feature | Status |
|---|---|---|
| 001 | [View a BTO template in 3D](001-view-template-in-3d/spec.md) | Spec approved. [Plan](001-view-template-in-3d/plan.md) drafted. |
| 002 | Switch between interior themes | Not started |
| 003 | Customise the layout (remove non-structural walls, kitchen options) | Not started |
| 004 | Add and arrange furniture | Not started |
| 005 | Upload a floor plan, with automatic digitising proposed for confirmation | Not started |
| 006 | More flat types (2-room Flexi, 3-room, 5-room, 3Gen) | Not started |
| 007 | Save, share and export a mockup | Not started |

The order can change. Each feature gets its own spec when we reach it.
