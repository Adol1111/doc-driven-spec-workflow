# Milestone Close Handoff Notes Blocked

## Expected Skill

`milestone-planning`, or `doc-driven-spec-workflow` routing back to milestone governance before closure.

## Expected Behavior

- Recognizes that milestone closure is still blocked because `Handoff Notes` is non-empty.
- Explains that `Handoff Notes` is a temporary transfer queue rather than historical residue.
- Requires the handoff item to be attached to a later milestone or backlog and removed from `M1` before closure.
- Keeps the workflow at milestone governance instead of closing `M1` immediately.

## Expected File Changes

None.

## Must Not

- Must not close `M1` while `Handoff Notes` is still non-empty.
- Must not treat the handoff note as already resolved without a recorded destination.
- Must not route directly to `task-spec-execution`.
- Must not start implementation work.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
