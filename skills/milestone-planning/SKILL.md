---
name: milestone-planning
description: Decomposes docs-driven delivery scope into milestones, optional modules, and independently reviewable tasks before task-local spec work. Use when roadmap boundaries, delivery order, or task breakdown are unclear.
---

# Milestone Planning

## Quick start

Use this before `spec.md` work when roadmap shape still unclear.
If planning direction is still unresolved, route back to `planning-clarification` before decomposing milestones, modules, or tasks.

## Workflows

| Boundary | Rule |
|----------|------|
| Milestone | Start from release goal, phase boundary, or acceptance boundary, not feature count. Use one milestone for the same delivery goal plus same completion definition and no meaningful stage boundary. Split when phase boundaries, exit criteria, release timing, or frozen history differ. |
| Module | Optional. Use only for multiple durable capability areas with distinct ownership, dependency graphs, risk profiles, release boundaries, or acceptance criteria. |
| Task | One independently reviewable implementation round delivering one coherent capability outcome, including required tests, migrations, docs/status updates, refactors, and verification. When the user needs roadmap-level tasks so a first implementation task can be chosen, prefer user-visible or operator-visible capability boundaries. Do not hide multiple independently selectable capabilities inside a vague `core`, `MVP`, `foundation`, or `polish` task. |

Routing:

| Situation | Action |
|-----------|--------|
| Empty `Open Milestones` and no docs/prompt evidence gives a concrete target or roadmap misalignment | Ask the planning mode question first |
| Empty `Open Milestones` and docs/prompt evidence gives a concrete short-term target | Decompose directly with `milestone-planning` |
| Empty `Open Milestones` and docs/prompt evidence says roadmap direction, goals, or phase boundaries are not aligned | Use `planning-clarification` first |
| `Roadmap confirmed: no` and user asks to decompose or start work | Ask whether to re-evaluate milestone structure or continue on the current milestone path; keep tasks provisional |
| Cross-milestone movement | Resolve previous milestone closure first |

**Planning mode question**: *"Do you already have a concrete short-term target for this iteration, or do we need to realign the next stage of the roadmap first?"*

## Mandatory rules

- Explain why each milestone, module, and task boundary exists. Structure without rationale is incomplete.
- Empty `Open Milestones` is a routing signal, not enough information to decompose by itself. Check `docs/tasks/planning-inbox.md`, `docs/tasks/backlog.md`, relevant task docs, and the prompt before choosing a path.
- Ask the planning mode question when no evidence identifies a concrete short-term target or roadmap misalignment.
- Use `planning-clarification` only for positive ambiguity evidence.
- If planning direction is still unresolved, do not decompose roadmap structure yet; route to `planning-clarification`.
- Decompose directly when docs or prompt evidence gives a concrete short-term target.
- Treat milestone confirmation as the primary routing signal. Tasks in `Roadmap confirmed: no` milestones are provisional planning output, not formally selected execution work.
- Treat milestone/module/task creation or reshaping as docs governance only. It does not authorize spec writing or implementation.
- Use stable task directory slugs without numeric order prefixes. Task order is expressed by the order of task links in the relevant `index.md`, not by task filenames.
- Stop at a planning review pause after creating or reshaping roadmap/task docs.
- When the user clearly indicates they want to move forward after reviewing planning docs, treat that as approval for that default follow-up.
- Hand off to `task-preparation` only after the current concrete task is chosen from confirmed roadmap state and no hard gate blocks the handoff.
- Before handoff, state `Decided`, `Undecided`, `Next skill`, and `Stop point`.

## Advanced features

- `Handoff Notes`: temporary transfer queue for follow-up findings. Resolve before milestone closure.
- Newly discovered follow-up work during an active milestone should go to that milestone's `Handoff Notes` first by default. Skip that only when the user explicitly decides the item is high priority enough to interrupt the current milestone and reorder or insert work immediately.
- **Before closure**: every `Handoff Notes` item must be resolved to current-milestone open work, later milestone, `docs/tasks/backlog.md`, or removal.
- Close milestone when original exit criteria are satisfied.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- If the user appears to be moving into a later milestone, resolve previous milestone closure and target milestone confirmation before decomposing or selecting work there.
- If milestone entry is still ambiguous, do not answer the routing question on the user's behalf before the user responds.

## Output Requirements

Always provide:

- Recommended milestone structure
- Why it is one milestone or several
- Whether modules are needed
- Task list per milestone or module
- Delivery order when not obvious
- Assumptions or open questions

Documents to create/update:

- `docs/tasks/index.md`
- Optional: `docs/tasks/backlog.md`
- `docs/tasks/<milestone>/index.md`
- Optional: `docs/tasks/<milestone>/<module>/index.md`
- `docs/tasks/<milestone>/<task>/task.md`

Use `references/roadmap-template.md` for exact planning-stage shape.
