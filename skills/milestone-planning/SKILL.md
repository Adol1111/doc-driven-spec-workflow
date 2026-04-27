---
name: milestone-planning
description: Use when a request or repository needs roadmap decomposition before spec writing because milestone boundaries, module grouping, or independently reviewable tasks are unclear.
---

# Milestone Planning

Plan roadmap structure before task-local spec work. This skill owns `Milestone -> optional Module -> Task` docs governance, not task-local specs or implementation.

## Composition

- **Entry**: reached from `doc-driven-spec-workflow` after scope is clear enough to plan delivery structure.
- **Owns**: milestone boundaries, optional module grouping, roadmap-layer task breakdown, backlog/handoff governance, planning-stage `docs/tasks/` documents.
- **Does not own**: repository scaffold bootstrap, task-local `spec.md`, task-local `plan.md`, readiness checks, implementation, verification, branch closing.
- **Handoff**: stop at a planning docs checkpoint after roadmap/task docs change; use `task-spec-execution` only after that checkpoint is resolved, the current concrete task is selected from confirmed roadmap state, and the user wants to enter spec-first execution.

## Core Rules

| Boundary | Rule |
|----------|------|
| Milestone | Start from release goal, phase boundary, or acceptance boundary, not feature count. Use one milestone for the same delivery goal plus same completion definition and no meaningful stage boundary; split when phase boundaries, exit criteria, release timing, or frozen history differ. |
| Module | Optional. Use only for multiple durable capability areas with distinct ownership, dependency graphs, risk profiles, release boundaries, or acceptance criteria. |
| Task | One independently reviewable implementation round delivering one coherent capability outcome, including required tests, migrations, docs/status updates, refactors, and verification. When the user asks for roadmap-level tasks so a first implementation task can be chosen, prefer user-visible or operator-visible capability boundaries; do not hide multiple independently selectable capabilities inside a vague `core`, `MVP`, `foundation`, or `polish` task. |

### Routing

| Situation | Action |
|-----------|--------|
| Empty `Open Milestones` and no docs/prompt evidence gives a concrete target or roadmap misalignment | Ask the planning mode question first |
| Empty `Open Milestones` and docs/prompt evidence gives a concrete short-term target | Decompose directly with `milestone-planning` |
| Empty `Open Milestones` and docs/prompt evidence says roadmap direction, goals, or phase boundaries are not aligned | Use `superpowers:brainstorming` first |
| `Roadmap confirmed: no` and user asks to decompose or start work | Ask whether to re-evaluate milestone structure or continue on the current milestone path; keep tasks provisional |
| Cross-milestone movement | Resolve previous milestone closure first |

**Planning mode question**: *"Do you already have a concrete short-term target for this iteration, or do we need to realign the next stage of the roadmap first?"*

### Mandatory Behavior

- Explain why each milestone, module, and task boundary exists. Structure without rationale is incomplete.
- Empty `Open Milestones` is a routing signal, not enough information to decompose by itself. Check `docs/tasks/planning-inbox.md`, `docs/tasks/backlog.md`, relevant task docs, and the prompt before choosing a path.
- Ask the planning mode question when no evidence identifies either a concrete short-term target or roadmap misalignment.
- Use `superpowers:brainstorming` first only when docs or prompt evidence says goals, constraints, success criteria, roadmap direction, or phase boundaries are not aligned.
- Decompose directly when the user already has a concrete short-term target.
- Treat milestone confirmation as the primary routing signal. Tasks in `Roadmap confirmed: no` milestones are provisional planning output, not formally selected execution work.
- Treat milestone/module/task creation or reshaping as docs governance only. It does not authorize spec writing or implementation.
- Stop at a planning docs checkpoint after creating or reshaping roadmap/task docs. Default checkpoint resolution is to commit those docs when the user asks to resolve the checkpoint; the user may explicitly approve keeping them uncommitted.
- Hand off to `task-spec-execution` only after the planning docs checkpoint is resolved and the current concrete task is chosen from confirmed roadmap state.

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
