---
name: task-preparation
description: Use when a docs-driven repository has a selected or selectable concrete docs/tasks task and needs task-local spec or plan governance before code execution.
---

# Task Preparation

Use after roadmap structure exists and one concrete task is selected or selectable from confirmed roadmap state.

Selectable task gate:

- its milestone has `Roadmap confirmed: yes`
- previous milestone closure is resolved when crossing milestones
- task status is `planned` or `in_progress`
- task dependencies are satisfied or explicitly waived
- no previous branch-closing or milestone-transition hard gate is unresolved
- the user selected it, or `docs/tasks/` clearly identifies it as next by order and status

Owns task-local `spec.md`, optional `plan.md`, review pauses for those docs, routine follow-up after review, and handoff context into an execution skill. Does not own implementation edits, branch/worktree isolation, readiness, post-code verification, or branch closing.

## Required Gates

| Gate | Required behavior |
|------|-------------------|
| Governance mode | Docs governance changes roadmap/docs only and does not authorize code. Task preparation requires a selected concrete task. |
| Spec | One task-local `spec.md` defines behavior, scope, exclusions, and tradeoffs. Default `1 task -> 1 spec`; revise instead of duplicating. |
| Plan | Default no `plan.md`. Create task-local `plan.md` only when a plan trigger is present. Spec and plan are separate documents. |
| Review | Stop after writing `spec.md`, and after `plan.md` when required, so the user can review the artifact. |
| Operational follow-up | After review approval, the agent may handle routine continuation steps such as committing reviewed docs or reporting intentional uncommitted state without a second approval question. |
| Handoff | After docs and routine follow-up are ready, hand off to an execution skill such as `task-execution-simple`. |

After a review pause, treat any clear forward-motion message as approval to follow the recommended path. Ask a separate approval question only for hard gates.

## Spec and Plan

Create or update task-local docs only for concrete implementation work. Pure docs governance, such as architecture edits, task/module reshaping, milestone changes, or index maintenance, does not create an implementation spec or code permission. Defer scaffold bootstrap to `docs-workflow-bootstrap`; defer roadmap decomposition and task reshaping to `milestone-planning`.

Plan triggers:

- 3 or more major files/modules must change and modification order affects correctness
- database schema, migration, data backfill, or persisted format changes
- public API, CLI, configuration format, plugin interface, or task document format compatibility boundary
- cross-module coordination such as auth plus billing plus audit, or parser plus adapter plus renderer
- phased rollout, feature flag, migration transition, dual-write, or dual-read behavior
- non-obvious verification order
- multiple implementation slices that remain one task and should not be split by `milestone-planning`
- exploratory spike or risk-reduction step required before implementation edits

Do not create `plan.md` for a small single-capability task with straightforward implementation order. If multiple specs seem necessary, stop and use `milestone-planning` to split the task first.

Compact specs are fine; vague specs are not. When implementation intent could be misread, `spec.md` must capture work type, allowed minimal implementation, relevant non-goals or forbidden shortcuts, and where new responsibility should or must not live. Choose the spec strictness from the expected execution mode: same agent continuing in the current session may use an author-ready compact spec; another agent, subagent, model, or fresh conversation defaults to handoff-ready and must include enough concrete anchors for implementation without a clarification round. Those anchors are preferred proof samples or evidence sources, preferred implementation surface, and case-level acceptance signals. If the execution mode cannot be inferred reliably and the difference matters, ask before drafting. Use task-specific subheadings when helpful, but do not add top-level sections only to restate the template.

## Review Pauses and Handoff

Default flow:

| Plan Trigger | Flow |
|------------|------|
| No trigger | `spec -> review pause -> auto follow-up -> execution handoff` |
| Trigger present | `spec -> review pause -> plan -> review pause -> auto follow-up -> execution handoff` |

- A review pause means the workflow can safely resume in a fresh conversation without relying on chat memory.
- Review approval and routine commit approval are merged by default. If the user reviews `spec.md` or `plan.md` and says `continue`, the agent may commit those reviewed docs when that is the recommended next operational step.
- If the agent intentionally continues with reviewed changes uncommitted, it must say so explicitly and report the affected files.
- If plan trigger status is uncertain, name the suspected trigger and ask whether to create `plan.md` before writing it.
- When `milestone-planning` has just created or reshaped roadmap/task docs, report those changes as a planning review pause before entering task-local `spec.md` work.
- If `milestone-planning` creates the first concrete task in a milestone, the first user `continue` may both accept those planning docs and advance into task-local `spec.md` work if no hard gate blocks the handoff.
- For docs-only governance work, stop after reporting changed files and key diffs. Do not commit unless the user asked up front or confirms after review.

## Task And Status Rules

- Use `docs/tasks/` as the only source of truth for concrete next work, not `docs/context/` or architecture alone.
- A task file exists only as a candidate until it satisfies the selectable-task gate. Tasks in `Roadmap confirmed: no` milestones remain provisional.
- Respect task sizing, dependencies, and status exactly. If the candidate is too small, too broad, only a sub-step, or implies a missing roadmap shape, stop and use `milestone-planning`.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- Do not begin a later milestone until the previous milestone is intentionally active by explicit user choice or reviewed for closure and the target milestone is explicitly confirmed.
- Each concrete task has a directory with `task.md`, task-local `spec.md`, and optional `plan.md`; `task.md` tracks status, dependencies, and acceptance points, not detailed implementation steps.
- Keep implementation steps inside `spec.md`, optional `plan.md`, or checklist items; do not promote them into tasks.
- `docs/tasks/index.md` lists `Open Milestones`, `Completed Milestones`, and supporting planning links such as `Planning Inbox`; it does not list modules, tasks, or counts.
- Report milestone-entry governance changes before drafting the first task spec, and still give the user a chance to review those planning changes first.

## Docs Boundaries

`docs/architecture/` holds stable behavior and long-lived constraints; `docs/tasks/` holds roadmap state and concrete task directories; `docs/context/` holds supporting research or unstable reference. Code is source of truth when code and docs diverge. Move stable rules out of `docs/context/`.

## Detailed Rules and References

Use the existing task execution references for task-local docs:

- `../task-spec-execution/references/spec-template.md`
- `../task-spec-execution/references/plan-template.md`
- `../task-spec-execution/references/task-execution-template.md`
- `../task-spec-execution/references/task-execution-detailed-rules.md`

## Workflow

Follow this order unless the user explicitly asks for something different:

1. If docs or prompt evidence shows task intent is ambiguous, use `superpowers:brainstorming`; do not infer ambiguity from missing docs alone.
2. If the uncertainty is roadmap shape, use `milestone-planning`.
3. Read `docs/index.md`, relevant docs indexes, relevant `docs/architecture/`, and the relevant `docs/tasks/` milestone/module/task docs. Use `docs/context/` only for supporting research or unstable reference.
4. If no suitable open task exists, or the next task is blocked by milestone closure/confirmation, stop and resolve that governance first.
5. Write or update one focused task-local `spec.md`, then stop for review.
6. Check plan triggers. If present, write task-local `plan.md` and stop for review; if uncertain, ask before writing.
7. After review approval, handle routine follow-up such as committing reviewed docs or reporting intentional uncommitted state, then hand off to an execution skill.

## When To Use

Use when the repository has the docs-driven layout and the current concrete task is selected or ready to select from confirmed roadmap state, and the next work is task-local `spec.md` or `plan.md` preparation before code execution. Use `milestone-planning` first when milestone/module/task structure is still being decided. Do not use for repositories without this layout.
