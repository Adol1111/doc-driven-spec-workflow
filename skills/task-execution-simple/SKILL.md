---
name: task-execution-simple
description: Implements a prepared concrete docs/tasks task through branch isolation, code changes, verification, review, and branch closing. Use when task-local spec or plan work is complete and next step is straightforward direct execution.
---

# Task Execution Simple

## Quick start

Use after `task-preparation` finished and task ready for direct impl.
This skill owns execution isolation, implementation, verification, implementation review, and branch closing. It does not own roadmap decomposition or task-local `spec.md` / `plan.md` authoring.

## Workflows

| Gate | Required behavior |
|------|-------------------|
| Branch | Default never implement on the current branch; create a dedicated task branch by default unless the user explicitly chooses otherwise or a worktree workflow is specifically needed. |
| Readiness | Handle execution isolation and any other pre-code readiness work before implementation edits. |
| Verification | Verify implementation and update docs/status in the same round when behavior, API shape, or task state changed. |
| Commit | Commit verified implementation work on the task branch before implementation review. If `plan.md` defines commit points, commit at those natural stable points after local verification for that slice. |
| Review | Stop for implementation review after the verified implementation is committed, before merge, destructive cleanup, or branch deletion. |
| Closing | Resolve only any remaining hard gate such as branch deletion or destructive cleanup after implementation review. |

After an implementation review pause, treat any clear forward-motion message as approval to follow the recommended non-destructive next step. Ask a separate approval question only for hard gates.

## Mandatory rules

- Follow the task-local `spec.md` and optional `plan.md` for testing and verification expectations.
- Treat `plan.md` commit points as judgment-based checkpoints, not mandatory per-stage commits. Simple tasks may only need the final task commit; complex tasks may commit after any stage that forms a verified, reviewable, reversible stable state.
- If relevant existing automated tests fail during the task, do not ignore them just because the task did not require adding new unit tests.
- Prefer fixing production code so existing tests keep expressing the same behavior.
- If existing tests need semantic changes because the task intentionally changes behavior, explain the reason and get user confirmation before changing what those tests assert.
- Small test-file repairs that preserve the original assertion intent do not need separate confirmation.
- Default to creating dedicated task branch in current workspace.
- Use worktree only when user explicitly wants one or when parallel/high-conflict execution makes separate workspace valuable.
- Stay on current branch only when user explicitly chooses that path.
- Confirm before deleting any branch or worktree. Removing worktree does not remove its task branch.
- Branch closing must be resolved before starting another task.
- Merge complete does not mean branch closing complete. A merged branch that is still undeleted remains an explicit closing choice.
- Closing outcomes are limited to: merge and keep branch, merge and delete branch, or discard work.
- If merge plus cleanup is chosen, confirm whether cleanup includes deleting the merged task branch.
- If the user asks to move forward, keep moving through non-destructive closing steps, but stop before branch deletion, worktree deletion, or discard.
- Default to committing completed implementation work before asking for implementation review.

Code is source of truth when code and docs diverge. If implementation changes behavior, API shape, task status, architecture assumptions, or stable constraints, update the relevant docs in the same round. Move stable rules out of `docs/context/`.

## Advanced features

Use `references/task-execution-detailed-rules.md` when branch-closing, checkpoint, or execution edge cases are unclear.

1. Receive handoff context from `task-preparation`.
2. Create execution isolation and complete readiness work before code edits.
3. Implement one concrete task.
4. Verify behavior and update docs/status affected by implementation.
5. Commit verified implementation work, including any planned commit-point slices.
6. Stop for implementation review of the committed task branch or merge diff.
7. Resolve branch closing through one explicit outcome: merge and keep branch, merge and delete branch, or discard work.
8. State `Decided`, `Undecided`, `Next skill`, and `Stop point` at implementation review and branch-closing gates.
