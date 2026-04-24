# Cross-Milestone Transition Requires Closure

## Prompt

Use doc-driven-spec-workflow.

`docs/tasks/index.md` still lists `M1` under `Open Milestones`. Inside `M1`, all concrete tasks are already marked completed. `docs/tasks/m2/index.md` exists, already contains `01`, and its status section still says `Roadmap confirmed: no`. The user now says:

start the next task

## Expected Skill

`milestone-planning`, or `doc-driven-spec-workflow` routing back to milestone governance before task execution.

## Expected Behavior

- Recognizes that this is not just a "pick the next task" request because the workflow is crossing from `M1` to `M2`.
- Recognizes that `M1` still appears open and should be reviewed for closure before moving on.
- Recognizes that `M2` is still explicitly unconfirmed because it says `Roadmap confirmed: no`.
- Uses the first response to hold at milestone governance and ask whether to close `M1` and confirm entry into `M2` before selecting a task there.
- Waits for the user's answer before selecting `M2/01` or starting task-local spec work.

## Expected File Changes

None.

## Must Not

- Must not immediately select `M2/01` as the next task.
- Must not treat "start the next task" as automatic permission to cross into the next milestone.
- Must not route directly to `task-spec-execution`.
- Must not start implementation.
- Must not skip milestone closure review for `M1`.
- Must not ignore the `Roadmap confirmed: no` flag on `M2`.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
