---
name: milestone-planning
description: Decomposes confirmed docs-driven direction into milestones, optional modules, and roadmap-level tasks. Use when roadmap boundaries, delivery order, or task breakdown are unclear.
---

# Milestone Planning

## Purpose

Turn a clear direction into roadmap structure. This skill owns docs governance, not task-local design.

## Use when

- planning direction is clear enough to decompose
- milestone boundaries, module grouping, or task breakdown still need decisions
- the user needs roadmap-level tasks before task-local `spec.md` work can begin

## Do not use when

- goals, constraints, or now-vs-later boundaries are still genuinely unclear
- the current task is already selected from confirmed roadmap state
- the work now is task-local spec, plan, implementation, or branch closing

## Read first

- `docs/tasks/index.md`
- `docs/tasks/planning-inbox.md`
- optional `docs/tasks/backlog.md`
- relevant milestone, module, and task docs under `docs/tasks/`
- the current user prompt

## Owns

- milestone boundaries
- optional module boundaries
- roadmap-level task decomposition
- `Roadmap confirmed` state and its consequences
- backlog and `Handoff Notes` governance
- `planning-inbox` versus `backlog` routing
- planning review pause and planning handoff context

## Must not own

- task-local `spec.md`
- task-local `plan.md`
- execution isolation or implementation
- readiness checks, verification flow, or branch closing
- implementation-level sequencing disguised as roadmap structure

## Entry checks

- If planning direction is still unresolved, route back to `planning-clarification`.
- If `Open Milestones` is empty, check `planning-inbox.md`, `backlog.md`, and prompt evidence before decomposing.
- If no evidence identifies either a concrete short-term target or roadmap misalignment, ask the planning mode question.
- If the user asks to start work inside `Roadmap confirmed: no`, keep decomposition provisional until milestone structure is explicitly confirmed.
- If the user is moving into a later milestone, resolve previous milestone closure first.

## Default flow

1. Confirm whether the current problem is roadmap structure rather than planning ambiguity.
2. Choose milestone boundaries from delivery goals, phase boundaries, or exit criteria, not feature count.
3. Add modules only when there are multiple durable capability areas with distinct ownership, risk, dependency, release, or acceptance boundaries.
4. Split roadmap tasks by coherent capability outcome. Each task should be independently reviewable, independently handoffable, and independently completable.
5. Record rationale for milestone, module, and task boundaries in roadmap docs.
6. Stop at a planning review pause after creating or reshaping roadmap docs.

## Boundary rules

- Milestone boundaries are about release or phase meaning, not about keeping milestone size visually balanced.
- Do not keep one giant milestone open just because the original request was broad. Split when there are real phase, exit, or release boundaries.
- Modules are optional. Do not create a single catch-all module for one capability area.
- Do not use tiny one-off modules as buckets for isolated tasks.
- Task boundaries must stay above implementation design. A roadmap task says what capability lands, not how code changes are sequenced.
- Do not hide multiple selectable capabilities inside vague task names such as `core`, `foundation`, `mvp`, or `polish`.
- Do not name roadmap tasks after files, endpoints, tests, migrations, or refactor slices.
- Do not split implementation, tests, docs, verification, or review follow-up into separate roadmap tasks unless that governance work is itself the user-visible delivery outcome.
- Task order belongs in the relevant ordered list, not in numeric directory prefixes.
- Newly discovered future work during an active milestone should go to that milestone's `Handoff Notes` first by default, not into task-local `plan.md`.

## Handoff Notes routing

- Record `Handoff Notes` in the current milestone `index.md`, not in task-local `plan.md`.
- Keep an item in the current milestone only when it must be completed to satisfy the current milestone's exit criteria.
- Move an item to a later milestone when it is clearly milestone-shaped future work, but not required to close the current milestone.
- Move an item to `docs/tasks/backlog.md` when it is already a recognizable roadmap item or deferred task, but not yet assigned to a milestone.
- Move an item to `docs/tasks/planning-inbox.md` when it is still a planning candidate, unresolved direction, or not yet milestone-shaped.
- Remove an item only when it is explicitly discarded or no longer worth tracking.
- If the user explicitly decides the item is high priority enough to interrupt the current path, replan it instead of leaving it as handoff-only follow-up.

## Inbox vs backlog

- `planning-inbox.md` stores unconfirmed planning candidates: ideas, goals, opportunities, or follow-up work that still needs alignment before milestone decomposition.
- `backlog.md` stores deferred roadmap items: work that is already concrete enough to keep as a known item, but is not currently attached to a milestone.
- `planning-inbox.md` is about deciding what the roadmap should become.
- `backlog.md` is about remembering roadmap work that is already shaped enough to keep, but not scheduled now.

## If blocked

- Ask the planning mode question when no evidence identifies a concrete short-term target or misalignment:
  - `Do you already have a concrete short-term target for this iteration, or do we need to realign the next stage of the roadmap first?`
- Route back to `planning-clarification` when roadmap structure still depends on unresolved goal or boundary ambiguity.
- Stop and ask directly when an unresolved item blocks milestone confirmation, milestone closure, or cross-milestone movement.

## Review and follow-up

- Stop at a planning review pause after roadmap docs change.
- Treat clear forward-motion language after that review pause as permission for routine follow-up.
- Default routine follow-up after review is:
  - commit reviewed planning docs
  - unless the user explicitly asks to leave them uncommitted
  - then report handoff context and move toward the next applicable stage
- Do not treat planning review approval as permission to skip unresolved hard gates.

## Hard gates

- Do not move into a later milestone while an earlier milestone still appears open and unresolved.
- Do not treat `continue` as milestone confirmation when the roadmap structure is still explicitly unconfirmed.
- Do not close a milestone while any `Handoff Notes` item remains unresolved.
- Do not add follow-up work to a completed milestone. Create a new open milestone or backlog item instead.

## Output

- recommended milestone structure
- why it is one milestone or several
- whether modules are needed
- task list per milestone or module
- delivery order when not obvious
- assumptions or open questions

## Stop point

- planning review pause
- or a direct blocking question about roadmap ambiguity, confirmation, or closure

## Handoff

- `Decided`
- `Undecided`
- `Next skill`
- `Stop point`

## References

- Use `references/roadmap-template.md` for roadmap document shape.
