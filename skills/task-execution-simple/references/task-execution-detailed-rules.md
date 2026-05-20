# Task Execution Simple Detailed Rules

Use this reference only when the main `SKILL.md` leaves a concrete execution edge case unresolved.

This file is not a second workflow definition. It only clarifies low-frequency execution issues and preserves the fixed closing prompt.

## Commit and Review Edge Cases

- Stop before implementation review if verified implementation work is still uncommitted, unless the commit is blocked by:
  - unrelated user edits that must not be swept into the task commit
  - unresolved verification failure
  - explicit user instruction to keep the work uncommitted for now
- If reviewed implementation work intentionally remains uncommitted, say that it is an explicit exception and list the affected files.
- If `plan.md` includes commit checkpoints, treat them as optional stable boundaries. They do not replace the expectation that verified task work is committed before implementation review.

## Test Semantics Edge Cases

- Treat tests and verification as delivery checks, not as a mandatory test-first workflow.
- If relevant existing automated tests fail during the task, do not ignore them just because the task does not require adding new unit tests.
- Prefer fixing production code so existing tests keep expressing the same behavior.
- If existing tests need semantic changes because the task intentionally changes behavior, explain why and get user confirmation before changing what those tests assert.
- Small test-file repairs that preserve the original assertion intent do not need separate confirmation.
- Do not quietly weaken assertions, delete tests, or mark them skip/xfail/todo without explicit explanation and confirmation when semantics change.

## Isolation and Cleanup Edge Cases

- Do not assume the workspace is clean.
- Stay on the current branch only when the user explicitly chooses that path.
- If a worktree is specifically needed, preserve the same safety rules as the default branch-isolation path.
- Removing a worktree does not remove its task branch.

## Closing Prompt

If closing is unresolved, use this prompt shape in the repository or conversation document language:

```text
Choose the closing outcome:

1. merge and delete branch
2. merge and keep branch
3. discard work

Reply with 1, 2, or 3.
```

- Do not paraphrase this into an inline comma-separated list.
- If the user selected a merge outcome but did not separately state cleanup timing, merge first, then ask again before the destructive delete step runs.
