---
name: planning-clarification
description: Clarifies ambiguous planning direction before roadmap decomposition by resolving goals, scope, stage boundaries, and first roadmap slice direction. Use when goals, constraints, success criteria, or now-versus-later boundaries are unresolved.
---

# Planning Clarification

## Quick start

Use this skill when docs or prompt show real ambiguity about direction, not just missing docs. Expand options first, then converge on a recommended direction.

## Workflows

1. Explore current evidence first: `docs/tasks/`, `docs/architecture/`, `docs/context/`, recent task docs, current prompt.
2. If codebase can answer a question, inspect code/docs instead of asking user.
3. Ask one question at a time until goals, constraints, success criteria, and now-vs-later boundaries are clear.
4. Expand option space before narrowing it: compare at least 2-3 plausible scope, stage, or sequencing directions when direction is still open.
5. Prefer short options with a recommendation.
6. Make stage boundaries explicit: what belongs now, what belongs later, and what first coherent roadmap slice direction should be.
7. If scope is too large for one planning pass, split it into smaller planning targets before recommending roadmap decomposition.
8. Present recommended direction and ask user to confirm or correct it.
9. After direction is confirmed, state handoff context in this shape: `Decided`, `Undecided`, `Next skill`, `Stop point`.
10. Stop before roadmap decomposition, spec writing, or implementation.
11. Hand off to `milestone-planning` when direction is clear enough to shape delivery.

## Mandatory rules

- Missing docs alone do not trigger this skill.
- Do not decompose milestones, write task-local `spec.md`, or implement code here.
- Treat this as a hard gate before downstream planning when direction is still ambiguous.
- Direction clarification here must include divergence, not only requirement collection.
- Clarify `now vs later`, phase boundaries, and first roadmap slice direction before handoff.
- Do not perform roadmap structure design here; `milestone-planning` owns milestone/module/task decomposition.
- Stop after direction is confirmed and handoff context is stated. Do not start roadmap decomposition in the same response.
- If scope is too large for one planning pass, help split it into smaller planning targets first.
- Keep output compact: current ambiguity, next question or options, recommendation, `Decided`, `Undecided`, `Next skill`, `Stop point`.

## Advanced features

Downstream handoff target is usually `milestone-planning` once direction is clear enough to shape delivery.
