# Milestone Detailed Rules

Detailed mandatory rules for milestone planning. See SKILL.md for core framework.

## Routing and Planning Mode

- Identify the delivery boundary before creating milestones. Start from release goal, phase boundary, and acceptance boundary, not from the number of features mentioned.
- Default to one milestone when the requested work shares one delivery goal, one completion definition, and no meaningful stage boundary.
- Split into multiple milestones when the work has clear phase boundaries, different exit criteria, different release timing, or follow-up work that should remain frozen history after an earlier stage completes.
- Treat modules as optional. Use modules only when one milestone contains multiple durable capability areas with distinct ownership, dependency graphs, risk profiles, release boundaries, or acceptance criteria.
- Treat tasks as independently reviewable implementation rounds. A task should deliver one coherent capability outcome, including implementation, tests, docs/status updates, and verification.
- Explain why each milestone, module, and task boundary exists. Output structure without rationale is incomplete.
- First determine whether the user needs roadmap alignment or decomposition of an already-defined target whenever the current situation is unclear.
- Treat an empty `Open Milestones` list as a routing signal, not enough information to decompose by itself.
- Treat milestone confirmation as the primary routing signal for task decomposition. If a milestone is explicitly unconfirmed, ask whether to re-evaluate milestone structure or continue on the current path.
- Treat tasks inside a milestone marked `Roadmap confirmed: no` as provisional candidate tasks for planning only, not as formally selected execution tasks.
- Treat cross-milestone movement as a separate governance decision from "start the next task". If the user appears to be moving from one milestone to another, first resolve whether the previous milestone should be closed and whether the next milestone path is confirmed.

## Milestone Entry and Closure

- Allow newly discovered follow-up discussion points to be recorded in the current milestone's `Handoff Notes` first when their final destination is not decided yet.
- Treat `Handoff Notes` as a temporary transfer queue. Once a handoff item is attached to a later milestone, backlog, or equivalent planning location, remove it from the current milestone.
- Treat placeholder names or other provisional milestone markers as fallback routing signals only when no explicit confirmation flag exists.
- Ask a routing question before recommending a path whenever it is still unclear whether the user needs roadmap alignment or direct decomposition.
- Treat that routing question as the required first response in ambiguous cases. Do not explain the recommended route, propose next steps, or start decomposition before the user answers.
- Use `superpowers:brainstorming` first when goals, constraints, success criteria, or roadmap alignment are still unclear. If `Open Milestones` is empty because mid/long-term goals are not aligned, use `superpowers:brainstorming` to align direction and prefer at least three milestones before detailed decomposition.
- Skip `superpowers:brainstorming` and decompose directly when the user already has a concrete short-term target, especially in enterprise or iteration-driven work with a clear case, scope, or delivery outcome.
- Hand off to `task-spec-execution` only after the current concrete task is chosen.
- Treat milestone/module/task creation or reshaping as docs governance. Updating roadmap structure does not by itself authorize spec writing or implementation.
- Close a milestone when its original exit criteria are satisfied, even if the work surfaced new follow-up findings for later milestones. Record those findings as handoff context or new roadmap items instead of keeping the finished milestone artificially open.
- Clear `Handoff Notes` before milestone closure by resolving each item into exactly one outcome: current-milestone open work, a later milestone, `docs/tasks/backlog.md`, or removal if it is no longer worth tracking.
- Remove any item kept in the current milestone from `Handoff Notes` and express it through open task state, new task creation, or `Exit Criteria` instead.
- Revisit backlog during roadmap planning and when changing `Roadmap confirmed: no` to `yes`; once an item clearly belongs to a milestone or task, attach it there and remove it from backlog.
- Keep its document output focused on roadmap structure and task selection. Task-local `spec.md`, `plan.md`, readiness, and implementation guidance belong to `task-spec-execution`.

## Document Shape Rules

- Milestone confirmation should be explicit in each milestone `Status` section. Use `Roadmap confirmed: no` for provisional placeholder milestones and flip it to `yes` when the user confirms continuing on that path.
- Starting a task in a later milestone requires two checks first: the earlier milestone is intentionally still active or explicitly closed, and the later milestone has `Roadmap confirmed: yes`.
- `Handoff Notes` is optional. Use it as a temporary transfer queue for follow-up findings discovered during the milestone while their destination is still being decided.
- Do not use `Handoff Notes` to restate open task status, explain the next task, or duplicate `Open Tasks`, `Completed Tasks`, `Goal`, or `Exit Criteria`.
- `Handoff Notes` must be empty before milestone closure. If a handoff item still exists there, the handoff is not finished.
- Before closing a milestone, resolve every `Handoff Notes` item into exactly one outcome: current-milestone open work, a later milestone, `docs/tasks/backlog.md`, or removal if it is no longer worth tracking.
- If a finding means the current milestone is not actually complete, express that through `Exit Criteria` or open task state instead of treating it as handoff-only information.
- Write `Exit Criteria` as checklist items and mark them complete before milestone closure; do not remove them after closure.
- `Open Tasks` lists only `planned`, `in_progress`, and `blocked`.
- `Completed Tasks` lists only `completed`.
- Numeric prefixes imply default order, not strict serialization.
