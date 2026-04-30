# Selected Task Spec Handoff Ready

## Expected Skill

`task-preparation`

## Expected Behavior

- Recognizes that a concrete task is selected from confirmed roadmap state with no blocking dependencies or prior checkpoints.
- Routes to `task-preparation`.
- Writes or proposes one focused task-local `spec.md`.
- Keeps the spec compact while treating explicit handoff readiness as an additional clarity requirement, not as a reason to create `plan.md`.
- Makes the spec concrete enough for another agent to implement without a follow-up clarification round.
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

The spec should explicitly capture enough concrete anchors for handoff:

- preferred proof samples, fixtures, or evidence sources for the key proof cases
- preferred implementation surface, ownership boundary, or first modification target
- per-case acceptance signals stating what each proof case must show to pass

These details may live inside existing sections such as `Option Selection`, `Design`, and `Testing and Verification`; a new top-level handoff section is optional and not required.

## Expected File Changes

When running a file-generating check, create or propose only this task-local spec under `tests/workflow-routing/expected/task-execution/selected-task-spec-handoff-ready/`:

- `docs/tasks/m1-private-beta/handoff/02-source-eligibility-proof/spec.md`

## Must Not

- Must not reshape milestones or modules.
- Must not create additional roadmap tasks.
- Must not create multiple specs for the same task.
- Must not create `plan.md` for this straightforward selected task.
- Must not treat "compact" as permission to omit handoff-critical concrete anchors once the prompt explicitly asks for direct handoff readiness.
- Must not defer sample selection, implementation surface, or case-level pass signals to a later clarification round.
- Must not start implementation before spec approval.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
