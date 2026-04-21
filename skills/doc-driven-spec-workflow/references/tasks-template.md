# Tasks Template

Use for current-task execution-compatible `docs/tasks/` documents: task directories, task metadata, dependencies, and milestone/module ordering after roadmap structure has been decided.

## Task Directory

```md
docs/tasks/<milestone>/<module>/<task>/
  task.md
  spec.md
  plan.md   # optional
```

If the milestone has only one real capability area, skip the module layer:

```md
docs/tasks/<milestone>/<task>/
  task.md
  spec.md
  plan.md   # optional
```

## `task.md`

```md
# Task: <Short Title>

## Placement
- Milestone: `<milestone>`
- Module: `<module>`

## Source
- Architecture: <path or link, if relevant>
- Spec: `spec.md`, if available
- Plan: `plan.md`, if available
- Request: <short request summary>

## Dependencies
- None
```

Or:

```md
## Dependencies
- Depends on: [01-some-task](../01-some-task/task.md)
- Reason: <why this task is blocked by that dependency>
- Parallelizable: no
```

Continue with:

```md
## Status
- [x] planned
- [ ] in_progress
- [ ] blocked
- [ ] completed

## Checklist
- [ ] Project-level acceptance point

## Notes
- Put detailed implementation steps in task-local `plan.md` when needed.
```

## Task Sizing Rules

- A task is one complete implementation round, not one implementation step.
- Good task size: one coherent behavior, system capability, or project outcome with its own acceptance points and verification.
- Too small: "code review", "write unit tests", "add repository file", "create migration", "update handler", "rename field", or any single-file/sub-step task.
- Too large: mixed outcomes that cannot be reviewed, verified, or shipped together.
- If the work only describes implementation mechanics or delivery verification, keep it in `spec.md`, optional `plan.md`, or checklist items.
- Split only when each piece can ship, verify, or be reviewed independently with different acceptance outcomes.
- Routine cleanup, concept clarification, link fixes, renames, formatting, index maintenance, and small docs reorganization should be inline maintenance in the current work round, not standalone tasks.
- Create a pure cleanup/governance/clarification task only when it is complex, cross-cutting, independently reviewable, or needs project-level execution tracking.

## Index Rules

Use `references/index-template.md` for milestone and module indexes.

Rules:

- `docs/tasks/index.md` lists only `Open Milestones` and `Completed Milestones`.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- Milestone indexes list modules and module progress.
- Modules should represent durable capability areas. If there is only one real capability area, skip modules and place tasks directly under the milestone.
- Module indexes list `Open Tasks` and `Completed Tasks`.
- Task-local `task.md` should state its `Milestone` and `Module` placement even when the path already implies it.
- Dependencies should use Markdown links to task-local `task.md`, not bare paths.
- Task-level `Depends on` should stay within the same milestone; document cross-milestone sequencing in milestone-level notes instead.
- `Status` must remain mutually exclusive.
- Unless the repository explicitly requires it, do not put detailed execution steps in `task.md`.
