---
name: task-spec-execution
description: Use during migration when older prompts still refer to task-spec-execution and the task should be redirected into task-preparation or task-execution-simple.
---

# Task Spec Execution

`task-spec-execution` is deprecated and kept only as a compatibility shim during migration.

Use the split stages instead:

- `task-preparation` for concrete task entry, task-local `spec.md`, optional `plan.md`, review pauses, and routine follow-up such as committing reviewed docs
- `task-execution-simple` for branch/worktree isolation, readiness, implementation, verification, implementation review, and branch-closing hard gates

## Migration Rule

If a prompt, saved workflow, or older test still says `task-spec-execution`, do not keep the old combined flow alive by default.

Route immediately to one of these:

- Use `task-preparation` when the next work is task-local `spec.md`, optional `plan.md`, or review/commit follow-up for those docs.
- Use `task-execution-simple` when task-local docs are already ready and the next work is straightforward direct implementation.

## Expected Behavior

- Preserve the same selectable-task gate that used to protect current-task execution:
  - milestone has `Roadmap confirmed: yes`
  - previous milestone closure is resolved when crossing milestones
  - task status is `planned` or `in_progress`
  - task dependencies are satisfied or explicitly waived
  - no previous branch-closing or milestone-transition hard gate is unresolved
  - the user selected the task, or `docs/tasks/` clearly identifies it as next by order and status
- Keep review pauses and hard gates unchanged during the redirect.
- Do not use this compatibility shim to invent roadmap structure or bypass the new split stages.

## References

The task-local references still live here during migration:

- `references/spec-template.md`
- `references/plan-template.md`
- `references/task-execution-template.md`
- `references/task-execution-detailed-rules.md`

## When To Use

Use only when older prompts, installed skills, tests, or habits still call `task-spec-execution` by name and you need a compatibility redirect. Prefer using `task-preparation` or `task-execution-simple` directly in new workflows.
