---
name: task-preparation
description: Use when a docs-driven repository has a selected or selectable concrete docs/tasks task and needs task-local spec or plan governance before code execution.
---

# Task Preparation

Use after roadmap structure exists and one concrete task already exists in `docs/tasks/` and is selected or selectable from confirmed roadmap state.

Owns task-local `spec.md`, optional `plan.md`, review pauses for those docs, routine follow-up after review, and handoff context into an execution skill. It consumes an existing roadmap-layer task; it does not create task directories, author `task.md`, or reshape roadmap structure.

## Required Gates

| Gate | Required behavior |
|------|-------------------|
| Task selection | Enter only when an existing concrete task is selected or clearly next from confirmed roadmap state. If milestone confirmation, task selection, or dependencies are still ambiguous, stop and use `milestone-planning`. |
| Governance mode | Docs governance changes roadmap/docs only and does not authorize code. |
| Spec | One task-local `spec.md` defines behavior, scope, exclusions, and tradeoffs. Default `1 task -> 1 spec`; revise instead of duplicating. |
| Plan | Default no `plan.md`. Create it only when a plan trigger is present. |
| Review | Stop after writing `spec.md`, and after `plan.md` when required, so the user can review the artifact. |
| Operational follow-up | After review approval, the agent may handle routine continuation steps such as committing reviewed docs or reporting intentional uncommitted state without a second approval question. |
| Handoff | After docs and routine follow-up are ready, hand off to an execution skill such as `task-execution-simple`. |

After a review pause, treat any clear forward-motion message as approval to follow the recommended path. Ask a separate approval question only for hard gates.

## Spec and Plan

Create or update task-local docs only for concrete implementation work on an existing task. Pure docs governance, such as architecture edits, task/module reshaping, milestone changes, task creation, or index maintenance, does not create an implementation spec or code permission.

- Default to writing `spec.md`.
- Default to no `plan.md`; create it only when ordering, compatibility, migration, cross-module coordination, rollout, or verification complexity makes implementation sequencing non-obvious.
- If multiple specs seem necessary, stop and use `milestone-planning` to split the task first.
- Compact specs are fine; vague specs are not. If implementation intent could be misread, make boundaries, non-goals, and allowed minimal implementation explicit.
- Same-agent continuation may use an author-ready compact spec. Another agent, subagent, model, or fresh conversation should default to handoff-ready anchors. If the execution mode cannot be inferred reliably and the difference matters, ask before drafting.

## Review Pauses and Handoff

Default flow:

| Plan Trigger | Flow |
|------------|------|
| No trigger | `spec -> review pause -> auto follow-up -> execution handoff` |
| Trigger present | `spec -> review pause -> plan -> review pause -> auto follow-up -> execution handoff` |

- A review pause means the workflow can safely resume in a fresh conversation without relying on chat memory.
- If the agent has just drafted `spec.md` and stopped for its review pause, a user reply such as `continue`, `next`, or other clear forward-motion language counts as approval to leave that review pause and follow the recommended safe next step.
- Review approval and routine commit approval are merged by default. If the user reviews `spec.md` or `plan.md` and says `continue`, the agent may commit those reviewed docs when that is the recommended next operational step.
- If the agent intentionally continues with reviewed changes uncommitted, it must say so explicitly and report the affected files.
- When `milestone-planning` has just created or reshaped roadmap/task docs, report those changes as a planning review pause before entering task-local `spec.md` work.
- If `milestone-planning` creates the first concrete task in a milestone, the first user `continue` may both accept those planning docs and advance into task-local `spec.md` work if no hard gate blocks the handoff.
- In that first-task-in-milestone case, once the drafted `spec.md` is shown and paused for review, the next `continue` should approve that reviewed spec and move to the next routine non-destructive step rather than requiring an extra approval whose only purpose is checkpointing the spec.

## Task And Status Rules

- Use `docs/tasks/` as the only source of truth for concrete next work, not `docs/context/` or architecture alone.
- A task file exists only as a candidate until it satisfies the selectable-task gate. Tasks in `Roadmap confirmed: no` milestones remain provisional.
- Respect task sizing, dependencies, and status exactly. If the candidate is too small, too broad, only a sub-step, or implies a missing roadmap shape, stop and use `milestone-planning`.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- Each concrete task already has a directory with `task.md`; task preparation adds task-local `spec.md` and optional `plan.md` there. `task.md` tracks status, dependencies, and acceptance points, not detailed implementation steps.
- Keep implementation steps inside `spec.md`, optional `plan.md`, or checklist items; do not promote them into tasks.
- If a planning stage just changed roadmap docs, report and review that planning output before drafting the first task spec.

## Detailed Rules and References

Use the task-local references when needed:

- `references/spec-template.md`
- `references/plan-template.md`
- `references/index-template.md`
- `references/architecture-template.md`
- `references/context-template.md`

## Workflow

Follow this order unless the user explicitly asks for something different:

1. If docs or prompt evidence shows task intent is ambiguous, use `superpowers:brainstorming`; do not infer ambiguity from missing docs alone.
2. If the uncertainty is roadmap shape, use `milestone-planning`.
3. Read the relevant `docs/tasks/` milestone/module/task docs plus supporting architecture/context only as needed.
4. If no suitable open task exists, or the next task is blocked by milestone closure/confirmation, stop and resolve that governance first.
5. Write or update one focused task-local `spec.md`, then stop for review.
6. If plan triggers are present, write task-local `plan.md` and stop for review; if trigger status is uncertain, ask before writing.
7. After review approval, handle routine follow-up such as committing reviewed docs or reporting intentional uncommitted state, then hand off to an execution skill.

## When To Use

Use when the repository has the docs-driven layout and the current concrete task is selected or ready to select from confirmed roadmap state, and the next work is task-local `spec.md` or `plan.md` preparation before code execution. Use `milestone-planning` first when milestone/module/task structure is still being decided. Do not use for repositories without this layout.
