---
name: doc-driven-spec-workflow
description: Use when a docs-driven repository request is unclear about whether the next step is scaffold initialization, clarification, roadmap decomposition, or current-task execution.
---

# Using Doc-Driven Spec Workflow

Use this root skill only to select and coordinate the next docs-driven stage. Stage-specific skills own bootstrap, planning, specs, plans, implementation, templates, and branch closing.

## Mandatory Rules

- MUST start docs-driven repository work by identifying the current workflow stage.
- MUST load exactly one stage skill next unless the user explicitly asks for a comparison or audit.
- MUST delegate stage behavior to the selected skill instead of restating or bypassing that skill's rules.
- MUST treat roadmap planning and task reshaping as docs governance. They do not authorize spec writing or implementation by themselves.
- MUST require explicit approval to name the artifact or decision being approved unless the user is answering a specific yes/no or either/or approval question.
- MUST stop at approval gates. `continue`, `ok`, `looks good`, `go ahead`, or `sure` are not approval for roadmap structure, spec, plan, docs checkpoints, branch closing, or destructive cleanup.
- MUST preserve handoff context when switching skills: what is decided, what is undecided, and why the next skill applies.

## Routing Rules

Default chain: `docs-workflow-bootstrap -> superpowers:brainstorming -> milestone-planning -> task-spec-execution`. Skip stages only when their decision is already settled.

Choose the next skill by the user's current uncertainty:

| Current uncertainty | Next skill |
|---------------------|------------|
| Minimum docs scaffold is missing | `docs-workflow-bootstrap` |
| Goals, constraints, success criteria, or "now versus later" boundaries are unresolved by docs or prompt evidence | `superpowers:brainstorming` |
| Milestone count, module grouping, task breakdown, delivery order, or stage boundaries are unclear | `milestone-planning` |
| A concrete task is selected or selectable from confirmed roadmap state | `task-spec-execution` |

Use `docs-workflow-bootstrap` when any minimum scaffold file is missing: `docs/index.md`, `docs/architecture/index.md`, `docs/tasks/index.md`, `docs/tasks/planning-inbox.md`, or `docs/context/index.md`.

Use `superpowers:brainstorming` for positive ambiguity evidence only. Missing or stale docs alone route to bootstrap or planning.

Use `task-spec-execution` only when the task milestone has `Roadmap confirmed: yes`, previous milestone closure is resolved when crossing milestones, status is `planned` or `in_progress`, dependencies are satisfied or waived, no prior checkpoint or branch closing gate is unresolved, and the user selected it or `docs/tasks/` clearly identifies it as next by order/status.

Do not skip from ambiguous scope to spec writing, use task execution to invent roadmap structure, or keep planning after the question is current-task execution.

## Handoff Rules

- Bootstrap -> brainstorming or planning: minimum docs scaffold exists.
- Brainstorming -> planning: scope, boundaries, and success criteria are clear enough to plan delivery structure.
- Planning -> task execution: selected concrete task is in confirmed roadmap state, dependencies and prior checkpoints are clear, and the user wants spec-first execution.

At each handoff, briefly restate:

- what has already been decided
- what remains undecided
- what the next skill is responsible for
- which explicit approval gate, if any, remains outstanding

Treat a user message such as `continue` as permission to advance to the next workflow stage only when the current stage is complete and no explicit approval gate is outstanding.

## Response Shape

Keep orchestration responses compact: current stage, why it applies, next skill, and expected stop point.
