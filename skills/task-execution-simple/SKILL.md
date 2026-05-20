---
name: task-execution-simple
description: Executes one prepared task through isolation, implementation, verification, review, and branch closing. Use when task-local docs are complete and the next work is straightforward direct execution.
---

# Task Execution Simple

## Purpose

Execute one prepared task end-to-end without reopening planning or spec work.

## Use when

- `task-preparation` is complete
- task-local docs are reviewed and ready
- the next work is branch isolation, implementation, verification, and closing

## Do not use when

- task-local `spec.md` is missing, unreviewed, or still blocked
- a `plan.md` trigger is discovered before coding and task-local planning is still incomplete
- the current work is roadmap reshaping, task selection, or task-local design

## Read first

- selected task `task.md`
- task-local `spec.md`
- optional task-local `plan.md`
- relevant milestone or module `index.md`
- current branch and task status
- the current user prompt

## Owns

- execution isolation
- readiness before code edits
- implementation
- verification
- docs and status updates caused by implementation
- implementation review pause
- branch closing choice and destructive cleanup gates

## Must not own

- roadmap decomposition or milestone reshaping
- task-local `spec.md` or `plan.md` authoring
- expanding task scope because execution is difficult
- treating generic forward-motion as permission for destructive closing actions

## Entry checks

- Enter only when task-local docs are complete enough for direct implementation.
- If required task-local docs are missing, blocked, or unreviewed, route back to `task-preparation`.
- Default to a dedicated task branch in the current workspace.
- Stay on the current branch only when the user explicitly chooses that path.
- Use a worktree only when the user explicitly wants one or parallel/high-conflict execution makes it clearly better.

## Default flow

1. Create execution isolation and finish readiness work before coding.
2. Implement the selected task.
3. Verify behavior and update affected docs or task status in the same round.
4. Commit verified implementation work on the task branch.
5. Stop for implementation review.
6. After review, enter branch-closing choice.
7. Execute only the explicitly chosen closing outcome.

## Execution rules

- Follow the approved `spec.md` and optional `plan.md` as the source of truth for scope and proof expectations.
- Code is the source of truth when code and docs diverge; update relevant docs in the same round when implementation changes behavior, API shape, task status, architecture assumptions, or stable constraints.
- Future work discovered during execution belongs in the current milestone `index.md` under `Handoff Notes` by default, unless the user explicitly reprioritizes it into current work.
- If relevant existing automated tests fail during the task, do not ignore them just because the task did not require adding new unit tests.
- Prefer fixing production code so existing tests keep expressing the same behavior.
- If existing tests need semantic changes because the task intentionally changes behavior, explain why and get user confirmation before changing what those tests assert.
- Small test-file repairs that preserve the original assertion intent do not need separate confirmation.
- If `plan.md` includes commit checkpoints, treat them as optional stable boundaries rather than mandatory per-slice commits.

## When to route back

Route back to `task-preparation` before coding when any of these become true:

- a required task-local doc is missing or incomplete
- the task still has a blocking `Undecided` item
- a real `plan.md` trigger appears before coding and the plan does not exist yet
- the task boundary looks wrong enough that execution would have to invent new scope

## Review and default follow-up

- Stop at an implementation review pause only after verified implementation work is committed, unless that commit is blocked by unrelated user edits, unresolved verification failure, or explicit user instruction.
- Treat clear forward-motion language after implementation review as permission to enter branch-closing choice.
- Default follow-up after implementation review is to present closing choices, not to select one.
- Branch closing remains unresolved until one explicit outcome is chosen.
- Must not start another task while branch closing is unresolved.

## Closing outcomes

- `merge and keep branch`
- `merge and delete branch`
- `discard work`

Present closing outcomes as a numbered choice using the fixed prompt in `references/task-execution-detailed-rules.md`.

## Hard gates

- `continue`, `ok`, or `next` may enter closing choice, but they do not choose a closing outcome.
- `git merge`, including fast-forward merge, must not run until a merge outcome is explicit.
- Deleting a branch or worktree always requires explicit confirmation at execution time.
- `discard work` always requires a fresh explicit confirmation for the current task.
- If the user selects `merge and delete branch`, merge first, then ask again before the destructive delete step runs.

## Output

- `Isolation`
- `Implementation result`
- `Verification result`
- `Docs/status updates`
- `Review stop`
- `Closing choice`

## Stop point

- implementation review pause
- closing choice prompt
- or a direct blocking question about execution readiness or test semantics

## Handoff

- `Decided`
- `Undecided`
- `Next skill`
- `Stop point`

## References

- Use `references/task-execution-detailed-rules.md` only for low-frequency execution edge cases and the fixed closing prompt.
