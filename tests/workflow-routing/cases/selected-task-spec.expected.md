# Selected Task Spec

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that a concrete task already exists and is selected.
- Routes to `task-spec-execution`.
- Reads or asks to read the relevant task, architecture, and context docs.
- Writes or proposes one focused task-local `spec.md`.
- Keeps compact specs precise: when implementation intent could be misread, the spec calls out the relevant boundary decisions, allowed minimal implementation, and forbidden inference paths instead of leaving them implicit.
- Stops for explicit user approval before implementation.
- Creates `plan.md` only if complexity genuinely justifies it, and only after spec approval.

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

The `## Design` section may use task-specific subheadings. For ambiguous tasks, it should include boundary-oriented design detail, such as `### Boundary Decisions` or `### Implementation Boundary`, without requiring that exact heading for every task.

## Expected File Changes

When running a file-generating check, create or propose only this task-local spec under `tests/workflow-routing/expected/selected-task-spec/`:

- `docs/tasks/m1-private-beta/authentication/01-login-session/spec.md`

## Must Not

- Must not reshape milestones or modules.
- Must not create additional roadmap tasks.
- Must not create multiple specs for the same task.
- Must not start implementation before spec approval.
- Must not run readiness checks before spec approval.
- Must not create a branch or worktree before implementation approval.
- Must not treat a short spec as permission to omit non-goals, boundaries, or forbidden implementation shortcuts that are necessary to preserve task intent.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
