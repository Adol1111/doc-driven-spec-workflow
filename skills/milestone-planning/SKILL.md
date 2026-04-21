---
name: milestone-planning
description: Use when a request or repository needs roadmap decomposition before spec writing because milestone boundaries, module grouping, or independently reviewable tasks are unclear.
---

# Milestone Planning

Plan roadmap structure before task-local spec work begins.

This skill is for deciding `Milestone -> optional Module -> Task` shape, not for writing implementation specs, using execution-side templates, or managing implementation execution. It helps keep task tracking aligned with delivery phases instead of topic lists or engineering sub-steps.

## Mandatory Rules

- MUST identify the delivery boundary before creating milestones. Start from release goal, phase boundary, and acceptance boundary, not from the number of features mentioned.
- MUST default to one milestone when the requested work shares one delivery goal, one completion definition, and no meaningful stage boundary.
- MUST split into multiple milestones when the work has clear phase boundaries, different exit criteria, different release timing, or follow-up work that should remain frozen history after an earlier stage completes.
- MUST treat modules as optional. Use modules only when one milestone contains multiple durable capability areas with distinct ownership, dependency graphs, risk profiles, release boundaries, or acceptance criteria.
- MUST treat tasks as independently reviewable implementation rounds. A task should deliver one coherent capability outcome, including implementation, tests, docs/status updates, and verification.
- MUST NOT create tasks for implementation mechanics such as single files, API endpoints, tests, migrations, refactors, code review, or docs updates when they belong inside one implementation round.
- MUST explain why each milestone, module, and task boundary exists. Output structure without rationale is incomplete.
- MUST use `brainstorming` first when the request is still ambiguous about goals, constraints, or success criteria.
- MUST hand off to `task-spec-execution` only after the current concrete task is chosen.
- MUST treat milestone/module/task creation or reshaping as docs governance. Updating roadmap structure does not by itself authorize spec writing or implementation.
- MUST keep its document output focused on roadmap structure and task selection. Task-local `spec.md`, `plan.md`, readiness, and implementation guidance belong to `task-spec-execution`.

## When To Use

Use this skill when:

- A product or business request contains several features and the roadmap shape is unclear
- The user asks whether work should be one milestone or several
- The user wants to break a phase into milestones, modules, and tasks
- A repository already uses `docs/tasks/`, but the task structure needs to be created or reshaped before current-task spec writing
- A request mixes current delivery scope with later enhancements, and the stage boundary needs to be made explicit

Do not use this skill when:

- The current concrete task is already selected and only needs task-local spec or implementation governance
- The problem is implementation design within one task rather than roadmap decomposition
- The work is pure docs maintenance with no milestone or task planning need

## Core Model

- `Milestone`: a delivery phase with its own completion meaning and frozen history boundary
- `Module`: an optional capability-area grouping inside one milestone
- `Task`: one independently reviewable implementation round

Use this test:

- If the work completes one phase of the project, it may be a milestone.
- If the work is one capability area inside that phase, it may be a module.
- If the work is one complete implementation round inside that area, it is a task.

## Decomposition Workflow

Follow this order:

1. Clarify the delivery frame
2. Find milestone boundaries
3. Decide whether modules add navigational value
4. Split tasks by independently reviewable capability outcome
5. Validate the decomposition against anti-patterns
6. Output the structure with rationale and recommended order
7. Stop after planning unless the user explicitly asks to update docs or hand off to current-task spec execution

## 1. Clarify The Delivery Frame

Establish these before creating structure:

- What is being delivered now versus later
- Whether the batch is one release, one program increment, or a multi-phase roadmap
- What counts as "done" for this round
- Which parts are hard dependencies versus optional follow-up work
- Whether any item has a different owner, rollout timing, or risk profile

If these are still unclear, use `brainstorming` first instead of forcing milestones.

## 2. Milestone Decision Rules

Default to one milestone when most answers are "yes":

- Same delivery goal
- Same completion definition
- Same release window or business checkpoint
- Same risk and review boundary
- No meaningful "finish this phase, then decide the next phase" break

Split into multiple milestones when one or more of these are true:

- There is a clear `foundation -> product capability -> enhancement/governance` sequence
- Later work should not block declaring the earlier phase complete
- The later group has different success criteria or different stakeholders
- The earlier phase should become frozen history once complete
- The work would otherwise create many cross-task dependencies that are really phase sequencing

Do not split milestones just because:

- Several features were mentioned in one conversation
- The topic list is long
- Different components or files are involved
- The implementation has multiple steps but still belongs to one delivery phase

## 3. Module Decision Rules

Inside one milestone, skip modules when there is only one real capability area.

Create modules only when the milestone contains multiple durable capability areas and the grouping will remain useful across several tasks. A good module usually has at least three likely tasks unless it has a distinct:

- domain
- owner
- dependency graph
- release boundary
- risk profile
- acceptance boundary

Avoid modules that are only temporary buckets or one-off categories.

## 4. Task Decision Rules

A task should be one coherent implementation round that can be reviewed and accepted on its own.

Good task boundaries usually have:

- one primary user-visible behavior or system capability
- one clear acceptance outcome
- one focused branch worth of work
- internal implementation steps that belong together

Keep these inside the task instead of splitting them out:

- tests
- migrations
- docs/status updates
- refactors required for the capability
- handler, API, UI, and persistence edits that together deliver the same outcome

Split tasks only when the parts can ship, verify, or be rejected independently with different acceptance outcomes.

## 5. Anti-Patterns

Stop and reshape if the output looks like any of these:

- One giant milestone containing multiple future phases only because the product request was broad
- Several tiny milestones that are really just ordered tasks
- One fake module inside a milestone that has only one real capability area
- Tasks named after files, endpoints, tests, migrations, or refactor slices
- Task dependencies carrying phase sequencing that should be expressed as milestone order

## 6. Output Requirements

Always provide:

- recommended milestone structure
- why it is one milestone or several
- whether modules are needed
- task list per milestone or module
- recommended order
- dependency notes
- assumptions or open questions

If the repository already uses `docs/tasks/`, prefer updating or proposing roadmap-layer docs only:

- `docs/tasks/index.md`
- `docs/tasks/<milestone>/index.md`
- optional `docs/tasks/<milestone>/<module>/index.md`
- `docs/tasks/<milestone>/<task>/task.md`

When writing these files, load `references/roadmap-template.md` for the exact planning-stage document shape.

Do not write `spec.md` or `plan.md` here unless the user explicitly asks to continue into current-task spec execution.
Do not use `task-spec-execution` execution-side templates as the default output format for this stage.

When writing docs in this stage, prefer a compact planning-side output shape:

- `docs/tasks/index.md`
  - `Open Milestones`
  - `Completed Milestones`
- `docs/tasks/<milestone>/index.md`
  - `Goal`
  - `Exit Criteria`
  - `Modules` or `Tasks`
  - `Status`
  - `Current Gaps`
  - `Notes`
- `docs/tasks/<milestone>/<module>/index.md`, if modules exist
  - `Goals`
  - `Recommended Order`
  - `Dependency Notes`
  - `Open Tasks`
  - `Completed Tasks`
- `docs/tasks/<milestone>/<task>/task.md`
  - `Placement`
  - `Source`
  - `Dependencies`
  - `Status`
  - `Checklist`
  - `Notes`

Keep this stage focused on planning-ready task metadata and roadmap navigation.
Do not expand into task-local design, implementation slices, or readiness instructions.

## Composition With Other Skills

- `doc-driven-spec-workflow`: use when the main question is which stage of the docs-driven workflow comes next
- `brainstorming`: use first when the request is still fuzzy or the product scope needs clarification
- `task-spec-execution`: use after the current concrete task is selected and the user wants to write or update the task spec

Recommended chain:

`doc-driven-spec-workflow -> brainstorming -> milestone-planning -> task-spec-execution`

Skip `brainstorming` when the scope is already well-defined and the user only needs decomposition.

## Response Shape

Prefer a compact structure:

1. Delivery frame
2. Recommended milestone layout
3. Rationale
4. Task breakdown
5. Open questions or assumptions

If the user asks for docs updates, write the roadmap structure first and stop before spec creation unless they explicitly ask to continue.
