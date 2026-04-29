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

## Docs Updates
```

Notes:

- Keep each section concise and focused on task-specific decisions and boundaries.
- Do not add content unrelated to the current task just to fill the template.
- For very small tasks, sections may be brief, but keep the same information order.
- Choose the compact spec strictness from the expected execution mode:
  - same agent continuing immediately in the current session: author-ready is acceptable
  - another agent, subagent, model, or fresh conversation: default to handoff-ready
  - if the execution mode is unclear and the difference matters, ask before drafting
- For handoff-ready compact specs, make the handoff anchors concrete inside the existing sections:
  - preferred proof samples, fixtures, or evidence sources
  - preferred implementation surface or first modification target
  - per-case acceptance signals stating what each proof case must show to pass
- Compact does not mean implicit. If another agent could reasonably misread the task, make the boundary explicit in the existing sections:
  - `Goals`: state whether the task is defining/proving a boundary, implementing behavior, migrating data, cleaning up docs, or another work type.
  - `Non-goals`: name tempting but forbidden implementation shortcuts or related changes that must not be done in this task.
  - `Design`: use task-specific subheadings as needed; for ambiguous tasks, include boundary decisions, the allowed minimal implementation, and where responsibility or classification must and must not live.
  - `Testing and Verification`: verify the required behavior and, when relevant, verify that forbidden shortcuts were not introduced.
