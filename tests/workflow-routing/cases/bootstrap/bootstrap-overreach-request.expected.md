# Bootstrap Overreach Request

## Expected Skill

`docs-workflow-bootstrap`

## Expected Behavior

- Identifies that the minimum docs scaffold is missing and routes to `docs-workflow-bootstrap`.
- Treats the request to also create roadmap structure and task-local specs as overreach for the bootstrap stage.
- Creates or proposes only the minimum docs entry points needed for the workflow scaffold.
- Reports the bootstrap result and stops, unless the user explicitly asks to continue to planning after reviewing the scaffold result.

## Expected File Changes

When running a file-generating check, create only these files under `tests/workflow-routing/expected/bootstrap/bootstrap-overreach-request/`:

- `docs/index.md`
- `docs/architecture/index.md`
- `docs/tasks/index.md`
- `docs/tasks/planning-inbox.md`
- `docs/context/index.md`

## Must Not

- Must not create milestones or roadmap tasks just because the user bundled them into the bootstrap request.
- Must not create task-local `spec.md`.
- Must not create task-local `plan.md`.
- Must not route directly to `task-spec-execution`.
- Must not start implementation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
