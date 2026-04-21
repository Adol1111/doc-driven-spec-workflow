---
name: doc-driven-spec-workflow
description: Use when working in a repository organized around docs/architecture, docs/tasks, docs/context, and task-local or standalone specs/plans, and task execution must stay aligned with repository docs.
---

# Doc-Driven Spec Workflow

## Mandatory Rules

These are requirements, not suggestions. If any rule below is not satisfied, the work is blocked until it is satisfied.

- MUST NOT edit implementation code for a concrete `docs/tasks/*` task until spec approval, plan approval when required, branch/worktree isolation, and the readiness checkpoint are complete.
- MUST keep pure docs governance in docs mode. Architecture edits, task/module reshaping, milestone updates, and index maintenance do not create implementation permission and do not require a new spec by default.
- MUST treat routine cleanup and concept clarification as inline maintenance, not standalone tasks. Create a pure cleanup/governance/clarification task only when it is complex, cross-cutting, independently reviewable, or needs project-level execution tracking.
- MUST use `docs/tasks/` as the only source of truth for concrete next work; if no open milestone/module/task exists, update `docs/tasks/` before writing a spec.
- MUST size tasks as complete implementation rounds that deliver user-visible behavior, system capability, or a coherent project outcome. NEVER create a task for code review, a single test, single file edit, refactor step, migration file, or other implementation/verification sub-step.
- MUST treat the module layer as optional. Use `Milestone -> tasks` when a milestone has only one real capability area; use `Milestone -> modules -> tasks` only when multiple meaningful capability areas exist.
- MUST treat completed milestones as frozen history. NEVER reopen them or add modules/tasks to them; put follow-up work in a new open milestone.
- MUST resolve the previous task checkpoint before starting another concrete task. Default action is commit; uncommitted checkpoints require explicit user approval.
- MUST NOT treat checkpoint rules as permission to auto-commit newly made docs-only/governance changes. Report the diff/result first; commit only when the user explicitly asked for commit upfront or confirms after review.
- MUST resolve branch closing after completing a concrete task: verification, docs/status updates, commit or approved uncommitted checkpoint, and branch closing decision.

Spec creation requirements:

- MUST NOT create a new spec for pure docs governance work: architecture docs, task/module reshaping, milestone changes, or index maintenance.
- MUST default to `1 task -> 1 spec` for concrete implementation tracking.
- MUST place concrete task specs and plans inside the task directory by default: `docs/tasks/<milestone>/<module>/<task>/task.md`, `spec.md`, and optional `plan.md`.
- MUST use global `docs/specs/` or `docs/plans/` only for standalone or cross-task documents that do not belong to one concrete task.
- MUST revise the existing spec for that task instead of creating a second spec for corrections or clarifications.
- MUST split the task in `docs/tasks/` first if multiple specs seem necessary. NEVER silently create multiple specs for one task.

Violations that require stopping immediately:

- Coding before branch/worktree isolation.
- Skipping the checkpoint because a change seems small.
- Inferring a task directly from architecture without adding it to `docs/tasks/`.
- Creating standalone tasks for routine cleanup, concept clarification, link fixes, renames, formatting, index maintenance, or small docs reorganization that should be handled in the current work round.
- Splitting implementation or delivery verification into separate tasks, such as "code review", "write unit tests", "add repository file", "update handler", or "write migration" when they belong to one coherent implementation round.
- Creating tiny modules as buckets for one-off tasks, or one catch-all module when tasks should live directly under the milestone.
- Adding cross-milestone task-level `Depends on` links when the milestone order already expresses the dependency.
- Creating a task-local spec or plan in global `docs/specs/` or `docs/plans/` by default.
- Creating multiple specs for one task instead of revising the existing spec or splitting the task first.
- Adding work to a completed milestone.
- Auto-committing docs-only/governance changes before reporting the result or before user commit confirmation.
- Starting another task before resolving branch closing for the current task.
- Assuming the workspace is clean or staying on the current branch without explicit user choice.

## When To Use

Use this skill when the repository uses `docs/architecture`, `docs/tasks`, `docs/context`, and task-local or standalone specs/plans, and task selection, design, status, or code changes must stay aligned with those docs. Do not use it for repositories without this layout.

## Docs Roles

- `docs/architecture/`: stable behavior and long-lived constraints
- `docs/tasks/`: milestone roadmap, optional module grouping, task order/dependencies/status, and task directories for complete implementation rounds
- `docs/context/`: supporting research only
- task-local `spec.md`: one current-task design per concrete task by default
- task-local `plan.md`: optional implementation plan for genuinely complex concrete tasks
- `docs/specs/`: standalone or cross-task design docs only
- `docs/plans/`: standalone or cross-task execution plans only

Task ownership: `docs/tasks/index.md` lists only open/completed milestones; milestone indexes list modules/progress when modules exist; module or milestone indexes list open/completed task directories, order, and dependencies; task-local `task.md` tracks source, status, dependencies, and acceptance points.

## Templates And Workflow

Load only the relevant reference:

- `docs/architecture/`: `references/architecture-template.md`
- `docs/tasks/`: `references/tasks-template.md`
- `docs/context/`: `references/context-template.md`
- `docs/*/index.md`: `references/index-template.md`
- task-local `spec.md`: `references/spec-template.md`
- task-local `plan.md`: `references/plan-template.md`

Do not load every template by default.

Follow this order unless the user explicitly asks for something different:

1. Read `docs/index.md` and the relevant docs index files.
2. Read the relevant `docs/architecture/` documents for behavior boundaries.
3. Read the relevant `docs/tasks/` milestone/module index plus task directory or `task.md` for order, status, and dependencies.
4. Use `docs/context/` only for supporting research or unstable reference material.
5. If there is no suitable open task, update `docs/tasks/` before creating a spec.
6. If implementing one concrete task, create or update its task directory and write one focused `spec.md` inside it.
7. Stop after writing the spec; do not code until the user explicitly confirms it in the current thread.
8. Create `plan.md` inside the task directory only for genuinely complex or multi-step work; if created, stop again for user confirmation before coding.
9. Before implementation edits, announce and run the readiness checkpoint.
10. Implement from the approved spec or plan, then verify, update docs/status, and resolve branch closing.
11. Stop after one concrete task. Continue only when the user explicitly asks in the current thread.
12. Add an `index.md` for every new major documentation section.

## Execution Rules

- Default flow: `spec -> user confirms -> code`
- Complex flow: `spec -> user confirms -> plan -> user confirms -> code`
- Do not default to TDD, plan-driven execution, or heavyweight shared workflows unless the user explicitly asks.
- Write task-local specs/plans directly in this repository's compact local format.
- Treat tests and verification as delivery checks, not as a mandatory test-first workflow.
- A concrete task is a hard pause point: report verification/docs updates, resolve commit or approved uncommitted checkpoint, resolve branch closing, then stop.
- Milestone completion is a hard boundary: once moved to `Completed Milestones`, it is frozen; follow-up work belongs in a new open milestone.
- For docs-only/governance work, stop after reporting changed files and key diffs. Do not commit unless the user already asked for commit/sync in the same request or confirms after seeing the result.

## Branch Closing Rules

- After completing a concrete `docs/tasks/*` task, do not start another task until branch closing is resolved.
- If work happened on a task branch, ask whether to merge/delete, keep for review, or leave committed but unmerged.
- If work happened in a worktree, follow `using-git-worktrees` cleanup and merge rules when that skill is available; otherwise follow an equivalent safe worktree cleanup process.
- Never delete a branch or worktree without confirming the closing decision.
- If the user asks to continue, treat that as a prompt to resolve branch closing first, not permission to skip it.

## Spec, Plan, And Readiness

- Spec defines behavior, scope, exclusions, and tradeoffs.
- Plan defines implementation slices, file map, and verification only when complexity justifies it.
- Do not collapse them into one document.
- Use local compact templates; if shared plan-writing guidance conflicts, prefer the local template.
- For concrete tasks, default paths are task-local `spec.md` and optional `plan.md`; use global `docs/specs/` or `docs/plans/` only for standalone or cross-task docs.

Run this checkpoint after spec confirmation, and after plan confirmation when a plan exists:

- Resolve previous task checkpoint first: commit by default, or keep uncommitted only with explicit user approval.
- Confirm permission to code: current-thread spec approval, and plan approval when a plan exists.
- If this is a concrete `docs/tasks/*` implementation round, branch isolation is mandatory before code edits.

| Situation | Required action |
| --- | --- |
| Workspace is dirty, shared, already risky, or likely to conflict | Use `using-git-worktrees` when available, or an equivalent safe worktree workflow |
| Workspace is clean and isolation risk is low | Create a dedicated task branch in place |
| User explicitly asks to stay on the current branch | You may stay, but only because the user explicitly chose that |

- Never start implementation for a concrete task on the current branch by default.
- If a worktree is needed, prefer `using-git-worktrees`; if it is unavailable, use the environment's equivalent git worktree workflow and preserve the same safety checks.
- Before the first implementation edit, tell the user: `Spec/plan is approved. I am handling branch isolation now before coding.`

## Task And Status Rules

- Use `docs/tasks/` to decide the next task, not `docs/context/`.
- Do not infer a new concrete implementation task from `docs/architecture/` alone.
- If architecture implies follow-up work but `docs/tasks/` has no corresponding open task, update `docs/tasks/` first.
- Modules are optional durable capability areas. Use them only for navigational value; if a milestone has one real capability area, place task directories directly under the milestone. Merge modules with fewer than three likely tasks unless they have distinct domain, ownership, dependency graph, release boundary, risk profile, or acceptance criteria.
- Tasks should fit one focused branch while including implementation, tests, docs/status updates, code review, and verification. Split only when pieces can ship, verify, or be reviewed independently with different acceptance outcomes.
- Keep implementation steps inside `spec.md`, optional `plan.md`, or checklist items; do not promote them into tasks.
- Task-level `Depends on` should normally stay within the same milestone. Put cross-milestone sequencing in milestone-level `Notes`, `Exit Criteria`, or roadmap text; if future task details depend on an earlier milestone, keep them as roadmap text or milestone-level `planned`.
- Respect task dependencies exactly as written.
- Keep task status mutually exclusive: `planned`, `in_progress`, `blocked`, `completed`.
- `docs/tasks/index.md` lists only `Open Milestones` and `Completed Milestones`, with no modules or task counts.
- Move milestones from open to completed only when the whole milestone is done; do not use milestone `[completed/total]`.
- Milestone indexes list modules/progress when modules exist; module or milestone indexes keep `Open Tasks` and `Completed Tasks` accurate.
- Each concrete task should be a directory containing `task.md`, task-local `spec.md`, and optional `plan.md`.
- `task.md` tracks status, dependencies, and acceptance points; it should not become a detailed step-by-step implementation plan.
- When all current open tasks are complete, decide whether the current milestone is complete; if yes, move it to completed and continue in a new open milestone; if no, add missing module/task under the open milestone before creating any spec.
- Pure cleanup, concept clarification, or docs governance belongs in the current work round by default. Create a task directory only for complex/cross-cutting governance or clarification with independent acceptance or project-level execution state; even then, do not create a spec unless it drives concrete implementation.

If you need the exact task-file or module-index shape, read `references/tasks-template.md`.

## Source Of Truth Rules

- Treat code as the source of truth when code and docs diverge.
- If implementation changes behavior, API shape, task status, architecture assumptions, or other documented constraints, update the relevant docs in the same round.
- If a conclusion in `docs/context/` becomes a stable system rule, move or restate it in `docs/architecture/`.
