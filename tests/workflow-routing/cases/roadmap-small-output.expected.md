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

When running a file-generating check, create only these roadmap-layer files under `tests/workflow-routing/expected/roadmap-small-output/`:

- `docs/tasks/index.md`
- `docs/tasks/team-invitations/index.md`
- `docs/tasks/team-invitations/01-invite-by-email/task.md`
- `docs/tasks/team-invitations/02-manage-pending-invitations/task.md`

## Must Not

- Must not write task-local `spec.md`.
- Must not write task-local `plan.md`.
- Must not start implementation.
- Must not create modules for this small scope.
- Must not split work into implementation mechanics such as files, endpoints, migrations, tests, or code review tasks.
- Must not route directly to `task-spec-execution`.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
