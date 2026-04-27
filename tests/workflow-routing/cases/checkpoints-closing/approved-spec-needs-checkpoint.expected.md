# Approved Spec Needs Checkpoint

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that approved task-local docs still need a docs checkpoint before implementation isolation.
- Does not start implementation.
- Does not create a branch or worktree yet.
- Asks to resolve the approved docs checkpoint first, with commit as the default action unless the user explicitly approves keeping the docs uncommitted.
- Keeps the workflow at the pre-implementation checkpoint gate.

## Expected File Changes

None.

## Must Not

- Must not start implementation.
- Must not create a branch or worktree before the approved docs checkpoint is resolved.
- Must not treat `continue` as permission to carry an approved-but-uncommitted `spec.md` into implementation isolation.
- Must not create `plan.md` unless the task genuinely needs it and the user has asked for or approved that step.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
