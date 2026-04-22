# Roadmap Needed

## Prompt

Use doc-driven-spec-workflow.

We need to deliver an enterprise admin package with organization settings, role management, audit logs, billing permissions, and an initial compliance export. Help me break this into work we can deliver safely.

## Expected Skill

`milestone-planning`

## Expected Behavior

- Recognizes that the request is a broad product scope, not a selected concrete task.
- Routes to `milestone-planning`.
- Decides whether the work should be one milestone or several.
- Decides whether modules are useful.
- Proposes independently reviewable tasks.
- Explains milestone/module/task boundary rationale.
- Stops after roadmap structure or task selection unless the user explicitly asks to continue.

## Expected File Changes

None.

## Must Not

- Must not write task-local `spec.md`.
- Must not write task-local `plan.md`.
- Must not start implementation.
- Must not use `task-spec-execution` as the primary place to invent task structure.
- Must not split work into implementation mechanics such as files, endpoints, migrations, tests, or code review tasks.

## Self-Check

```text
Result: PASS/WARN/FAIL
Observed skill:
Stop point:
Forbidden behavior observed:
Notes:
```
