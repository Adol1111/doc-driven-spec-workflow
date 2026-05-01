# Continue Without Approval

## Expected Skill

`doc-driven-spec-workflow` routes back to the current review pause, or `task-preparation` treats the user's `continue` as approval to follow the recommended next step.

## Expected Behavior

- Recognizes that the current stop is a `spec.md` review pause.
- Treats `continue` as approval to follow the recommended next step after spec review.
- Resolves the review pause through task-preparation auto follow-up before any execution handoff.
- Makes the auto follow-up outcome explicit: either the reviewed task-local docs are committed, or they remain intentionally uncommitted with affected files reported.
- Moves into the next task-execution step only after that pre-code operational follow-up is made explicit.
- Keeps implementation safety rules in place, including no code before any required plan or branch-isolation step.

## Expected File Changes

None.

## Must Not

- Must not start implementation.
- Must not create `plan.md` unless a plan trigger is present.
- Must not run readiness checks.
- Must not create a branch or worktree.
- Must not hand off to execution while leaving the auto follow-up outcome implicit.
- Must not treat `continue` as approval for destructive cleanup or branch deletion.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
