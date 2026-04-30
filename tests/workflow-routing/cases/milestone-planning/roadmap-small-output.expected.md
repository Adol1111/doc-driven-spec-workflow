# Roadmap Small Output

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the request needs roadmap-level task structure, not task-local spec execution.
- Routes to `milestone-planning`.
- Keeps this as one milestone because the work shares one delivery goal and completion boundary.
- Does not create modules because the scope is too small for durable module grouping.
- Splits the work into independently reviewable capability tasks.
- Explains why each task boundary exists.
- Stops after roadmap structure or task selection unless the user explicitly asks to continue.

## Expected File Changes

When running a file-generating check, create only roadmap-layer files under `tests/workflow-routing/expected/milestone-planning/roadmap-small-output/`.

Required shape:

- `docs/tasks/index.md`
- `docs/tasks/<milestone-or-capability-slug>/index.md`
- `docs/tasks/<milestone-or-capability-slug>/<invite-by-email-task>/task.md`
- `docs/tasks/<milestone-or-capability-slug>/<manage-pending-invitations-task>/task.md`

The exact task directory slugs may vary. Accept either a neutral capability slug such as `team-invitations` or a milestone-prefixed slug such as `m1-team-invitations`, as long as the task files represent the expected capability boundaries: inviting by email, and managing pending invitations including revoke.

## Must Not

- Must not write task-local `spec.md`.
- Must not write task-local `plan.md`.
- Must not start implementation.
- Must not create modules for this small scope.
- Must not split work into implementation mechanics such as files, endpoints, migrations, tests, or code review tasks.
- Must not route directly to `task-preparation`.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
