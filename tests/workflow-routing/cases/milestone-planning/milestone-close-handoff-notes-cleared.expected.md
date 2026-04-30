# Milestone Close Handoff Notes Cleared

## Expected Skill

`milestone-planning`, or `doc-driven-spec-workflow` routing to milestone closure governance.

## Expected Behavior

- Recognizes that milestone closure is now allowed because the milestone's own work is done and `Handoff Notes` is empty.
- Treats the previously moved follow-up findings as no longer blocking `M1`.
- Proceeds with milestone closure governance, such as moving `M1` from `Open Milestones` to `Completed Milestones`.
- Does not reopen task decomposition or task execution unnecessarily.

## Expected File Changes

When running a file-generating check, create or propose only these milestone-closure governance files under `tests/workflow-routing/expected/milestone-planning/milestone-close-handoff-notes-cleared/`:

- `docs/tasks/index.md`
- `docs/tasks/m1/index.md`

## Must Not

- Must not block closure just because follow-up work exists elsewhere now.
- Must not require historical handoff residue to stay in `M1`.
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
