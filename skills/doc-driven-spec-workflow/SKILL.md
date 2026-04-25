---
name: doc-driven-spec-workflow
description: Use when a docs-driven repository request is unclear about whether the next step is scaffold initialization, clarification, roadmap decomposition, or current-task execution.
---

# Using Doc-Driven Spec Workflow

Use this root skill to select and coordinate the right docs-driven workflow skill.

This skill is the entry protocol for the workflow. It does not own bootstrap, planning, specs, plans, implementation, templates, or branch-closing details. Those belong to the stage-specific skills.

This is analogous to `using-superpowers`: it makes the agent choose and respect the right composable skill instead of improvising the whole workflow from memory.

## Mandatory Rules

- MUST start docs-driven repository work by identifying the current workflow stage.
- MUST load exactly one stage skill next unless the user explicitly asks for a comparison or audit.
- MUST delegate stage behavior to the selected skill instead of restating or bypassing that skill's rules.
- MUST treat roadmap planning and task reshaping as docs governance. They do not authorize spec writing or implementation by themselves.
- MUST stop at approval gates. `continue` is not approval for roadmap structure, spec, plan, branch closing, or destructive cleanup.
- MUST preserve handoff context when switching skills: what is decided, what is undecided, and why the next skill applies.

## Workflow Chain

Default chain:

`docs-workflow-bootstrap -> superpowers:brainstorming -> milestone-planning -> task-spec-execution`

Not every request uses every stage. Skip stages only when their decision is already settled.

## Routing Rules

Choose the next skill by the user's current uncertainty:

- "We need the minimum docs scaffold first." -> `docs-workflow-bootstrap`
- "We still do not understand what we are building." -> `superpowers:brainstorming`
- "We understand the request, but not the milestone/module/task shape." -> `milestone-planning`
- "We know the current concrete task and need spec-first execution." -> `task-spec-execution`

Use `docs-workflow-bootstrap` when the repository lacks:

- `docs/index.md`
- `docs/architecture/index.md`
- `docs/tasks/index.md`
- `docs/context/index.md`

Use `superpowers:brainstorming` when goals, constraints, success criteria, or "now versus later" boundaries are still ambiguous.

Use `milestone-planning` when the user needs milestone count, module grouping, task breakdown, delivery order, or stage boundaries.

Use `task-spec-execution` only after a concrete task exists or is selected and the user wants task-local `spec.md`, optional `plan.md`, readiness, implementation, verification, or branch closing.

Do not skip directly from ambiguous scope to spec writing.
Do not use `task-spec-execution` to invent roadmap structure.
Do not keep using `milestone-planning` after the question becomes current-task execution.

## Handoff Rules

- `docs-workflow-bootstrap -> superpowers:brainstorming or milestone-planning`: after the minimum docs scaffold exists
- `superpowers:brainstorming -> milestone-planning`: after scope, boundaries, and success criteria are clear enough to plan delivery structure
- `milestone-planning -> task-spec-execution`: after the current concrete task is selected and the user wants to enter spec-first execution

At each handoff, briefly restate:

- what has already been decided
- what remains undecided
- what the next skill is responsible for
- which explicit approval gate, if any, remains outstanding

Treat a user message such as `continue` as permission to advance to the next workflow stage only when the current stage is complete and no explicit approval gate is outstanding.

Do not treat `continue` as automatic approval for:

- roadmap structure that still needs confirmation
- spec approval
- plan approval
- branch closing or destructive cleanup decisions

## Response Shape

Keep orchestration responses compact:

1. Current stage
2. Why this stage applies
3. Next skill to use
4. Expected stop point
