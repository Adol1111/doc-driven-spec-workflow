# Milestone Close Handoff Notes Gate

## Scenario A - Blocked By Nonempty Handoff Notes

### Prompt

Use doc-driven-spec-workflow.

`M1` has finished all of its concrete tasks and its original `Exit Criteria` are satisfied. The user wants to close `M1`. However, `docs/tasks/m1/index.md` still contains:

```md
## Handoff Notes
- Follow-up rate limiting work still needs to be attached to `M2` or backlog.
```

The user now says:

close M1

### Expected Skill

`milestone-planning`, or `doc-driven-spec-workflow` routing back to milestone governance before closure.

### Expected Behavior

- Recognizes that milestone closure is still blocked because `Handoff Notes` is non-empty.
- Explains that `Handoff Notes` is a temporary transfer queue rather than historical residue.
- Requires the handoff item to be attached to a later milestone or backlog and removed from `M1` before closure.
- Keeps the workflow at milestone governance instead of closing `M1` immediately.

### Expected File Changes

None.

### Must Not

- Must not close `M1` while `Handoff Notes` is still non-empty.
- Must not treat the handoff note as already resolved without a recorded destination.
- Must not route directly to `task-spec-execution`.
- Must not start implementation work.

## Scenario B - Allowed After Handoff Notes Clear

### Prompt

Use doc-driven-spec-workflow.

`M1` has finished all of its concrete tasks, its original `Exit Criteria` are satisfied, and `docs/tasks/m1/index.md` no longer has any pending handoff items because they were already moved into `M2` and backlog. The `Handoff Notes` section is now empty. The user now says:

close M1

### Expected Skill

`milestone-planning`, or `doc-driven-spec-workflow` routing to milestone closure governance.

### Expected Behavior

- Recognizes that milestone closure is now allowed because the milestone's own work is done and `Handoff Notes` is empty.
- Treats the previously moved follow-up findings as no longer blocking `M1`.
- Proceeds with milestone closure governance, such as moving `M1` from `Open Milestones` to `Completed Milestones`.
- Does not reopen task decomposition or task execution unnecessarily.

### Expected File Changes

None.

### Must Not

- Must not block closure just because follow-up work exists elsewhere now.
- Must not require historical handoff residue to stay in `M1`.
- Must not route directly to `task-spec-execution`.
- Must not start implementation work.

## Self-Check

```text
Scenario: A/B
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
