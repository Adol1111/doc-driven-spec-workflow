---
name: task-spec-execution
description: Use when a docs-driven repository has a selected or selectable concrete docs/tasks task and needs task-local spec or implementation governance before code changes.
---

# Task Spec Execution

Use this skill after roadmap structure exists and one concrete task is selected or ready to be selected.

## Composition

- **Entry**: reached from `doc-driven-spec-workflow` or `milestone-planning` after a concrete task exists or is selected.
- **Owns**: task-local `spec.md`, optional task-local `plan.md`, readiness checks, implementation governance, verification, docs/status updates, and branch closing.
- **Does not own**: minimum docs scaffold bootstrap, milestone boundary decisions, module grouping, roadmap-layer task creation, or planning-stage templates.
- **Handoff**: return to `doc-driven-spec-workflow` after one concrete task checkpoint and branch closing are resolved.

## Core Rules

### Spec and Plan

- **Spec**: defines behavior, scope, exclusions, and tradeoffs.
- **Plan**: defines implementation slices, file map, and verification (only when complexity justifies it).
- Do not collapse into one document.
- Default to task-local `spec.md` and optional `plan.md`; use global `docs/specs/` or `docs/plans/` only for standalone or cross-task docs.
- Do not create a new spec for pure docs governance work such as architecture edits, task/module reshaping, milestone changes, or index maintenance.
- Default to `1 task -> 1 spec`. Revise the existing spec for corrections or clarifications instead of creating another one.
- If multiple specs seem necessary, stop and use `milestone-planning` to split the task first.

### Governance Mode

| Mode | Work Type | Requires Spec |
|------|-----------|---------------|
| Docs governance | Architecture edits, task/module reshaping, milestone updates, index maintenance | No |
| Implementation governance | Code edits for concrete `docs/tasks/*` task | Yes |

- Keep pure docs governance in docs mode. It does not create implementation permission.
- Defer minimum docs scaffold initialization to `docs-workflow-bootstrap`.
- This skill may read or maintain bootstrap-created docs after they exist, but it is not the primary owner of repository scaffold initialization.
- Defer roadmap decomposition, milestone boundaries, module grouping, and task reshaping to `milestone-planning`.

### Implementation Requirements

Before code edits:
1. Spec approval
2. Plan approval (when required)
3. Branch/worktree isolation
4. Readiness checkpoint

- Do not edit implementation code for a concrete `docs/tasks/*` task until all four conditions are satisfied.
- Resolve a docs checkpoint for approved task-local docs before implementation isolation.

### Branch Isolation Rules

| Situation | Action |
|-----------|--------|
| Workspace dirty, shared, risky, or likely to conflict | Use `superpowers:using-git-worktrees` or equivalent safe worktree workflow |
| Workspace clean and isolation risk is low | Create dedicated task branch in place |
| User explicitly asks to stay on current branch | Only with explicit user choice |

Default: never start implementation on current branch. Do not carry approved-but-uncommitted task-local docs into implementation worktree by default.

### Checkpoint Flow

| Complexity | Flow |
|------------|------|
| Default | `spec -> user confirms -> docs checkpoint -> code` |
| Complex | `spec -> user confirms -> plan -> user confirms -> docs checkpoint -> code` |

- When `milestone-planning` has just created or reshaped roadmap/task docs and stopped with a docs checkpoint still unresolved, that planning checkpoint must be resolved before entering task-local `spec.md` work.
- If `milestone-planning` creates the first concrete task in a milestone, treat the resulting task docs as planning-governance output first, not as automatic permission to draft the first task spec.
- In that situation, the first user `continue` should resolve the task-planning docs checkpoint. Only after that checkpoint is resolved may a later `continue` enter task-local `spec.md` drafting.
- Hard pause at concrete task: report verification/docs updates, resolve commit or approved uncommitted checkpoint, resolve branch closing, then stop.
- Milestone completion is hard boundary: frozen after move to `Completed Milestones`.
- Crossing milestones: resolve previous milestone closure and new milestone confirmation first.
- For docs-only or governance work, stop after reporting changed files and key diffs. Do not commit unless the user asked for it up front or confirms after review.

### Branch Closing

- After completing concrete `docs/tasks/*` task, do not start another task until branch closing is resolved.
- Use `superpowers:finishing-a-development-branch` for merge/PR/keep/discard options.
- Use `superpowers:using-git-worktrees` cleanup rules for worktree cleanup.
- Removing a worktree does not remove its task branch.
- If the user chooses merge and cleanup, confirm whether cleanup includes deleting the fully merged task branch before deleting it.
- Never delete branch or worktree without confirming closing decision.
- If user asks to "continue", treat as prompt to resolve branch closing first.

## Task And Status Rules

- Use `docs/tasks/` to decide next task, not `docs/context/`.
- Do not infer new concrete task from `docs/architecture/` alone.
- If architecture implies follow-up work but `docs/tasks/` has no open task, use `milestone-planning` first.
- Tasks inside unconfirmed milestone (`Roadmap confirmed: no`) are not suitable open work.
- Respect task sizing. If too small, too broad, or only sub-step, stop and use `milestone-planning`.
- Completed milestones are frozen. Never reopen or add modules/tasks.
- Tasks fit one focused branch including implementation, tests, docs/status updates, code review, verification.
- Keep implementation steps inside `spec.md`, optional `plan.md`, or checklist items; do not promote into tasks.
- Task-level `Depends on` stays within same milestone normally. Put cross-milestone sequencing in milestone-level notes.
- Respect task dependencies exactly as written.
- Keep task status mutually exclusive: `planned`, `in_progress`, `blocked`, `completed`.
- `docs/tasks/index.md` lists `Open Milestones` and `Completed Milestones`, no modules or task counts.
- Move milestones from open to completed only when whole milestone done; no `[completed/total]`.
- Do not begin task from later milestone until previous milestone intentionally active by explicit user choice or reviewed for closure and target milestone explicitly confirmed.
- Keep milestone/module indexes accurate, do not redesign structure here.
- Each concrete task: directory with `task.md`, task-local `spec.md`, optional `plan.md`.
- `task.md` tracks status, dependencies, acceptance points; not detailed step-by-step plan.
- When all open tasks complete, report if milestone appears complete. Use `milestone-planning` before moving milestone state or adding missing work.
- Pure cleanup, concept clarification, docs governance belongs in current work round by default. Create task directory only for complex/cross-cutting governance with independent acceptance or project-level execution state; even then, do not create spec unless it drives concrete implementation.
- Use `docs/tasks/` as the only source of truth for concrete next work.
- Tasks in a milestone still marked `Roadmap confirmed: no` remain candidate tasks only until milestone entry is explicitly confirmed.
- Resolve the previous task checkpoint before starting another concrete task.
- Report milestone-entry governance changes before drafting the first task spec in that milestone.
- Reporting milestone-entry governance changes does not replace the need to resolve any outstanding task-planning docs checkpoint created by `milestone-planning`.

## Docs Boundaries

- `docs/architecture/` holds stable behavior and long-lived constraints.
- `docs/tasks/` holds roadmap state, milestone or module indexes, and concrete task directories.
- `docs/context/` holds supporting research and unstable reference material.
- Treat code as the source of truth when code and docs diverge.
- If implementation changes behavior, API shape, task status, architecture assumptions, or other documented constraints, update the relevant docs in the same round.
- If a conclusion in `docs/context/` becomes a stable system rule, move or restate it in `docs/architecture/`.

## Detailed Rules and Violations

For stop conditions, low-frequency execution details, and template-loading guidance, see [references/task-execution-detailed-rules.md](./references/task-execution-detailed-rules.md).

## Workflow

Follow this order unless the user explicitly asks for something different:

1. If the user's feature, behavior, or task intent is ambiguous, use `superpowers:brainstorming` when available, or an equivalent clarification workflow, before selecting or creating a concrete task.
2. If the main uncertainty is roadmap shape rather than current-task design, use `milestone-planning` before continuing here.
3. Read `docs/index.md` and the relevant docs index files.
4. Read the relevant `docs/architecture/` documents for behavior boundaries.
5. Read the relevant `docs/tasks/` milestone/module index plus task directory or `task.md` for order, status, and dependencies.
6. Use `docs/context/` only for supporting research or unstable reference material.
7. If there is no suitable open task because the roadmap shape itself is missing or unclear, stop and use `milestone-planning`.
8. If the next candidate task is in a new milestone, first verify that the previous milestone checkpoint is closed and the target milestone is explicitly confirmed for entry. If not, stop and resolve milestone governance first.
9. If `milestone-planning` just created or updated roadmap/task docs for the selected task and left a docs checkpoint unresolved, resolve that checkpoint before starting task-local `spec.md` work.
10. If implementing one concrete task, create or update its task directory and write one focused `spec.md` inside it.
11. Stop after writing the spec; do not code until the user explicitly confirms it in the current thread.
12. Create `plan.md` inside the task directory only for genuinely complex or multi-step work; if created, stop again for user confirmation before coding.
13. After spec approval, and after plan approval when a plan exists, resolve a docs checkpoint for the approved task-local docs before implementation isolation.
14. Before implementation edits, announce and run the readiness checkpoint.
15. Implement from the approved spec or plan, then verify, update docs/status, and resolve branch closing.
16. Stop after one concrete task. Continue only when the user explicitly asks in the current thread.
17. Add an `index.md` for every new major documentation section.

## When To Use

Use this skill when:

- The repository uses `docs/architecture`, `docs/tasks`, `docs/context`, and task-local or standalone specs/plans
- The current concrete task has been chosen or is ready to be chosen from the existing roadmap

Use `milestone-planning` first when the user is still deciding milestone/module/task structure.

Do not use for repositories without this layout.
