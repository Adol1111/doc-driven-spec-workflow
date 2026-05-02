# Spec Template

Prefer a compact task spec structure:

```md
# <Task Name> Design

## Background

## Goals

## Non-goals

## Option Selection

## Design

## Error Handling

## Testing and Verification

- Unit tests: `required | preferred | not needed`
- Integration tests: `required | preferred | not needed`
- Manual verification: `<steps>` or `none`
- Other verification: `<optional>` such as migration checks, compatibility checks, smoke checks, or other task-specific proof

## Docs Updates
```

Notes:

- Keep each section concise and focused on task-specific decisions and boundaries.
- Do not add content unrelated to the current task just to fill the template.
- For very small tasks, sections may be brief, but keep the same information order.
- Choose spec detail from the expected execution mode:
  - if the same agent continues immediately in the current session, the spec may stay compact and rely on nearby context
  - if another agent, subagent, model, or fresh conversation may pick up the work, make the spec self-contained enough to execute without chat memory
  - if the execution mode is unclear and the difference matters, ask before drafting
- For self-contained compact specs, write the concrete handoff details inside the existing sections:
  - preferred proof samples, fixtures, or evidence sources
  - preferred implementation surface or first modification target
  - per-case acceptance signals stating what each proof case must show to pass
- Compact does not mean implicit. If another agent could reasonably misread the task, make the boundary explicit in the existing sections:
  - `Goals`: state whether the task is defining/proving a boundary, implementing behavior, migrating data, cleaning up docs, or another work type.
  - `Non-goals`: name tempting but forbidden implementation shortcuts or related changes that must not be done in this task.
  - `Design`: use task-specific subheadings as needed; for ambiguous tasks, include boundary decisions, the allowed minimal implementation, and where responsibility or classification must and must not live.
  - `Testing and Verification`: say explicitly which proof types are required for this task. Unit tests are one possible proof type, not the only one.
- Prefer making testing expectations explicit rather than implied.
- For code changes, consider automated verification by default when it is practical, but do not force unit tests when they do not fit the task.
- If the user explicitly asks not to add unit tests, record that decision in `Testing and Verification` instead of silently omitting tests.
- If relevant existing automated tests already cover the touched behavior, they still need to remain truthful and passing unless the task intentionally changes that behavior.
- Distinguish changing test files from changing test meaning. Small repairs that preserve the original assertion intent are normal maintenance; changing the asserted behavior, weakening coverage, deleting tests, or marking them skip/xfail/todo should be called out explicitly.
- If the task intentionally changes behavior that existing tests cover, record that expectation in `Testing and Verification` so later execution can update those tests with the right rationale.
- Keep TDD separate from testing expectations. `Testing and Verification` describes what proof is needed, not whether the implementation must be test-first.
