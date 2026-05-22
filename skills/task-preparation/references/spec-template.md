# Spec Template

Language rule: localize generated headings, labels, and field names to the repository documentation language. The English headings below describe structure only and are not fixed output text.

Prefer a compact task spec structure:

```md
# <Task Name> Design

## Background

## Goals

## Non-goals

## Option Selection

### Option A: <option name>

Approach:

- <what this option does>
- <optional second detail>

Pros:

- <short advantage>
- <short advantage>

Cons:

- <short drawback>
- <short drawback>

Conclusion: `reject, <very short reason>` or `choose`

### Option B: <option name>

Approach:

- <what this option does>
- <optional second detail>

Pros:

- <short advantage>
- <short advantage>

Cons:

- <short drawback>
- <short drawback>

Conclusion: `reject, <very short reason>` or `choose`

### Option C: <option name>

Approach:

- <what this option does>
- <optional second detail>

Pros:

- <short advantage>
- <short advantage>

Cons:

- <short drawback>
- <short drawback>

Conclusion: `reject, <very short reason>` or `choose`

Selected: `Option <A | B | C>`

### Decision Matrix

| Decision Point | Chosen | Rejected | Why |
| --- | --- | --- | --- |
| <what needs deciding> | <selected option> | <other real options> | <selection rationale> |

## Design Overview

## Design Details

### Entry Points / Surfaces

### Data / Control Flow

### Boundary Decisions

## Diagram

- Optional: add a small `mermaid` diagram only when flow, state, ownership, or system interaction would be hard to understand from text alone

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
- Prefer writing this as a real design document, not only a task summary. A good spec should make the intended solution, boundaries, and implementation shape understandable before code starts.
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
- `Option Selection`: prefer a shallow structure like `Option A/B/C` headings rather than deeply nested bullets. For each option, include `Approach`, `Pros`, `Cons`, and a one-line `Conclusion`. Rejected options should end with `reject, <very short reason>`. After the options, add one short `Selected: Option X` line to make the final choice obvious. Use a small `Decision Matrix` only as supporting structure when there are multiple real branches. Use the clarification-loop answers as the selection rationale when relevant. If the decision is tiny, short bullets are better than a table.
  - `Design Overview`: summarize the chosen approach in a few sentences so the reader knows what is being built before reading details.
  - `Entry Points / Surfaces`: name the first edit surface, owning module, external interface, or user-visible touchpoint.
  - `Data / Control Flow`: explain the main request, state, or event flow from entry to outcome. Prefer a small `mermaid` diagram when this would otherwise be dense.
  - `Boundary Decisions`: state what responsibility lives where, the allowed minimal implementation, and where responsibility or classification must and must not live.
- Do not drop the option section just because clarification happened through back-and-forth questions. The final spec should still make the evaluated alternatives and final rationale visible to later readers.
- `Testing and Verification`: say explicitly which proof types are required for this task. Unit tests are one possible proof type, not the only one.
- Use `Diagram` only when it materially improves understanding. Prefer one small high-signal diagram over large decorative diagrams.
- Prefer making testing expectations explicit rather than implied.
- For code changes, consider automated verification by default when it is practical, but do not force unit tests when they do not fit the task.
- If the user explicitly asks not to add unit tests, record that decision in `Testing and Verification` instead of silently omitting tests.
- If relevant existing automated tests already cover the touched behavior, they still need to remain truthful and passing unless the task intentionally changes that behavior.
- Distinguish changing test files from changing test meaning. Small repairs that preserve the original assertion intent are normal maintenance; changing the asserted behavior, weakening coverage, deleting tests, or marking them skip/xfail/todo should be called out explicitly.
- If the task intentionally changes behavior that existing tests cover, record that expectation in `Testing and Verification` so later execution can update those tests with the right rationale.
- Keep TDD separate from testing expectations. `Testing and Verification` describes what proof is needed, not whether the implementation must be test-first.
