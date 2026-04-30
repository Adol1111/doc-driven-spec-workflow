# Complex Selected Task Needs Plan

## Expected Skill

`task-preparation`

## Expected Behavior

- Recognizes that the approved spec has multiple plan triggers: persisted format change, migration/transition behavior, public API compatibility boundary, and non-obvious verification order.
- Creates or proposes a task-local `plan.md` before implementation.
- Keeps the plan separate from `spec.md`.
- Stops for plan review before starting implementation.
- If the user later says `continue`, that should count as approval to follow the recommended post-review next step.

## Expected File Changes

When running a file-generating check, create or propose only this task-local plan under `tests/workflow-routing/expected/task-preparation/complex-selected-task-needs-plan/`:

- `docs/tasks/m1-private-beta/api-compatibility/02-session-token-migration/plan.md`

## Must Not

- Must not start implementation.
- Must not create a branch or worktree before plan review and any required post-review follow-up.
- Must not merge plan content into `spec.md` instead of creating `plan.md`.
- Must not skip plan review.
- Must not route to `milestone-planning` unless the task boundary itself is disputed.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
