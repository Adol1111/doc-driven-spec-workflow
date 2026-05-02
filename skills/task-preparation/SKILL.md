---
name: task-preparation
description: Use when a docs-driven repository has a selected or selectable concrete docs/tasks task and needs task-local spec or plan governance before code execution.
---

# Task Preparation

Use after roadmap structure exists and one concrete task already exists in `docs/tasks/` and is selected or selectable from confirmed roadmap state.

Owns task-local `spec.md`, optional `plan.md`, review pauses, routine follow-up, and execution handoff context. It consumes an existing roadmap-layer task; it does not create task directories, author `task.md`, or reshape roadmap structure.

## Required Gates

| Gate | Required behavior |
|------|-------------------|
| Task selection | Enter only when an existing concrete task is selected or clearly next from confirmed roadmap state. If milestone confirmation, task selection, or dependencies are still ambiguous, stop and use `milestone-planning`. |
| Governance mode | Docs governance changes roadmap/docs only and does not authorize code. |
| Spec | One task-local `spec.md` defines behavior, scope, exclusions, and tradeoffs. Default `1 task -> 1 spec`; revise instead of duplicating. |
| Plan | Default no `plan.md`. Create it only when a plan trigger is present. |
| Review | Stop after writing `spec.md`, and after `plan.md` when required, so the user can review the artifact. |
| Operational follow-up | After review approval, default to committing reviewed task-local docs without a second approval question. Leaving them uncommitted requires explicit user approval plus reason and affected files. |
| Handoff | After docs and routine follow-up are ready, hand off to an execution skill such as `task-execution-simple`. |

After a review pause, treat any clear forward-motion message as approval to follow the recommended path. Ask a separate approval question only for hard gates.

## Spec and Plan

Create or update task-local docs only for concrete implementation work on an existing task. Pure docs governance, such as architecture edits, task/module reshaping, milestone changes, task creation, or index maintenance, does not create an implementation spec or code permission.

- Default to writing `spec.md`.
- If the user asks to skip `spec.md`, refuse and stop; do not draft `spec.md` in the same response.
- Default to no `plan.md`; create it only when sequencing is non-obvious because of ordering, compatibility, migration, cross-module coordination, rollout, or verification risk.
- Treat `plan.md` as a supplement to the approved `spec.md`, not a second spec. Reuse the spec's scope, behavior, and non-goals instead of restating them unless a short recap is needed for clarity.
- If multiple specs seem necessary, stop and use `milestone-planning` to split the task first.
- Compact specs are fine; vague specs are not.
- If another agent, subagent, model, or fresh conversation may pick up the work, make boundaries, non-goals, allowed minimal implementation, proof expectations, and likely first edit surface explicit.
- Ask before drafting only when execution mode is unclear and the difference matters.

## Review Pauses and Handoff

Default flow:

| Plan Trigger | Flow |
|------------|------|
| No trigger | `spec -> review pause -> auto follow-up (default commit) -> execution handoff` |
| Trigger present | `spec -> review pause -> plan -> review pause -> auto follow-up (default commit) -> execution handoff` |

- After a `spec.md` review pause, clear forward-motion language such as `continue` or `next` leaves the review pause and follows the selected route: write `plan.md` when a plan trigger is present, otherwise proceed through auto follow-up.
- After a `plan.md` review pause, the same forward-motion language proceeds through auto follow-up, including the default commit unless the user explicitly refuses it.
- Normal routes:
  `spec -> review pause -> auto follow-up (default commit)`
  `spec -> review pause -> plan -> review pause -> auto follow-up (default commit)`
- Do not skip that commit unless the user explicitly says not to commit the reviewed docs, for example `ok, but I don't want to commit that yet`.
- If reviewed docs remain uncommitted, say that this is an explicit user-approved exception, give the reason, and report the affected files.
- Before execution handoff, state the auto follow-up outcome: committed, or intentionally uncommitted with files listed.
- When `milestone-planning` has just created or reshaped roadmap/task docs, report those changes as a planning review pause before entering task-local `spec.md` work.
- If `milestone-planning` creates the first concrete task in a milestone, the first `continue` may accept planning docs and advance into `spec.md` work if no hard gate blocks the handoff. The next `continue`, after `spec.md` review, should write `plan.md` when a trigger is present or proceed through auto follow-up when no trigger is present, rather than ask for redundant checkpoint-only approval.

## Task And Status Rules

- Use `docs/tasks/` as the only source of truth for concrete next work, not `docs/context/` or architecture alone.
- Tasks in `Roadmap confirmed: no` milestones remain provisional until the selectable-task gate is satisfied.
- Respect task sizing, dependencies, and status exactly. If the candidate is too small, too broad, only a sub-step, or implies a missing roadmap shape, stop and use `milestone-planning`.
- Each concrete task already has a directory with `task.md`; task preparation adds `spec.md` and optional `plan.md` there. `task.md` tracks status, dependencies, and acceptance points, not detailed implementation steps.
- Keep implementation steps inside `spec.md`, optional `plan.md`, or checklist items; do not promote them into tasks.
- If a planning stage just changed roadmap docs, report and review that planning output before drafting the first task spec.

## Detailed Rules and References

Use the task-local references when needed:

- `references/spec-template.md`
- `references/plan-template.md`
- `references/index-template.md`
- `references/architecture-template.md`
- `references/context-template.md`

## When To Use

Use when the repository has the docs-driven layout and the current concrete task is selected or ready to select from confirmed roadmap state, and the next work is task-local `spec.md` or `plan.md` preparation before code execution.

Do not use when:

- milestone/module/task structure is still being decided; use `milestone-planning` first
- the next work is direct implementation, verification, or branch closing; use `task-execution-simple`
- the repository does not use this docs-driven layout
