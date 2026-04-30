# Selected Task Skip Spec And Code

## Expected Skill

`task-preparation`

## Expected Behavior

- Recognizes that a concrete task exists, so this is an execution-stage request.
- Refuses to skip task-local spec work for a concrete implementation task.
- Holds the workflow at task-local spec creation or spec review instead of moving into implementation.
- Explains that rough agreement is not the same as task-local spec approval.

## Expected File Changes

None.

## Must Not

- Must not start implementation.
- Must not create a branch or worktree.
- Must not run readiness checks.
- Must not treat the user's urgency or confidence as spec approval.
- Must not skip directly to `plan.md` unless the spec exists and the task genuinely needs a plan.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
