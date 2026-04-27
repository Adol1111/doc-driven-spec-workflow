# Unconfirmed Milestone Continue Current Path

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the user has now explicitly chosen to keep the current milestone path.
- Proceeds with milestone-planning rather than asking the same routing question again.
- Treats the next step as milestone-entry governance plus roadmap decomposition, not task-local execution.
- Completes or proposes the milestone-entry docs update that records the routing decision before any later handoff to `task-spec-execution`. `Roadmap confirmed` stays `no` unless the user explicitly confirms the roadmap; the tasks remain provisional candidates.

## Expected File Changes

When running a file-generating check, create or propose provisional milestone-entry planning files under `tests/workflow-routing/expected/milestone-planning/unconfirmed-milestone-continue-current-path/`.

Required shape:

- `docs/tasks/team-invitations/index.md`
- `docs/tasks/team-invitations/<candidate-capability-task>/task.md`
- `docs/tasks/team-invitations/<candidate-capability-task>/task.md`

The exact number, titles, and directory slugs may vary. Accept outputs when the task files are provisional roadmap-layer candidate tasks under the current `team-invitations` milestone and the milestone remains `Roadmap confirmed: no` unless the user explicitly confirms it.

## Must Not

- Must not ask the same routing question again as if the user had not answered.
- Must not route directly to `task-spec-execution`.
- Must not write task-local `spec.md`.
- Must not start implementation.
- Must not leave the routing question unresolved after the user explicitly chose to continue on the current route. The milestone may still be unconfirmed (`Roadmap confirmed: no`) and its tasks still provisional candidates — that is the correct intermediate state until roadmap confirmation.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
