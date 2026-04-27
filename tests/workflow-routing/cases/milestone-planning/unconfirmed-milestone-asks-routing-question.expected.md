# Unconfirmed Milestone Asks Routing Question

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the milestone has an explicit unconfirmed-roadmap flag.
- Treats that flag as the primary routing signal instead of assuming direct decomposition is already approved.
- Uses the first response to ask whether to re-evaluate milestone structure first or keep the current route and decompose tasks within it anyway.
- Waits for the user's answer before recommending milestone/task structure.

## Expected File Changes

None.

## Must Not

- Must not immediately decompose tasks under the unconfirmed milestone.
- Must not ignore the `Roadmap confirmed: no` flag.
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
