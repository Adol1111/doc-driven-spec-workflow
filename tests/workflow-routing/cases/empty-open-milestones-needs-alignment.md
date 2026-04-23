# Empty Open Milestones Need Alignment

## Prompt

Use doc-driven-spec-workflow.

Our `docs/tasks/` index has no `Open Milestones` right now. We have a rough idea for an internal developer platform, but no agreed roadmap yet and people keep proposing one-off near-term work that may not fit together. Help me figure out what we should do next.

## Expected Skill

`brainstorming`

## Expected Behavior

- Recognizes that `Open Milestones` is empty because roadmap goals and phase boundaries are not aligned yet.
- Routes to `brainstorming` before roadmap decomposition.
- Frames the next step as clarifying mid/long-term goals and `now versus later` boundaries.
- Does not jump straight into milestone or task decomposition.

## Expected File Changes

None.

## Must Not

- Must not route directly to `task-spec-execution`.
- Must not start writing roadmap-layer tasks as if priorities were already aligned.
- Must not split work into implementation mechanics such as files, endpoints, tests, migrations, or code review tasks.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
