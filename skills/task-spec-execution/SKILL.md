---
name: task-spec-execution
description: Use when a docs-driven repository has a selected or selectable concrete docs/tasks task and needs task-local spec or implementation governance before code changes.
---

# Task Spec Execution

Use after roadmap structure exists and one concrete task is selected or selectable from confirmed roadmap state.

Selectable task gate:

- its milestone has `Roadmap confirmed: yes`
- previous milestone closure is resolved when crossing milestones
- task status is `planned` or `in_progress`
- task dependencies are satisfied or explicitly waived
- no previous task checkpoint, planning docs checkpoint, or branch closing gate is unresolved
- the user selected it, or `docs/tasks/` clearly identifies it as next by order and status

Owns task-local `spec.md`, optional `plan.md`, readiness, implementation governance, verification, docs/status updates, and branch closing. Does not own scaffold bootstrap or roadmap-layer planning.

## Required Gates

| Gate | Required behavior |
|------|-------------------|
| Governance mode | Docs governance changes roadmap/docs only and does not authorize code. Implementation governance requires a selected concrete task. |
| Spec | One task-local `spec.md` defines behavior, scope, exclusions, and tradeoffs. Default `1 task -> 1 spec`; revise instead of duplicating. |
| Plan | Default no `plan.md`. Create task-local `plan.md` only when a plan trigger is present. Spec and plan are separate documents. |
| Approval | Before code: spec approval, plan approval when required, branch/worktree isolation, readiness checkpoint. |
| Checkpoint | Approved docs are not checkpointed until committed or explicitly approved to remain uncommitted. |
| Branch | Default never implement on the current branch; use a worktree or dedicated task branch unless the user explicitly chooses otherwise. |
| Closing | After one concrete task, resolve implementation checkpoint and branch closing, then stop. |

Explicit approval must name the artifact or decision being approved unless the user answers a specific yes/no or either/or approval question. Vague replies such as `continue`, `ok`, `looks good`, `go ahead`, or `sure` are not approval by themselves.

## Spec and Plan

Create or update task-local docs only for concrete implementation work. Pure docs governance, such as architecture edits, task/module reshaping, milestone changes, or index maintenance, does not create an implementation spec or code permission. Defer scaffold bootstrap to `docs-workflow-bootstrap`; defer roadmap decomposition and task reshaping to `milestone-planning`.

Plan triggers:

- 3 or more major files/modules must change and modification order affects correctness
- database schema, migration, data backfill, or persisted format changes
- public API, CLI, configuration format, plugin interface, or task document format compatibility boundary
- cross-module coordination such as auth plus billing plus audit, or parser plus adapter plus renderer
- phased rollout, feature flag, migration transition, dual-write, or dual-read behavior
- non-obvious verification order
- multiple implementation slices that remain one task and should not be split by `milestone-planning`
- exploratory spike or risk-reduction step required before implementation edits

Do not create `plan.md` for a small single-capability task with straightforward implementation order. If multiple specs seem necessary, stop and use `milestone-planning` to split the task first.

Compact specs are fine; vague specs are not. When implementation intent could be misread, `spec.md` must capture work type, allowed minimal implementation, relevant non-goals or forbidden shortcuts, and where new responsibility should or must not live. Choose the spec strictness from the expected execution mode: same agent continuing in the current session may use an author-ready compact spec; another agent, subagent, model, or fresh conversation defaults to handoff-ready and must include enough concrete anchors for implementation without a clarification round. Those anchors are preferred proof samples or evidence sources, preferred implementation surface, and case-level acceptance signals. If the execution mode cannot be inferred reliably and the difference matters, ask which route the user wants before drafting. Use task-specific subheadings when helpful, but do not add top-level sections only to restate the template.

## Checkpoints and Branches

Checkpoint flow:

| Plan Trigger | Flow |
|------------|------|
| No trigger | `spec -> user confirms -> docs checkpoint -> code` |
| Trigger present | `spec -> user confirms -> plan -> user confirms -> docs checkpoint -> code` |

- A checkpoint means the workflow can safely resume in a fresh conversation without relying on chat memory.
- Content approval and checkpoint resolution are different gates: approved `spec.md` or `plan.md` is not checkpointed until it is committed or the user explicitly approves keeping it uncommitted.
- Default checkpoint resolution is to commit approved task-local docs, or verified implementation plus docs/status updates, when the user asks to resolve that checkpoint. If the user explicitly approves keeping files uncommitted, report the files and the gate satisfied.
- If plan trigger status is uncertain, name the suspected trigger and ask whether to create `plan.md` before writing it.
- When `milestone-planning` has just created or reshaped roadmap/task docs and stopped with a docs checkpoint still unresolved, that planning checkpoint must be resolved before entering task-local `spec.md` work.
- If `milestone-planning` creates the first concrete task in a milestone, the first user `continue` resolves the planning docs checkpoint; only a later `continue` may enter task-local spec drafting.
- For docs-only governance work, stop after reporting changed files and key diffs. Do not commit unless the user asked up front or confirms after review.

Branch isolation:

- Workspace dirty, shared, risky, or likely to conflict: use `superpowers:using-git-worktrees` or equivalent safe worktree workflow.
- Workspace clean and isolation risk is low: create a dedicated task branch in place.
- User explicitly asks to stay on current branch: proceed only with explicit user choice.
- Do not carry approved-but-uncommitted task-local docs into an implementation worktree by default.

Branch closing:

- Use `superpowers:finishing-a-development-branch` for merge/PR/keep/discard options.
- Use `superpowers:using-git-worktrees` cleanup rules; removing a worktree does not remove its task branch.
- Confirm before deleting any branch or worktree. If merge plus cleanup is chosen, confirm whether cleanup includes deleting the fully merged task branch.
- If user asks to "continue", treat as prompt to resolve branch closing first.

## Task And Status Rules

- Use `docs/tasks/` as the only source of truth for concrete next work, not `docs/context/` or architecture alone.
- A task file exists only as a candidate until it satisfies the selectable-task gate. Tasks in `Roadmap confirmed: no` milestones remain provisional.
- Respect task sizing, dependencies, and status exactly. If the candidate is too small, too broad, only a sub-step, or implies a missing roadmap shape, stop and use `milestone-planning`.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- Do not begin a later milestone until the previous milestone is intentionally active by explicit user choice or reviewed for closure and the target milestone is explicitly confirmed.
- Each concrete task has a directory with `task.md`, task-local `spec.md`, and optional `plan.md`; `task.md` tracks status, dependencies, and acceptance points, not detailed implementation steps.
- Keep implementation steps inside `spec.md`, optional `plan.md`, or checklist items; do not promote them into tasks.
- `docs/tasks/index.md` lists `Open Milestones`, `Completed Milestones`, and supporting planning links such as `Planning Inbox`; it does not list modules, tasks, or counts.
- When all open tasks complete, report if the milestone appears complete. Use `milestone-planning` before moving milestone state or adding missing work.
- Report milestone-entry governance changes before drafting the first task spec, and still resolve any outstanding planning docs checkpoint first.

## Docs Boundaries

`docs/architecture/` holds stable behavior and long-lived constraints; `docs/tasks/` holds roadmap state and concrete task directories; `docs/context/` holds supporting research or unstable reference. Code is source of truth when code and docs diverge. If implementation changes behavior, API shape, task status, architecture assumptions, or stable constraints, update the relevant docs in the same round. Move stable rules out of `docs/context/`.

## Detailed Rules and Violations

For stop conditions, low-frequency execution details, and template-loading guidance, see [references/task-execution-detailed-rules.md](./references/task-execution-detailed-rules.md).

## Workflow

Follow this order unless the user explicitly asks for something different:

1. If docs or prompt evidence shows task intent is ambiguous, use `superpowers:brainstorming`; do not infer ambiguity from missing docs alone.
2. If the uncertainty is roadmap shape, use `milestone-planning`.
3. Read `docs/index.md`, relevant docs indexes, relevant `docs/architecture/`, and the relevant `docs/tasks/` milestone/module/task docs. Use `docs/context/` only for supporting research or unstable reference.
4. If no suitable open task exists, or the next task is blocked by milestone closure/confirmation or a planning docs checkpoint, stop and resolve that governance first.
5. Write or update one focused task-local `spec.md`, then stop for explicit approval.
6. Check plan triggers. If present, write task-local `plan.md` and stop for explicit approval; if uncertain, ask before writing.
7. Resolve the approved docs checkpoint, isolate branch/worktree, run readiness, implement, verify, update docs/status, resolve implementation checkpoint and branch closing, then stop.
8. Add an `index.md` for every new major documentation section.

## When To Use

Use when the repository has the docs-driven layout and the current concrete task is selected or ready to select from confirmed roadmap state. Use `milestone-planning` first when milestone/module/task structure is still being decided. Do not use for repositories without this layout.
