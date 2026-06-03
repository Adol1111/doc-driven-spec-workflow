---
name: docs-workflow-bootstrap
description: Creates the minimum docs-driven workflow scaffold for a repository. Use when the repository is missing core workflow entry-point docs.
---

# Docs Workflow Bootstrap

## Purpose

Create the minimum workflow scaffold so later stages have authoritative docs to read.

## Use when

- one or more minimum scaffold files are missing
- the repository has not been initialized for this docs-driven workflow
- later stages cannot recover state because the basic docs entry points do not exist yet

## Do not use when

- the minimum scaffold already exists
- the current work is roadmap decomposition, task-local design, or execution
- the user wants implementation tasks, specs, plans, or code changes during bootstrap

## Read first

- existing `docs/` files, if any
- repository doc language cues, if any
- the current user prompt

## Owns

- minimum scaffold detection
- creation of the minimum workflow entry-point docs
- compact planning-inbox goal capture only when explicitly requested during bootstrap
- bootstrap review pause and handoff suggestion

## Must not own

- milestone decomposition
- implementation task creation
- task-local `spec.md` or `plan.md`
- implementation or branch workflow
- overfilling scaffold docs with roadmap or execution detail

## Entry checks

Create only these files when missing:

- `docs/index.md`
- `docs/architecture/index.md`
- `docs/tasks/index.md`
- `docs/tasks/planning-inbox.md`
- `docs/tasks/backlog.md`
- `docs/context/index.md`

Use repository doc language rules when available. Otherwise follow the current user language.

## Default flow

1. Detect which minimum scaffold files are missing.
2. Create only the missing workflow entry points.
3. Keep content minimal and navigational.
4. If the user explicitly asks to preserve roadmap-like input during bootstrap, record it only as compact planning-inbox goal context.
5. Stop at a bootstrap review pause after reporting created or changed files.

## Boundary rules

- Bootstrap is docs governance only.
- Do not create milestones, modules, tasks, `spec.md`, `plan.md`, `docs/specs/`, or `docs/plans/` by default.
- Do not turn broad user requirements into task breakdown during bootstrap.
- `planning-inbox.md` may capture compact goal context, but it is not milestone decomposition.
- Keep scaffold docs small enough that later stages can reshape them without cleanup work.

## If blocked

- If the minimum scaffold exists but the next stage is unclear, hand off back to `doc-driven-spec-workflow`.
- If the user asks for roadmap planning during bootstrap, finish the minimal scaffold first, then suggest `milestone-planning`.
- If the user asks for concrete task execution during bootstrap, do not skip directly there unless the repository already has confirmed roadmap state.

## Review and follow-up

- Stop at a bootstrap review pause after reporting created or changed files.
- Treat clear forward-motion language after that review pause as permission for routine follow-up.
- Default follow-up after review is:
  - commit reviewed scaffold docs
  - unless the user explicitly asks to leave them uncommitted
  - then return to `doc-driven-spec-workflow` so routing can choose the next stage
- Continue directly to another stage only when the user explicitly asks for that path.

## Output

- created files
- changed files
- preserved planning-inbox goal context, if any
- recommended next skill

## Stop point

- bootstrap review pause

## Handoff

- `Decided`
- `Undecided`
- `Next skill`
- `Stop point`

## References

- Use `references/scaffold-template.md` for minimum scaffold document shape.
