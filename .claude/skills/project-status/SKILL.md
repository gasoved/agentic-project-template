---
name: project-status
description: Use this skill to maintain tasks/status.md as a compact current-state assessment file.
---

# Project Status Skill

Use this skill to maintain `tasks/status.md` as a compact current-state assessment file.

## Purpose

`tasks/status.md` is not a spec, plan, or changelog. It exists to preserve live execution context that could be lost across turns:
- current blockers
- active risks
- confidence notes
- important unknowns
- short hand-off context
- decisions in flight

## When to use

- Before planning or implementation, load `tasks/status.md` if it exists.
- If it does not exist and meaningful assessment context emerges that is likely to matter across turns, create it from the template.
- Update it when the project’s current execution state materially changes.

## What belongs

Include only notes that still affect near-term execution or decisions.

Good examples:
- a blocker requiring human action
- a risk that changes implementation order
- uncertainty about a dependency or local environment
- a short note that a task is partially complete and what remains
- a recent decision that affects the next steps

Do not include:
- requirements already captured in `spec/`
- detailed task decomposition already captured in `tasks/`
- long historical narrative
- resolved issues
- speculative future ideas with no current impact

## Maintenance rules

- Keep the file short.
- Rewrite or delete stale notes instead of appending indefinitely.
- Prefer current state over history.
- If a note no longer changes what should happen next, remove it.

## Preferred sections

Use these sections when relevant:
- Summary
- Current State
- Blockers
- Risks
- Open Questions
- Next Check

## Authoritative sources

- `spec/` and explicit task documents define requirements and scope.
- `tasks/status.md` is situational execution context only.
