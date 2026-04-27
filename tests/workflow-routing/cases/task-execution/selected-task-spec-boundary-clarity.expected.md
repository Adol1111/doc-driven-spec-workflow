# Selected Task Spec Boundary Clarity

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that a concrete task is selected from confirmed roadmap state with no blocking dependencies or prior checkpoints.
- Routes to `task-spec-execution`.
- Writes or proposes one compact task-local `spec.md`.
- Makes clear that compact does not mean vague: the spec preserves implementation intent by naming boundary decisions and forbidden inference paths.
- Treats the task as boundary definition/proof work, not as permission to introduce default runtime classification behavior.
- Stops for explicit user approval before implementation.

## Expected Output Shape

The generated `spec.md` should follow the local task spec template shape:

- `# <Task Name> Design`
- `## Background`
- `## Goals`
- `## Non-goals`
- `## Option Selection`
- `## Design`
- `## Error Handling`
- `## Testing and Verification`
- `## Docs Updates`

The `## Design` section should include task-specific boundary detail, such as `### Boundary Decisions` or `### Implementation Boundary`, but the exact subsection heading is not mandatory.

The spec should explicitly capture:

- the work type: boundary definition/proof, not default runtime classification
- the allowed minimal implementation
- forbidden shortcuts, including inference from `sourceKind`, inference from `outputMode`, and helper defaults added only for test convenience
- where classification information or responsibility is allowed to live, and where it must not leak
- verification that the forbidden shortcuts were not introduced

## Expected File Changes

When running a file-generating check, create or propose only this task-local spec under `tests/workflow-routing/expected/task-execution/selected-task-spec-boundary-clarity/`:

- `docs/tasks/m1-private-beta/handoff/01-source-eligibility-boundary/spec.md`

## Must Not

- Must not reshape milestones or modules.
- Must not create additional roadmap tasks.
- Must not start implementation before spec approval.
- Must not introduce default runtime classification rules.
- Must not infer eligibility from `sourceKind`.
- Must not infer adapter responsibility from `outputMode`.
- Must not add helper defaults only to make tests easier.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
