# Context Template

Use for research notes, references, experiment results, and conclusions that are not yet stable.

## Recommended Structure

```md
# <Topic>

## Purpose
- Why this record is needed

## Background
- Context for the current discussion or research

## Findings / References
- Examples, observations, API behavior, experiment comparisons, external references

## Current Conclusions
- Main conclusions confirmed in this round

## Viable Options
- What can be done now
- Why it is viable

## Not Viable / Deferred
- What cannot be done now, or why it is deferred

## Known Issues
- Remaining risks, limits, dependencies, or unclear points

## Next Actions
- What still needs validation
- Which conclusions should move to `docs/architecture/`

## Promotion Rule
- Move stable conclusions to `docs/architecture/`
```

## Rules

- Do not use `docs/context/` as the source of current task status.
- Unless content has moved to `docs/architecture/`, do not treat it as a stable behavior rule.
