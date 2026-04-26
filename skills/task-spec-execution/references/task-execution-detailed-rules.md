# Task Spec Execution Detailed Rules

Low-frequency execution details and stop conditions for task spec execution. Read this when the main `SKILL.md` leaves a concrete execution edge case unresolved.

## Violations That Require Stopping Immediately

- Coding before branch/worktree isolation.
- Skipping the checkpoint because a change seems small.
- Inferring a task directly from architecture instead of using `milestone-planning` to add or select it in `docs/tasks/`.
- Creating standalone tasks for routine cleanup, concept clarification, link fixes, renames, formatting, index maintenance, or small docs reorganization that should be handled in the current work round.
- Splitting implementation or delivery verification into separate tasks, such as "code review", "write unit tests", "add repository file", "update handler", or "write migration" when they belong to one coherent implementation round.
- Creating tiny modules as buckets for one-off tasks, or one catch-all module when tasks should live directly under the milestone.
- Adding cross-milestone task-level `Depends on` links when the milestone order already expresses the dependency.
- Creating a task-local spec or plan in global `docs/specs/` or `docs/plans/` by default.
- Creating multiple specs for one task instead of revising the existing spec or splitting the task first.
- Adding work to a completed milestone.
- Auto-committing docs-only/governance changes before reporting the result or before user commit confirmation.
- Starting task-local `spec.md` work while a task-planning docs checkpoint from `milestone-planning` is still unresolved.
- Starting another task before resolving branch closing for the current task.
- Starting a task in milestone `M(n+1)` while `M(n)` still appears open and unclosed, or while the target milestone is still explicitly unconfirmed.
- Assuming the workspace is clean or staying on the current branch without explicit user choice.

## Execution Details

- Do not default to TDD, plan-driven execution, or heavyweight shared workflows unless the user explicitly asks.
- Write task-local specs/plans directly in this repository's compact local format.
- Treat tests and verification as delivery checks, not as a mandatory test-first workflow.
- If `milestone-planning` just created the selected task or reshaped its roadmap docs, treat the next stop as a planning docs checkpoint first.
- In that state, a user `continue` should advance the unresolved planning checkpoint, not jump straight into `spec.md`, `plan.md`, or implementation.
- After the planning checkpoint is resolved, the next `continue` may begin drafting task-local `spec.md`.

- If a worktree is needed, prefer `superpowers:using-git-worktrees`; if it is unavailable, use the environment's equivalent git worktree workflow and preserve the same safety checks.
- Before the first implementation edit, tell the user: `Spec/plan is approved and checkpointed. I am handling branch isolation now before coding.`

## Task And Status Rules

- If architecture implies follow-up work but `docs/tasks/` has no corresponding open task, use `milestone-planning` or an equivalent roadmap update flow before creating a spec.
- Modules are optional durable capability areas owned by roadmap planning. Respect the selected task's existing milestone/module placement; if placement seems wrong, stop and use `milestone-planning`.
- Keep implementation steps inside `spec.md`, optional `plan.md`, or checklist items; do not promote them into tasks.
- Task-level `Depends on` should normally stay within the same milestone. Put cross-milestone sequencing in milestone-level `Notes`, `Exit Criteria`, or roadmap text; if future task details depend on an earlier milestone, keep them as roadmap text or milestone-level `planned`.
- Respect task dependencies exactly as written.
- Keep milestone/module indexes accurate, but do not redesign their structure here.
- `task.md` tracks status, dependencies, and acceptance points; it should not become a detailed step-by-step implementation plan.
- Pure cleanup, concept clarification, or docs governance belongs in the current work round by default. Create a task directory only for complex/cross-cutting governance or clarification with independent acceptance or project-level execution state; even then, do not create a spec unless it drives concrete implementation.

## Templates And Workflow

Load only the relevant reference:

- `docs/architecture/`: `references/architecture-template.md`
- `docs/context/`: `references/context-template.md`
- non-roadmap docs indexes: `references/index-template.md`
- selected task directory or `task.md`: `references/task-execution-template.md`
- task-local `spec.md`: `references/spec-template.md`
- task-local `plan.md`: `references/plan-template.md`

Do not load every template by default.
Do not use these references as the default planning-stage output for milestone decomposition.
