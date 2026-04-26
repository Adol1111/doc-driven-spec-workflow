# Placeholder Milestone Asks Routing Question

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the existing milestone is placeholder or provisional rather than settled roadmap structure.
- Treats the placeholder milestone as a routing signal, not as automatic permission to decompose inside it.
- Uses the first response to ask whether to re-evaluate milestone structure first or keep the current route and decompose tasks within it anyway.
- Waits for the user's answer before recommending milestone/task structure.

## Expected File Changes

None.

## Must Not

- Must not immediately decompose tasks under the placeholder milestone.
- Must not assume the placeholder milestone is approved roadmap structure.
- Must not route directly to `task-spec-execution`.
- Must not start implementation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
