# Bootstrap Needed

## Expected Skill

`docs-workflow-bootstrap`

## Expected Behavior

- Identifies that the minimum docs scaffold is missing.
- Routes to `docs-workflow-bootstrap`.
- Creates or proposes only the minimum docs entry points:
  - `docs/index.md`
  - `docs/architecture/index.md`
  - `docs/tasks/index.md`
  - `docs/context/index.md`
- Treats bootstrap as docs governance, not implementation permission.
- Stops after reporting the bootstrap result unless the user explicitly asks to continue.

## Expected File Changes

When running a file-generating check, create only these files under `tests/workflow-routing/expected/bootstrap-needed/`:

- `docs/index.md`
- `docs/architecture/index.md`
- `docs/tasks/index.md`
- `docs/context/index.md`

## Must Not

- Must not create milestones unless the user supplies actual roadmap content.
- Must not create implementation tasks.
- Must not create task-local `spec.md`.
- Must not create task-local `plan.md`.
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
