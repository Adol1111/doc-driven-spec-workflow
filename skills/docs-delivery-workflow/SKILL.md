---
name: docs-delivery-workflow
description: Use when a docs-driven repository needs an overall workflow decision across bootstrap, clarification, roadmap decomposition, and current-task spec execution, especially to decide whether to use docs-workflow-bootstrap, brainstorming, milestone-planning, or doc-driven-spec-workflow next.
---

# Docs Delivery Workflow

Coordinate the overall docs-driven workflow across four stages:

`docs-workflow-bootstrap -> brainstorming -> milestone-planning -> doc-driven-spec-workflow`

This skill is an orchestrator. It decides which stage comes next and where to stop. It does not replace the stage-specific rules in the other skills.

## Mandatory Rules

- MUST choose the next stage based on the user's current uncertainty and decision need, not by loading every workflow skill at once.
- MUST use `docs-workflow-bootstrap` when the repository needs the minimum docs scaffold initialized.
- MUST use `brainstorming` first when goals, constraints, success criteria, or scope boundaries are still ambiguous.
- MUST use `milestone-planning` when the user needs roadmap decomposition: milestone count, module need, task breakdown, delivery order, or stage boundaries.
- MUST use `doc-driven-spec-workflow` only after the current concrete task is chosen and the user is ready to write or revise that task's `spec.md`, optionally `plan.md`, and then move toward implementation.
- MUST treat roadmap planning and task reshaping as docs governance. Creating or reshaping milestones, modules, tasks, or indexes does not authorize writing specs or code by itself.
- MUST stop at the end of each stage unless the user explicitly asks to continue into the next one.

## Stage Model

## 0. Bootstrap

Use `docs-workflow-bootstrap` when the repository lacks the minimum docs-driven workflow scaffold.

Typical work:

- create `docs/index.md`
- create `docs/architecture/index.md`
- create `docs/tasks/index.md`
- create `docs/context/index.md`

Stop after the scaffold is created and reported.

## 1. Clarification

Use `brainstorming` when the work is still fuzzy.

Typical signals:

- The request mixes multiple goals without clear scope
- The user is still exploring options
- Success criteria are unclear
- It is not yet clear what belongs in "now" versus "later"

Stop when the scope and intent are clear enough to plan structure.

## 2. Roadmap Decomposition

Use `milestone-planning` when the scope is clear enough, but the delivery structure is not.

Typical decisions:

- one milestone or several
- whether modules are useful
- which tasks should exist
- recommended order and dependency notes
- what belongs in the current phase versus later follow-up work

Stop when the current concrete task is selected or the roadmap docs are updated.

## 3. Current-Task Spec Execution

Use `doc-driven-spec-workflow` when the current concrete task already exists or has just been chosen.

Typical work:

- read the relevant docs
- write or revise `spec.md`
- create `plan.md` only if complexity justifies it
- run readiness checks before implementation
- implement, verify, update docs, and resolve branch closing

Stop after the current concrete task checkpoint is resolved.

## Routing Rules

Choose the next skill with this test:

- "We still do not understand what we are building." -> `brainstorming`
- "We need the minimum docs scaffold first." -> `docs-workflow-bootstrap`
- "We understand the request, but not the milestone/module/task shape." -> `milestone-planning`
- "We know the current task and need to execute it safely." -> `doc-driven-spec-workflow`

Do not skip directly from ambiguous scope to spec writing.
Do not keep using `milestone-planning` once the question is no longer about roadmap shape.
Do not use `doc-driven-spec-workflow` as the primary place to invent milestone structure.

## Handoff Rules

- `docs-workflow-bootstrap -> brainstorming or milestone-planning`: after the minimum docs scaffold exists
- `brainstorming -> milestone-planning`: after scope, boundaries, and success criteria are clear enough to plan delivery structure
- `milestone-planning -> doc-driven-spec-workflow`: after the current concrete task is selected and the user wants to enter spec-first execution

At each handoff, briefly restate:

- what has already been decided
- what remains undecided
- what the next skill is responsible for

Treat a user message such as `continue` or `继续` as permission to advance to the next workflow stage only when the current stage is complete and no explicit approval gate is outstanding.

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
