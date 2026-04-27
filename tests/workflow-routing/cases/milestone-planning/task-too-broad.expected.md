# Task Too Broad

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the named task is too broad for one independently reviewable implementation round.
- Refuses to write a task-local spec until the roadmap/task shape is corrected.
- Routes to `milestone-planning`.
- Proposes splitting or reshaping the task into independently reviewable tasks.
- Explains why the current task boundary is unsafe.
- Stops after roadmap/task reshaping or task selection.

## Expected File Changes

None.

## Must Not

- Must not write a giant `spec.md` for the broad task.
- Must not start implementation.
- Must not create `plan.md`.
- Must not treat the broad task name as sufficient concrete task selection.
- Must not split by implementation mechanics such as files, endpoints, migrations, tests, or code review.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
