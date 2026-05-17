# Plan Template

Create a plan only when a plan trigger is present. Prefer a compact structure:

The plan supplements the approved `spec.md`. It should focus on implementation sequencing, file touch points, coordination boundaries, and verification order. Do not restate the full spec unless a short recap is needed to make the plan readable on its own.

```md
# <Task Name> Implementation Plan

**Goal:** <One sentence describing what this implementation should deliver>

**Approach:** <2-4 sentences on implementation strategy, responsibilities, and key tradeoffs>

**Tech Stack:** <Key technologies or modules involved>

**Key Risks / Constraints:** <What can go wrong, what must stay compatible, or what sequencing pressure matters>

---

## File Map

- Create: `path/to/file`
  - Explain what this file is responsible for
- Modify: `path/to/file`
  - Explain the responsibility of the change

## 1. <Implementation Slice>

- Outcome: <what is true after this slice>
- Files: `<path>`, `<path>`
- Notes: <key boundary, ordering, or coordination note>
- Verification: <how this slice is proven before moving on>
- Commit checkpoint: `<optional checkpoint name>` only when this slice ends in a verified, reviewable, reversible state

## 2. <Implementation Slice>

- Outcome: <what is true after this slice>
- Files: `<path>`, `<path>`
- Notes: <key boundary, ordering, or coordination note>
- Verification: <how this slice is proven before moving on>
- Commit checkpoint: `<optional checkpoint name>` only when this slice ends in a verified, reviewable, reversible state

## 3. <Implementation Slice>

- Outcome: <what is true after this slice>
- Files: `<path>`, `<path>`
- Notes: <key boundary, ordering, or coordination note>
- Verification: <how this slice is proven before moving on>
- Commit checkpoint: `<optional checkpoint name>` only when this slice ends in a verified, reviewable, reversible state

## Optional Flow Diagram

- Optional: add a small `mermaid` diagram only when implementation sequencing, rollout flow, or system coordination is hard to explain with bullets alone

## Verification

- `command`
- `command`
```

Notes:

- Prefer `Goal + File Map + 3-5 implementation slices + Verification`
- Treat the approved `spec.md` as the source of truth for behavior, scope, exclusions, and tradeoffs
- Keep any recap minimal; avoid rewriting sections that already belong in `spec.md`
- Favor concise implementation guidance over step-by-step execution scripts, but make the sequencing and expected post-slice state obvious.
- Use short code snippets only when they clarify a critical interface, data shape, migration rule, or tricky algorithm boundary. Avoid large code blocks or implementation drafts that can be copied wholesale into production code.
- If a reader cannot tell why the order matters, what each slice delivers, or where the risky boundary is, the plan is still too vague.
- Use a small `mermaid` diagram only when it materially improves understanding of rollout, sequencing, or cross-system coordination.
- Put commit checkpoints inside the relevant implementation slices, not in a separate summary section.
- Commit checkpoints are optional judgment-based checkpoints. Do not add one per slice mechanically; simple tasks may only need the final implementation commit.
- Name each checkpoint by the stable state it captures, not as `commit1`, `commit2`, or by fixed stage numbers.
- Keep docs-sync work in one compact section instead of many mechanical substeps
