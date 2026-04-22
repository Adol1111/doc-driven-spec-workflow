# Branch Closing After Worktree

## Prompt

Use doc-driven-spec-workflow.

The selected task implementation is complete. Verification passed, docs/status updates are done, and the task commit was merged back to `main`. The task worktree has been removed, but the merged task branch still exists. The user now says:

continue

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that branch closing is still unresolved because deleting a worktree does not delete the merged task branch.
- Does not start another task.
- Does not treat `continue` as permission to skip branch closing.
- Asks whether to delete the merged task branch or keep it for review/history.
- Explains that branch deletion requires explicit confirmation unless the prior closing decision already included branch deletion.
- Keeps the workflow at the branch closing gate.

## Expected File Changes

None.

## Must Not

- Must not start another task.
- Must not write a new task-local `spec.md`.
- Must not write `plan.md`.
- Must not run implementation readiness checks.
- Must not silently leave branch closing unresolved.
- Must not delete the merged branch without explicit confirmation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
