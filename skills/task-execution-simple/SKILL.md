---
name: task-execution-simple
description: Implements a prepared concrete docs/tasks task through branch isolation, code changes, verification, review, and branch closing. Use when task-local spec or plan work is complete and next step is straightforward direct execution.
---

# Task Execution Simple

## Quick start

Use after `task-preparation` finished and task ready for direct impl.
This skill owns execution isolation, implementation, verification, implementation review, and branch closing. It does not own roadmap decomposition or task-local `spec.md` / `plan.md` authoring.

## Mandatory rules

- Follow the task-local `spec.md` and optional `plan.md` for testing and verification expectations.
- Default never implement on the current branch. Create a dedicated task branch in the current workspace unless the user explicitly wants another path.
- Use a worktree only when the user explicitly wants one or parallel/high-conflict execution makes it meaningfully better.
- Handle branch isolation and any other readiness work before code edits.
- Verify implementation and update affected docs or status in the same round when behavior, API shape, task status, architecture assumptions, or stable constraints changed.
- Default to committing completed implementation work before asking for implementation review.
- Treat `plan.md` commit points as judgment-based checkpoints, not mandatory per-stage commits. Simple tasks may only need the final task commit; complex tasks may commit after any stage that forms a verified, reviewable, reversible stable state.
- If relevant existing automated tests fail during the task, do not ignore them just because the task did not require adding new unit tests.
- Prefer fixing production code so existing tests keep expressing the same behavior.
- If existing tests need semantic changes because the task intentionally changes behavior, explain the reason and get user confirmation before changing what those tests assert.
- Small test-file repairs that preserve the original assertion intent do not need separate confirmation.
- Stay on current branch only when user explicitly chooses that path.
- Branch closing must be resolved before starting another task.
- After implementation review, branch closing starts by choosing one explicit outcome: `merge and keep branch`, `merge and delete branch`, or `discard work`.
- Present closing outcomes as a numbered choice so the user can reply with `1`, `2`, or `3` instead of retyping the full outcome text.
- When closing is unresolved, use the fixed closing prompt from `references/task-execution-detailed-rules.md` instead of paraphrasing the choices freely.
- Generic forward-motion language such as `continue`, `next`, or `go on` may enter branch closing, but it does not choose a closing outcome.
- `git merge`, including fast-forward merge, must not run until a merge outcome is explicit.
- Any default branch-closing preference must be explicit in the current task context; do not infer it from how a previous task was closed. Persistent defaults may cover `merge and keep branch` or `merge and delete branch`, but never `discard work`.
- If a closing outcome is already explicit, `continue` may advance only its non-destructive steps.
- Confirm before deleting any branch or worktree. Removing worktree does not remove its task branch.
- Destructive actions, including branch deletion, worktree deletion, and discard, always require explicit confirmation at execution time. `discard work` always requires a fresh explicit confirmation for the current task, and `merge and delete branch` still requires a second explicit confirmation when branch deletion is about to run.

Code is source of truth when code and docs diverge. If implementation changes behavior, API shape, task status, architecture assumptions, or stable constraints, update the relevant docs in the same round. Move stable rules out of `docs/context/`.

## Advanced features

Use `references/task-execution-detailed-rules.md` only as supplementary clauses when the main skill leaves an execution edge case unresolved.
Read it for test-semantics changes, docs-follow-up edge cases, fixed closing-prompt wording, destructive-confirmation timing, current-task-context rules, or checkpoint boundary cases.

Default flow:

1. Receive handoff context from `task-preparation`.
2. Create execution isolation and complete readiness work.
3. Implement one concrete task.
4. Verify behavior and update affected docs or status.
5. Commit verified implementation work, including any useful checkpoint commits from `plan.md`.
6. Stop for implementation review of the committed task branch or merge diff.
7. Ask for one explicit branch-closing outcome and execute only that outcome.
8. State `Decided`, `Undecided`, `Next skill`, and `Stop point` at implementation review and branch-closing gates.
