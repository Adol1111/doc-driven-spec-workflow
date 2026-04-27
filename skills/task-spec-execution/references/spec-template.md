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
- Compact does not mean implicit. If another agent could reasonably misread the task, make the boundary explicit in the existing sections:
  - `Goals`: state whether the task is defining/proving a boundary, implementing behavior, migrating data, cleaning up docs, or another work type.
  - `Non-goals`: name tempting but forbidden implementation shortcuts or related changes that must not be done in this task.
  - `Design`: use task-specific subheadings as needed; for ambiguous tasks, include boundary decisions, the allowed minimal implementation, and where responsibility or classification must and must not live.
  - `Testing and Verification`: verify the required behavior and, when relevant, verify that forbidden shortcuts were not introduced.
