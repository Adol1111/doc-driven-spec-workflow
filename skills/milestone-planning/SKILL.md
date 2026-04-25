---
name: milestone-planning
description: Use when a request or repository needs roadmap decomposition before spec writing because milestone boundaries, module grouping, or independently reviewable tasks are unclear.
---

# Milestone Planning

Plan roadmap structure before task-local spec work begins.

This skill decides `Milestone -> optional Module -> Task` shape. It owns roadmap-layer `docs/tasks/` structure and governance, not task-local specs or implementation flow.

## Composition

- **Entry**: reached from `doc-driven-spec-workflow` after scope is clear enough to plan delivery structure.
- **Owns**: milestone boundaries, optional module grouping, roadmap-layer task breakdown, backlog/handoff governance, planning-stage `docs/tasks/` documents.
- **Does not own**: repository scaffold bootstrap, task-local `spec.md`, task-local `plan.md`, readiness checks, implementation, verification, branch closing.
- **Handoff**: use `task-spec-execution` only after the current concrete task is selected and the user wants to enter spec-first execution.

## Core Rules

### Delivery Boundary

- **Start from**: release goal, phase boundary, acceptance boundary — not feature count.
- **One milestone**: same delivery goal + same completion definition + no meaningful stage boundary.
- **Multiple milestones**: clear phase boundaries, different exit criteria, different release timing, or frozen history needed.

### Module Rules

- Modules are **optional**. Use only when a milestone has multiple durable capability areas with distinct ownership, dependency graphs, risk profiles, release boundaries, or acceptance criteria.
- Skip modules when there is only one real capability area.

### Task Rules

- One independently reviewable implementation round.
- Delivers one coherent capability outcome: implementation, tests, docs/status updates, verification.
- Keep inside the task: tests, migrations, docs updates, refactors required for the capability.

### Routing

| Situation | Action |
|-----------|--------|
| Empty `Open Milestones` | Use `brainstorming` first |
| `Roadmap confirmed: no` | Treat tasks as candidates only |
| Cross-milestone movement | Resolve previous milestone closure first |

**Planning mode question**: *"Do you already have a concrete short-term target for this iteration, or do we need to realign the next stage of the roadmap first?"*

### Mandatory Behavior

- Explain why each milestone, module, and task boundary exists. Structure without rationale is incomplete.
- Ask the planning mode question first when it is still unclear whether the user needs roadmap alignment or direct decomposition.
- Treat an empty `Open Milestones` list as a routing signal, not enough information to decompose by itself.
- Use `brainstorming` first when goals, constraints, success criteria, or roadmap alignment are still unclear.
- Skip `brainstorming` and decompose directly when the user already has a concrete short-term target.
- Treat milestone confirmation as the primary routing signal for task decomposition.
- Treat tasks inside a milestone marked `Roadmap confirmed: no` as provisional planning output, not formally selected execution work.
- Treat milestone/module/task creation or reshaping as docs governance only. It does not authorize spec writing or implementation.
- Hand off to `task-spec-execution` only after the current concrete task is chosen.

## Handoff and Closure

- `Handoff Notes`: temporary transfer queue for follow-up findings. Resolve before milestone closure.
- **Before closure**: every `Handoff Notes` item must be resolved to current-milestone open work, later milestone, `docs/tasks/backlog.md`, or removal.
- Close milestone when original exit criteria are satisfied.
- Completed milestones are frozen; add follow-up work to a new open milestone.
- If the user appears to be moving into a later milestone, resolve previous milestone closure and target milestone confirmation before decomposing or selecting work there.
- If milestone entry is still ambiguous, do not answer the routing question on the user's behalf before the user responds.

## Output Requirements

Always provide:

- Recommended milestone structure
- Why it is one milestone or several
- Whether modules are needed
- Task list per milestone or module
- Delivery order when not obvious
- Assumptions or open questions

Documents to create/update:

- `docs/tasks/index.md`
- Optional: `docs/tasks/backlog.md`
- `docs/tasks/<milestone>/index.md`
- Optional: `docs/tasks/<milestone>/<module>/index.md`
- `docs/tasks/<milestone>/<task>/task.md`

Use `references/roadmap-template.md` for exact planning-stage shape.

## Detailed Rules and Anti-Patterns

For complete mandatory rules, routing rules, and anti-patterns, see:

- [references/milestone-detailed-rules.md](./references/milestone-detailed-rules.md)
- [references/milestone-anti-patterns.md](./references/milestone-anti-patterns.md)

## When To Use

Use this skill when:

- Milestone boundaries, module grouping, or task breakdown need to be decided
- Milestones are missing, stale, or need reshaping around current goals
- The user wants a phase, iteration, or request broken into roadmap structure
- Roadmap-layer `docs/tasks/` structure must be created or reshaped before current-task spec writing
- Current delivery scope and later enhancements need an explicit stage boundary

Do not use this skill when:

- The current concrete task is already selected and only needs task-local spec or implementation governance
- The problem is implementation design within one task rather than roadmap decomposition
- The work is pure docs maintenance with no milestone or task planning need
