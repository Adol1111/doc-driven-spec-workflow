# Roadmap No Mechanical Split

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

When running a file-generating check, create or propose only roadmap-layer planning files under `tests/workflow-routing/expected/milestone-planning/roadmap-no-mechanical-split/`.

Required shape:

- `docs/tasks/team-invitations/index.md`
- `docs/tasks/team-invitations/<capability-task>/task.md`

The exact number, titles, and directory slugs may vary when the task boundaries are capability-level and independently reviewable. A single capability task is acceptable when the prompt only establishes one coherent capability and the proposed task keeps database tables, API endpoints, UI components, tests, docs updates, and code review inside the relevant implementation task instead of making them standalone roadmap tasks.

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
