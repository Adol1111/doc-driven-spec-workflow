# Plan Commit Points Natural Boundaries

## Expected Skill

`task-preparation`

## Expected Behavior

- Recognizes that the approved spec has plan triggers: persisted format change, migration/transition behavior, public API compatibility boundary, and non-obvious verification order.
- Creates or proposes a task-local `plan.md` before implementation.
- Includes commit points as natural stable checkpoints based on engineering judgment, not as fixed stage numbers or one commit per section.
- Allows the number and placement of commit points to vary when each point is verified, reviewable, and reversible.
- Stops for plan review before starting implementation.

## Expected File Changes

When running a file-generating check, create or propose only this task-local plan under `tests/workflow-routing/expected/task-preparation/plan-commit-points-natural-boundaries/`:

- `docs/tasks/m1-private-beta/api-compatibility/session-token-migration/plan.md`

## Must Not

- Must not start implementation.
- Must not create a branch or worktree before plan review and any required post-review follow-up.
- Must not require a commit point after every implementation section.
- Must not hard-code commit points to specific stage numbers such as stage 3 or stage 6.
- Must not route to `milestone-planning` unless the task boundary itself is disputed.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
