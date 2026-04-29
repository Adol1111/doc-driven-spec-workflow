# Selected Task Spec Subagent Handoff Default

## Expected Skill

`task-spec-execution`

## Expected Behavior

- Recognizes that a concrete task is selected from confirmed roadmap state with no blocking dependencies or prior checkpoints.
- Routes to `task-spec-execution`.
- Recognizes that implementation is expected to move to a subagent after approval, so the compact spec should default to handoff-ready without needing an extra clarification question.
- Writes or proposes one focused task-local `spec.md`.
- Keeps the spec compact while making handoff-critical anchors concrete enough for a subagent to implement without a follow-up clarification round.
- Keeps the extra handoff detail inside the existing task-local spec sections instead of inventing a separate top-level handoff document.
- Recognizes that this small proof-oriented task has no plan trigger.
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

The spec should explicitly capture enough concrete anchors for subagent handoff:

- preferred proof samples, fixtures, or evidence sources for the key proof cases
- preferred implementation surface, ownership boundary, or first modification target
- per-case acceptance signals stating what each proof case must show to pass

## Expected File Changes

When running a file-generating check, create or propose only this task-local spec under `tests/workflow-routing/expected/task-execution/selected-task-spec-subagent-handoff-default/`:

- `docs/tasks/m1-private-beta/handoff/03-source-proof-subagent/spec.md`

## Must Not

- Must not reshape milestones or modules.
- Must not create additional roadmap tasks.
- Must not create multiple specs for the same task.
- Must not create `plan.md` for this straightforward selected task.
- Must not ask an unnecessary route-selection question once the prompt already says the spec will be handed to a subagent.
- Must not omit handoff-critical concrete anchors when the next implementation step will be delegated to a subagent.
- Must not start implementation before spec approval.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
