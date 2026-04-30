# Approved Spec Needs Checkpoint

## Expected Skill

`task-preparation`, potentially handing off into `task-execution-simple`

## Expected Behavior

- Recognizes that the reviewed `spec.md` can continue through the recommended operational next step without a second commit-approval question.
- Does not start implementation.
- May commit the reviewed `spec.md` as part of normal continuation.
- If it does not commit yet, it must make that choice explicit rather than asking for a redundant commit approval.
- Proceeds only to the next non-destructive preparation or execution handoff step, such as a final docs follow-up, branch/worktree isolation, or plan evaluation.

## Expected File Changes

None.

## Must Not

- Must not start implementation.
- Must not ask a second approval question whose only purpose is deciding whether to commit the already reviewed `spec.md`.
- Must not silently carry an intentionally uncommitted `spec.md` forward without reporting that choice.
- Must not create `plan.md` unless the task genuinely needs it and the user has asked for or approved that step.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
