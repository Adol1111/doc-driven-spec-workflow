# Selected Task Spec

## Prompt

Use doc-driven-spec-workflow.

The docs scaffold exists, and `docs/tasks/m1-private-beta/authentication/01-login-session/task.md` is the selected current task. Please write the spec for this task before implementation.

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that a concrete task already exists and is selected.
- Routes to `task-spec-execution`.
- Reads or asks to read the relevant task, architecture, and context docs.
- Writes or proposes one focused task-local `spec.md`.
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

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
