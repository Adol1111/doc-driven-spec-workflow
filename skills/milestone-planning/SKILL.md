---
name: milestone-planning
description: Use when a request or repository needs roadmap decomposition before spec writing because milestone boundaries, module grouping, or independently reviewable tasks are unclear.
---

# Milestone Planning

Plan roadmap structure before task-local spec work begins.

This skill is for deciding `Milestone -> optional Module -> Task` shape, not for writing implementation specs, using execution-side templates, or managing implementation execution. It helps keep task tracking aligned with delivery phases instead of topic lists or engineering sub-steps.

## Composition

- Entry: normally reached from `doc-driven-spec-workflow` after scope is clear enough to plan delivery structure.
- Owns: milestone boundaries, optional module grouping, roadmap-layer task breakdown, task order, dependency notes, and planning-stage `docs/tasks/` documents.
- Does not own: repository scaffold bootstrap, task-local `spec.md`, task-local `plan.md`, readiness checks, implementation, verification, or branch closing.
- Handoff: use `task-spec-execution` only after the current concrete task is selected and the user wants to enter spec-first execution.

## Mandatory Rules

- MUST identify the delivery boundary before creating milestones. Start from release goal, phase boundary, and acceptance boundary, not from the number of features mentioned.
- MUST default to one milestone when the requested work shares one delivery goal, one completion definition, and no meaningful stage boundary.
- MUST split into multiple milestones when the work has clear phase boundaries, different exit criteria, different release timing, or follow-up work that should remain frozen history after an earlier stage completes.
- MUST treat modules as optional. Use modules only when one milestone contains multiple durable capability areas with distinct ownership, dependency graphs, risk profiles, release boundaries, or acceptance criteria.
- MUST treat tasks as independently reviewable implementation rounds. A task should deliver one coherent capability outcome, including implementation, tests, docs/status updates, and verification.
- MUST NOT create tasks for implementation mechanics such as single files, API endpoints, tests, migrations, refactors, code review, or docs updates when they belong inside one implementation round.
- MUST explain why each milestone, module, and task boundary exists. Output structure without rationale is incomplete.
- MUST first determine whether the user needs roadmap alignment or decomposition of an already-defined target whenever the current situation is unclear.
- MUST treat an empty `Open Milestones` list as a routing signal, not enough information to decompose by itself.
- MUST use `brainstorming` first when goals, constraints, success criteria, or roadmap alignment are still unclear. If `Open Milestones` is empty because mid/long-term goals are not aligned, use `brainstorming` to align direction and prefer at least three milestones before detailed decomposition.
- MUST skip `brainstorming` and decompose directly when the user already has a concrete short-term target, especially in enterprise or iteration-driven work with a clear case, scope, or delivery outcome.
- MUST hand off to `task-spec-execution` only after the current concrete task is chosen.
- MUST treat milestone/module/task creation or reshaping as docs governance. Updating roadmap structure does not by itself authorize spec writing or implementation.
- MUST keep its document output focused on roadmap structure and task selection. Task-local `spec.md`, `plan.md`, readiness, and implementation guidance belong to `task-spec-execution`.

## When To Use

Use this skill when:

- milestone boundaries, module grouping, or task breakdown need to be decided
- milestones are missing, stale, or need to be reshaped around current goals
- the user wants a phase, iteration, or request broken into roadmap structure
- a roadmap-layer `docs/tasks/` structure must be created or reshaped before current-task spec writing
- current delivery scope and later enhancements need an explicit stage boundary

Do not use this skill when:

- the current concrete task is already selected and only needs task-local spec or implementation governance
- the problem is implementation design within one task rather than roadmap decomposition
- the work is pure docs maintenance with no milestone or task planning need

## Core Model

- `Milestone`: a delivery phase with its own completion meaning and frozen history boundary
- `Module`: an optional capability-area grouping inside one milestone
- `Task`: one independently reviewable implementation round

Quick test:

- one project phase -> `Milestone`
- one capability area inside that phase -> `Module`
- one complete implementation round inside that area -> `Task`

## Decomposition Workflow

Follow this order:

1. Choose planning mode: roadmap alignment or direct decomposition
2. Clarify the delivery frame
3. Find milestone boundaries
4. Decide whether modules add navigational value
5. Split tasks by independently reviewable capability outcome
6. Validate against anti-patterns
7. Output the structure with rationale and recommended order
8. Stop after planning unless the user explicitly asks to update docs or hand off to current-task spec execution

## 1. Choose The Planning Mode

Ask which mode applies before decomposing:

- `roadmap alignment`: `Open Milestones` is empty or unclear, no agreed mid/long-term outcome exists, or a single short-term goal may conflict with later phases
- `direct decomposition`: the target is already concrete and the user wants this phase or iteration broken into milestones, modules, or tasks

If the answer is unclear, ask directly instead of inferring from an empty `Open Milestones` list alone.

Route like this:

- `roadmap alignment` -> use `brainstorming` first, align direction, and prefer at least three milestones before detailed decomposition
- `direct decomposition` -> stay in `milestone-planning` and decompose the current phase or iteration

Typical `direct decomposition` signals:

- enterprise delivery with a named case, customer ask, contract scope, or fixed near-term objective
- a team already knows what this iteration must ship
- the user wants task breakdown more than product-direction alignment

## 2. Clarify The Delivery Frame

Establish these before creating structure:

- What is being delivered now versus later
- Whether the batch is one release, one program increment, or a multi-phase roadmap
- What counts as "done" for this round
- Which parts are hard dependencies versus optional follow-up work
- Whether any item has a different owner, rollout timing, or risk profile

If these are still unclear, use `brainstorming` first instead of forcing milestones.

## 3. Milestone Decision Rules

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

## 4. Module Decision Rules

Inside one milestone, skip modules when there is only one real capability area.

Create modules only when the milestone contains multiple durable capability areas and the grouping will remain useful across several tasks. A good module usually has at least three likely tasks unless it has a distinct:

- domain
- owner
- dependency graph
- release boundary
- risk profile
- acceptance boundary

Avoid modules that are only temporary buckets or one-off categories.

## 5. Task Decision Rules

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

## 6. Anti-Patterns

Stop and reshape if the output looks like any of these:

- One giant milestone containing multiple future phases only because the product request was broad
- Several tiny milestones that are really just ordered tasks
- Only one milestone created from an otherwise open-ended product request without first aligning the longer roadmap
- One fake module inside a milestone that has only one real capability area
- Tasks named after files, endpoints, tests, migrations, or refactor slices
- Task dependencies carrying phase sequencing that should be expressed as milestone order

## 7. Output Requirements

Always provide:

- recommended milestone structure
- why it is one milestone or several
- whether modules are needed
- task list per milestone or module
- recommended order
- dependency notes
- assumptions or open questions

If the repository already uses `docs/tasks/`, update or propose roadmap-layer docs only:

- `docs/tasks/index.md`
- `docs/tasks/<milestone>/index.md`
- optional `docs/tasks/<milestone>/<module>/index.md`
- `docs/tasks/<milestone>/<task>/task.md`

Use `references/roadmap-template.md` for the exact planning-stage shape and section layout.

Do not write `spec.md` or `plan.md` here unless the user explicitly asks to continue into current-task spec execution.
Do not use `task-spec-execution` execution-side templates as the default output format for this stage.

Keep this stage focused on planning-ready task metadata and roadmap navigation, not task-local design, implementation slices, or readiness instructions.

## Related Skills

- `doc-driven-spec-workflow`: use when the main question is which stage of the docs-driven workflow comes next
- `brainstorming`: use as the upstream alignment step when planning mode shows decomposition should not start yet
- `task-spec-execution`: use after the current concrete task is selected and the user wants to write or update the task spec

## Response Shape

Prefer a compact structure:

1. Delivery frame
2. Recommended milestone layout
3. Rationale
4. Task breakdown
5. Open questions or assumptions

If the user asks for docs updates, write the roadmap structure first and stop before spec creation unless they explicitly ask to continue.
