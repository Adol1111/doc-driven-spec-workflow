# Selected Task Spec

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that a concrete task is selected from confirmed roadmap state with no blocking dependencies or prior checkpoints.
- Routes to `task-spec-execution`.
- Uses the selected task and provided workflow context as the basis for the simulated spec output.
- Does not require extra document reads in this isolated simulated case when the prompt already provides the task selection, milestone confirmation, dependency, and checkpoint state.
- Writes or proposes one focused task-local `spec.md`.
- Keeps compact specs precise and follows the local task spec template. Case-specific boundary decisions or forbidden shortcuts are required only when they are present in the prompt, task docs, architecture docs, context docs, or the loaded template guidance.
- Recognizes that this simple single-capability task has no plan trigger.
- Stops for explicit user approval before implementation.
- Does not create `plan.md` before or alongside the spec.

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

The `## Design` section may use task-specific subheadings. Boundary-oriented design detail is required only when the prompt, task docs, architecture docs, context docs, or loaded template guidance make a boundary decision relevant to the task.

## Expected File Changes

When running a file-generating check, create or propose only this task-local spec under `tests/workflow-routing/expected/task-execution/selected-task-spec/`:

- `docs/tasks/m1-private-beta/authentication/01-login-session/spec.md`

## Must Not

- Must not reshape milestones or modules.
- Must not create additional roadmap tasks.
- Must not create multiple specs for the same task.
- Must not create `plan.md` for this straightforward selected task.
- Must not start implementation before spec approval.
- Must not run readiness checks before spec approval.
- Must not create a branch or worktree before implementation approval.
- Must not treat a short spec as permission to omit the local template sections or task-specific non-goals needed to preserve task intent.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
