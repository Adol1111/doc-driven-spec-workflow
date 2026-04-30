# Completed Milestone Frozen Followup

## Expected Skill

`milestone-planning`, or `doc-driven-spec-workflow` routing back to milestone governance.

## Expected Behavior

- Recognizes that completed milestones are frozen.
- Refuses to reopen `M1` or add a new task inside it.
- Routes the follow-up to milestone governance for placement in a new open milestone, backlog, or planning inbox.
- Does not select or start the follow-up as a concrete task.
- Waits for explicit placement or planning decision before task-local spec work.

## Expected File Changes

None.

## Must Not

- Must not add new work to a completed milestone.
- Must not route directly to `task-preparation`.
- Must not write task-local `spec.md`.
- Must not start implementation.
- Must not treat "start the task" as permission to bypass completed-milestone governance.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
