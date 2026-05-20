---
name: task-preparation
description: Prepares one selected concrete task for implementation through task-local spec, optional plan, review pauses, and execution handoff. Use when roadmap state is confirmed and the next work is task-local preparation.
---

# Task Preparation

## Purpose

Turn one selected roadmap task into implementation-ready task-local docs. This is the spec stage.

## Use when

- one concrete task is selected or clearly next from confirmed roadmap state
- the next work is task-local clarification, `spec.md`, optional `plan.md`, and execution handoff
- roadmap structure is stable enough that implementation can be prepared without reshaping milestones or tasks

## Do not use when

- milestone confirmation, task selection, or dependency order is still ambiguous
- the current work is still roadmap decomposition or planning alignment
- the current work is implementation, readiness, verification, or branch closing

## Read first

- selected task `task.md`
- relevant milestone or module `index.md`
- relevant `docs/architecture/` constraints
- supporting `docs/context/` notes when needed
- the current user prompt

## Owns

- task selectability checks
- task-local clarification loop
- `spec.md`
- optional `plan.md`
- review pauses for task-local docs
- default reviewed-doc follow-up
- execution handoff context

## Must not own

- milestone reshaping or new roadmap decomposition
- execution isolation, implementation, verification, or branch closing
- leaving blocking task-boundary ambiguity hidden inside a vague spec
- using `plan.md` to introduce new scope or rewrite the approved spec

## Entry checks

- Enter only when all are true:
  - the milestone has `Roadmap confirmed: yes`
  - previous milestone closure is resolved when crossing milestones
  - task status is `planned` or `in_progress`
  - dependencies are satisfied or explicitly waived
  - no unresolved hard gate blocks progress
  - the user selected the task, or docs clearly identify it as next
- If any of those conditions are unclear, route back to `milestone-planning`.
- Always write `spec.md`. Do not skip it.
- Default to no `plan.md`. Create one only when a real plan trigger is present.

## Clarification rules

- Run a clarification loop before drafting `spec.md`, even when the task looks obvious.
- Use code and docs to resolve present-state facts first.
- Do not treat current implementation or existing docs as authority for future intent, scope, acceptance, or non-goal decisions.
- Ask the user whenever the unresolved branch is about what should change, what should stay out of scope, or what future behavior the task is meant to produce.
- Ask one blocking question at a time and include your recommended answer.
- Treat scope, acceptance, non-goals, migration ownership, rollout behavior, proof expectations, and allowed minimal implementation as blocking when they materially affect the task-local design.
- Do not draft from assumed defaults while blocking branches remain unresolved.

## Default flow

1. Confirm the selected task is genuinely selectable from confirmed roadmap state.
2. If the task is still `planned`, move it to `in_progress` when active task-local work begins.
3. Run the task-local clarification loop until blocking branches are resolved.
4. Draft the full `spec.md` in one pass.
5. Stop for spec review.
6. If a plan trigger is present after spec review, write `plan.md` and stop for plan review.
7. Run the default docs follow-up.
8. Hand off to execution only after the docs follow-up outcome is explicit.

## Plan triggers

- 3 or more major files or modules must change and modification order affects correctness
- database schema, migration, backfill, or persisted-format changes
- public API, CLI, config format, plugin interface, or task-doc compatibility boundary
- cross-module coordination where responsibilities or sequence are non-obvious
- phased rollout, feature flag, dual-read, dual-write, or migration transition behavior
- non-obvious verification order
- multiple implementation slices remain inside one task and should not be split at roadmap level
- exploratory spike or risk-reduction work is required before implementation edits

Do not create `plan.md` for a small single-capability task with straightforward implementation order. If plan-trigger status is uncertain, name the suspected trigger and ask before writing the plan.

## Boundary rules

- Keep `1 task -> 1 spec`. If the task appears to need multiple specs, the task boundary is wrong.
- `plan.md` supplements the approved `spec.md`; it does not restate the spec.
- Do not write follow-up work into the current `plan.md` unless it is already in the current task scope.
- Future work discovered during preparation belongs in the current milestone `index.md` under `Handoff Notes` by default, not in `plan.md`.
- Compact specs are fine; vague specs are not.
- Make boundaries, non-goals, likely first edit surface, and proof expectations explicit enough for a fresh conversation or another agent to continue.

## When to route back

Route back to `milestone-planning` instead of forcing the current spec when any of these become true:

- the task needs two mutually exclusive scope choices to make sense
- the task appears to need two separate specs
- acceptance actually describes two independently reviewable or independently shippable capabilities
- a missing dependency is really a roadmap-order problem rather than a task-local design question

## Task status rules

- Entering active task-local preparation should move the task from `planned` to `in_progress` if it has not already changed.
- Keep the task at `in_progress` while clarification, `spec.md`, optional `plan.md`, review pauses, or docs follow-up are still active.
- Use `blocked` when task-local preparation cannot continue because a real blocking question, external dependency, missing prerequisite, or explicit user hold prevents progress.
- Move a blocked task back to `in_progress` once the blocking condition is resolved and active work resumes.
- Do not mark the task `completed` during preparation; completion belongs to execution after implementation and branch closing are done.

## Review and default follow-up

- Stop at a review pause after `spec.md`.
- Stop at a second review pause after `plan.md` when a plan exists.
- Treat any clear forward-motion message after a review pause as permission for routine follow-up.
- At a `spec.md` review pause, that same forward-motion message counts as approval of the reviewed spec unless the user asks for changes instead.
- Default follow-up after the final task-local review is:
  - commit reviewed task-local docs
  - unless the user explicitly asks to leave them uncommitted
- If reviewed docs stay uncommitted, say that it is an explicit exception, give the reason, and list the affected files.
- The stage is not complete until the docs follow-up outcome is resolved and reported.

## Hard gates

- Do not use `continue` to bypass unresolved task-boundary ambiguity.
- Do not hand off to execution while a blocking `Undecided` item still affects `spec.md`, `plan.md`, or the reviewed-doc follow-up.
- Do not let reviewed-doc approval imply permission for destructive execution actions; those belong to the execution stage.

## Output

- `Task`
- `Readiness check`
- `Blocking questions`
- `Spec result`
- `Plan needed? why?`
- `Review stop`
- `Docs follow-up outcome`
- `Execution handoff`

## Stop point

- spec review pause
- plan review pause
- or a direct blocking question about task-local ambiguity or task boundary failure

## Handoff

- `Decided`
- `Undecided`
- `Next skill`
- `Stop point`

## References

- Use `references/spec-template.md` for task-local `spec.md`.
- Use `references/plan-template.md` for task-local `plan.md`.
