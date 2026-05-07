# Plan Template

Create a plan only when a plan trigger is present. Prefer a compact structure:

The plan supplements the approved `spec.md`. It should focus on implementation sequencing, file touch points, coordination boundaries, and verification order. Do not restate the full spec unless a short recap is needed to make the plan readable on its own.

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

## Commit Points

- Optional: after `<Implementation Section>` when the completed slice is verified, reviewable, and reversible
- Optional: final task commit after verification and docs/status updates

## Verification

- `command`
- `command`
```

Notes:

- Prefer `Goal + File Map + 3-5 implementation sections + Verification`
- Treat the approved `spec.md` as the source of truth for behavior, scope, exclusions, and tradeoffs
- Keep any recap minimal; avoid rewriting sections that already belong in `spec.md`
- Favor concise implementation guidance over step-by-step execution scripts
- Use short code snippets only when they clarify a critical interface, data shape, migration rule, or tricky algorithm boundary. Avoid large code blocks or implementation drafts that can be copied wholesale into production code.
- Commit points are optional judgment-based checkpoints. Do not add one per section mechanically; simple tasks may only need the final implementation commit.
- Keep docs-sync work in one compact section instead of many mechanical substeps
