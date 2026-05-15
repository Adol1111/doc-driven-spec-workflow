---
name: task-preparation
description: Prepares a selected concrete docs/tasks task through task-local spec, optional plan, review pauses, and execution handoff before code changes. Use when roadmap state is confirmed and next work is task-local preparation.
---

# Task Preparation

## Quick start

Use after roadmap exists and one concrete task already selected or clearly next.
This skill consumes an existing concrete task. It does not create task directories, reshape roadmap structure, or implement code.

## Workflows

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

Use a grill-me style clarification pass inside this stage:

- Inspect code/docs first when they can answer.
- Ask one question at a time when boundary, acceptance, non-goals, migration risk, rollout, or verification proof still unclear.
- Give a recommended answer with each question when useful.

## Mandatory rules

Create or update task-local docs only for concrete implementation work on an existing task. Pure docs governance, such as architecture edits, task/module reshaping, milestone changes, task creation, or index maintenance, does not create an implementation spec or code permission.

- Default to writing `spec.md`.
- If the user asks to skip `spec.md`, refuse and stop; do not draft `spec.md` in the same response.
- Default to no `plan.md`; create it only when sequencing is non-obvious because of ordering, compatibility, migration, cross-module coordination, rollout, or verification risk.
- Treat `plan.md` as a supplement to the approved `spec.md`, not a second spec. Reuse the spec's scope, behavior, and non-goals instead of restating them unless a short recap is needed for clarity.
- If multiple specs seem necessary, stop and use `milestone-planning` to split the task first.
- Compact specs are fine; vague specs are not.
- If another agent, subagent, model, or fresh conversation may pick up the work, make boundaries, non-goals, allowed minimal implementation, proof expectations, and likely first edit surface explicit.
- If boundary, acceptance, non-goals, migration risk, rollout, or verification proof is still unclear, ask exactly one question at a time before drafting.
- Ask before drafting only when execution mode is unclear and the difference matters.

## Advanced features

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
- Before execution handoff, state `Decided`, `Undecided`, `Next skill`, and `Stop point`.
- When `milestone-planning` has just created or reshaped roadmap/task docs, report those changes as a planning review pause before entering task-local `spec.md` work.
- If `milestone-planning` creates the first concrete task in a milestone, the first `continue` may accept planning docs and advance into `spec.md` work if no hard gate blocks the handoff. The next `continue`, after `spec.md` review, should write `plan.md` when a trigger is present or proceed through auto follow-up when no trigger is present, rather than ask for redundant checkpoint-only approval.

Reference loading:

- Use `references/spec-template.md` for task-local `spec.md`.
- Use `references/plan-template.md` for task-local `plan.md`.
- Use `references/index-template.md`, `references/architecture-template.md`, or `references/context-template.md` only when that exact doc type is relevant.
- Do not load every reference by default.
