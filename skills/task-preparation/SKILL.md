---
name: task-preparation
description: Prepares a selected concrete docs/tasks task through task-local spec, optional plan, review pauses, and execution handoff before code changes. Use when roadmap state is confirmed and next work is task-local preparation.
---

# Task Preparation

## Quick start

Use after roadmap exists and one concrete task already selected or clearly next.
This skill consumes an existing concrete task. It does not create task directories, reshape roadmap structure, or implement code.

## Mandatory rules

Create or update task-local docs only for concrete implementation work on an existing task. Pure docs governance, such as architecture edits, task or module reshaping, milestone changes, task creation, or index maintenance, does not create an implementation spec or code permission.

- Enter only when one existing concrete task is selected or clearly next from confirmed roadmap state. If milestone confirmation, task selection, or dependencies are still ambiguous, stop and use `milestone-planning`.
- Always write `spec.md`. If the user asks to skip it, refuse and stop.
- Default to no `plan.md`. Create it only when sequencing is non-obvious because of ordering, compatibility, migration, rollout, cross-module coordination, or verification risk.
- Keep `1 task -> 1 spec`. If multiple specs seem necessary, stop and use `milestone-planning` to split the task first.
- `plan.md` supplements the approved `spec.md`; it does not restate it.
- Compact specs are fine; vague specs are not.
- If another agent or fresh conversation may pick up the work, make boundaries, non-goals, allowed minimal implementation, proof expectations, and likely first edit surface explicit.

Required before drafting:

- Run a clarification loop before any `spec.md` content, even when the task seems obvious.
- If code or docs can answer a question, explore first instead of asking.
- Walk each blocking design branch to shared understanding.
- Ask one blocking question at a time and include your recommended answer.
- Do not draft `spec.md` until scope, acceptance, non-goals, migration risk, rollout, and proof expectations are settled enough for shared understanding.
- If a design branch would materially change scope, acceptance, proof, rollout, migration ownership, implementation level, `Option Selection`, `Design Overview`, `Testing and Verification`, or allowed minimal implementation, treat it as blocking.
- Do not draft from assumed defaults while blocking branches remain unresolved.
- If an `Undecided` item still blocks `spec.md`, `plan.md`, reviewed-doc follow-up, or execution handoff, resolve it before moving on.
- Keep explicit option comparison when real alternatives exist.
- After shared understanding is reached, draft the full `spec.md` in one pass.

## Advanced features

Default flow:

| Plan Trigger | Flow |
|------------|------|
| No trigger | `spec -> review pause -> auto follow-up (default commit) -> execution handoff` |
| Trigger present | `spec -> review pause -> plan -> review pause -> auto follow-up (default commit) -> execution handoff` |

- After a review pause, clear forward-motion language such as `continue` or `next` means follow the recommended route. Ask a separate approval question only for hard gates.
- After `spec.md` review, write `plan.md` only when a plan trigger is present; otherwise proceed through auto follow-up.
- After `plan.md` review, proceed through auto follow-up, including the default docs commit, unless the user explicitly refuses that commit.
- Do not skip the reviewed-docs commit unless the user explicitly wants the docs left uncommitted.
- If reviewed docs stay uncommitted, say it is an explicit exception, give the reason, and list affected files.
- Before execution handoff, state the docs follow-up outcome, `Decided`, `Undecided`, `Next skill`, and `Stop point`.
- When `milestone-planning` has just created or reshaped roadmap or task docs, report that as a planning review pause before entering task-local doc work.
- If `milestone-planning` created the first concrete task in a milestone, the first `continue` may accept planning docs and move into `spec.md` work when no hard gate blocks it.

Reference loading:

- Use `references/spec-template.md` for task-local `spec.md`.
- Use `references/plan-template.md` for task-local `plan.md`.
- Use `references/index-template.md`, `references/architecture-template.md`, or `references/context-template.md` only when that exact doc type is relevant.
- Do not load every reference by default.
