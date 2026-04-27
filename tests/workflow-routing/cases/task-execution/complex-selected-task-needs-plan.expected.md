# Complex Selected Task Needs Plan

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that the approved spec has multiple plan triggers: persisted format change, migration/transition behavior, public API compatibility boundary, and non-obvious verification order.
- Creates or proposes a task-local `plan.md` before implementation.
- Keeps the plan separate from `spec.md`.
- Stops for explicit plan approval before resolving the docs checkpoint or starting implementation.
- Does not treat `continue` as approval to skip the plan gate.

## Expected File Changes

When running a file-generating check, create or propose only this task-local plan under `tests/workflow-routing/expected/task-execution/complex-selected-task-needs-plan/`:

- `docs/tasks/m1-private-beta/api-compatibility/02-session-token-migration/plan.md`

## Must Not

- Must not start implementation.
- Must not create a branch or worktree before plan approval and docs checkpoint resolution.
- Must not merge plan content into `spec.md` instead of creating `plan.md`.
- Must not skip plan approval.
- Must not route to `milestone-planning` unless the task boundary itself is disputed.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
