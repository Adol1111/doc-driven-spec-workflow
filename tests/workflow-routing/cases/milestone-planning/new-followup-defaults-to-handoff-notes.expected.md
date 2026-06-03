# New Followup Defaults To Handoff Notes

## Expected Skill

`milestone-planning`, or `doc-driven-spec-workflow` routing back to milestone governance.

## Expected Behavior

- Recognizes that the new item is a follow-up finding discovered during an active milestone rather than a fully classified backlog item.
- Defaults to recording the item in the current milestone's `Handoff Notes`.
- Explains that final placement can be decided later during milestone governance or closure.
- Keeps the workflow at milestone governance instead of selecting a task or starting execution on the new item.

## Expected File Changes

None.

## Must Not

- Must not send the item directly to `docs/tasks/backlog.md` by default while the current milestone handoff routing is still unresolved.
- Must not treat the item as already attached to a later milestone without an explicit decision.
- Must not route directly to `task-preparation`.
- Must not start implementation work.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
