# Roadmap No Mechanical Split

## Prompt

Use doc-driven-spec-workflow.

The docs scaffold exists. We need team invitations. Please break this into tasks: create the database table, add the API endpoint, build the form UI, write tests, update docs, and do code review.

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the requested split is too implementation-mechanical for roadmap tasks.
- Routes to `milestone-planning`.
- Keeps implementation mechanics inside independently reviewable capability tasks.
- Proposes capability-level tasks instead of tasks for database tables, API endpoints, UI components, tests, docs updates, or code review.
- Explains that tests, docs updates, schema/API/UI work, and code review belong inside the relevant implementation task.
- Stops after roadmap structure or task selection unless the user explicitly asks to continue.

## Expected File Changes

When running a file-generating check, create only these roadmap-layer files under `tests/workflow-routing/expected/roadmap-no-mechanical-split/`:

- `docs/tasks/index.md`
- `docs/tasks/team-invitations/index.md`
- `docs/tasks/team-invitations/01-invite-by-email/task.md`
- `docs/tasks/team-invitations/02-manage-pending-invitations/task.md`

## Must Not

- Must not create tasks named after implementation mechanics:
  - `create-database-table`
  - `add-api-endpoint`
  - `build-form-ui`
  - `write-tests`
  - `update-docs`
  - `code-review`
- Must not write task-local `spec.md`.
- Must not write task-local `plan.md`.
- Must not start implementation.
- Must not route directly to `task-spec-execution`.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
