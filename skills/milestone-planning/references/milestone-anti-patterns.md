# Milestone Anti-Patterns

Stop and reshape if the output looks like any of these.

## Milestone Anti-Patterns

- One giant milestone containing multiple future phases only because the product request was broad
- Several tiny milestones that are really just ordered tasks
- Only one milestone created from an otherwise open-ended product request without first aligning the longer roadmap
- A milestone kept open only because it discovered follow-up work that really belongs in a later milestone

## Module Anti-Patterns

- One fake module inside a milestone that has only one real capability area
- Modules as one-off buckets or temporary categories

## Task Anti-Patterns

- Tasks named after files, endpoints, tests, migrations, or refactor slices
- Implementation or verification split into separate tasks ("code review", "write unit tests", "add repository file", "update handler", "write migration")
- Vague `core`, `MVP`, `foundation`, `polish`, or `release readiness` tasks that bundle multiple independently selectable capabilities or collect docs, verification, review follow-up, and planning updates as leftovers
- Tiny modules as buckets for one-off tasks
- One catch-all module when tasks should live directly under the milestone

## Dependency Anti-Patterns

- Task dependencies carrying phase sequencing that should be expressed as milestone order
- Cross-milestone task-level `Depends on` links when the milestone order already expresses the dependency

## Milestone Transition Anti-Patterns

- Jumping into a task from a later milestone while the previous milestone is still open or the later milestone is still marked `Roadmap confirmed: no`
- Closing a milestone with non-empty `Handoff Notes`
- Adding work to a completed milestone

## Spec/Plan Anti-Patterns

- Creating a task-local spec or plan in global `docs/specs/` or `docs/plans/` by default
- Creating multiple specs for one task instead of revising the existing spec or splitting the task first

## Governance Anti-Patterns

- Auto-committing docs-only/governance changes before reporting the result or before user commit confirmation
- Starting another task before resolving branch closing for the current task
- Starting a task in milestone `M(n+1)` while `M(n)` still appears open and unclosed, or while the target milestone is still explicitly unconfirmed
