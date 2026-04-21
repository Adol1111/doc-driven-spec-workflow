# Task Execution Template

Use for selected concrete task directories after roadmap structure exists.

This template owns task-local execution metadata and links to `spec.md` and optional `plan.md`. Roadmap decomposition and milestone/module indexes belong to `milestone-planning`.

## Task Directory

```md
docs/tasks/<milestone>/<task>/
  task.md
  spec.md
  plan.md   # optional
```

If the milestone has a module layer:

```md
docs/tasks/<milestone>/<module>/<task>/
  task.md
  spec.md
  plan.md   # optional
```

## `task.md`

```md
# Task: <Short Title>

## Placement
- Milestone: `<milestone>`
- Module: `<module or None>`

## Source
- Architecture: <path or link, if relevant>
- Spec: `spec.md`, if available
- Plan: `plan.md`, if available
- Request: <short request summary>

## Dependencies
- None

## Status
- [ ] planned
- [x] in_progress
- [ ] blocked
- [ ] completed

## Checklist
- [ ] Project-level acceptance point

## Notes
- Put detailed implementation steps in task-local `plan.md` when needed.
```

If blocked by another task in the same milestone:

```md
## Dependencies
- Depends on: [01-some-task](../01-some-task/task.md)
- Reason: <why this task is blocked by that dependency>
- Parallelizable: no
```

## Rules

- A concrete task is one complete implementation round, not one implementation step.
- Keep implementation mechanics in `spec.md`, optional `plan.md`, or checklist items.
- Do not promote code review, tests, migrations, single files, or refactor slices into standalone tasks.
- Task-local `task.md` should state its `Milestone` and `Module` placement even when the path already implies it.
- Dependencies should use Markdown links to task-local `task.md`, not bare paths.
- Task-level `Depends on` should normally stay within the same milestone.
- `Status` must remain mutually exclusive.
- Mark the task `completed` only after verification, docs/status updates, commit or approved uncommitted checkpoint, and branch closing are resolved.
