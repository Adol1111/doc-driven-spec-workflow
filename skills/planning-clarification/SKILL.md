---
name: planning-clarification
description: Resolves roadmap-blocking planning ambiguity before roadmap decomposition. Use when goals, constraints, success criteria, or now-vs-later boundaries are unresolved by docs or prompt evidence.
---

# Planning Clarification

## Purpose

Resolve only the ambiguity that blocks roadmap planning. Do not decompose roadmap structure here.

## Use when

- docs or prompt show real ambiguity about goals, constraints, success criteria, or now-vs-later boundaries
- roadmap decomposition cannot proceed without first choosing direction
- the next step depends on clarifying what belongs now, what belongs later, or what the first planning slice should target

## Do not use when

- missing docs are the only problem
- roadmap direction is already clear enough to decompose
- the current work is milestone decomposition, task-local design, or execution

## Read first

- `docs/tasks/index.md`
- `docs/tasks/planning-inbox.md`
- relevant `docs/tasks/` materials
- `docs/architecture/`
- `docs/context/`
- the current user prompt

## Owns

- identifying roadmap-blocking ambiguity
- asking the smallest blocking question
- making now-vs-later boundaries explicit
- recommending one clarified direction
- handing off clarified planning context

## Must not own

- milestone, module, or task decomposition
- task-local `spec.md` or `plan.md`
- implementation or execution isolation
- open-ended product discovery beyond what is needed to unblock roadmap planning

## Entry checks

- Use this skill only for positive ambiguity evidence, not for missing docs alone.
- If codebase or docs can answer a question, inspect them before asking the user.
- If the issue is already about roadmap structure rather than direction, route to `milestone-planning`.

## Default flow

1. Identify the specific ambiguity blocking roadmap planning.
2. Resolve one blocking branch at a time.
3. Ask one question at a time, with a recommended answer.
4. Make the consequence of each branch explicit: what belongs now, what belongs later, and what the next planning target becomes.
5. Once direction is clear enough for decomposition, stop and hand off to `milestone-planning`.

## Clarification rules

- Treat this as roadmap-blocking clarification, not broad product discovery.
- Keep the question surface narrow: ask only what changes roadmap direction, phase boundaries, success criteria, or first-slice scope.
- Treat a goal as a desired future state, product outcome, opportunity, or phase direction. Do not use clarification just to relabel an already concrete task-shaped item as a goal.
- If the prompt item already has a concrete outcome, rough scope, and obvious acceptance surface, hand it to `milestone-planning` for placement instead of asking abstract goal questions.
- When real alternatives exist, compare 2-3 plausible directions briefly and recommend one.
- If scope is too large for one planning pass, clarify the first coherent planning target instead of trying to settle the whole product at once.
- Do not start roadmap decomposition in the same response that finishes clarification.

## If blocked

- Ask one blocking question at a time.
- Do not stack multiple unresolved questions in one turn unless one answer depends directly on another.
- If the user has not answered the current routing question, do not answer it on their behalf.

## Review and follow-up

- Stop after clarified direction is confirmed or corrected.
- Treat clear forward-motion language after that stop as permission to move into the recommended next planning stage.
- Default follow-up is handoff to `milestone-planning`.

## Output

- current ambiguity
- next question or option set
- recommended direction
- clarified now-vs-later boundary

## Stop point

- one blocking clarification question
- or clarified-direction handoff to `milestone-planning`

## Handoff

- `Decided`
- `Undecided`
- `Next skill`
- `Stop point`
