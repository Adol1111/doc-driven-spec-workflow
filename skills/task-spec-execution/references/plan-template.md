# Plan Template

Create a plan only when the task is genuinely complex or multi-step. Prefer a compact structure:

```md
# <Task Name> Implementation Plan

**Goal:** <One sentence describing what this implementation should deliver>

**Architecture:** <2-3 sentences on approach, responsibilities, and key tradeoffs>

**Tech Stack:** <Key technologies or modules involved>

---

## File Map

- Create: `path/to/file`
  - Explain what this file is responsible for
- Modify: `path/to/file`
  - Explain the responsibility of the change

## 1. <Implementation Section>

- Use concise bullets for implementation scope, boundaries, and key notes

## 2. <Implementation Section>

- Use concise bullets for implementation scope, boundaries, and key notes

## 3. <Implementation Section>

- Use concise bullets for implementation scope, boundaries, and key notes

## Verification

- `command`
- `command`
```

Notes:

- Prefer `Goal + File Map + 3-5 implementation sections + Verification`
- Favor concise implementation guidance over step-by-step execution scripts
- Unless the task truly needs it, avoid large code blocks, TDD scaffolding, or commit steps
- Keep docs-sync work in one compact section instead of many mechanical substeps
