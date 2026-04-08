# Spec and Plan Guide

This guide helps the agent conduct a productive spec conversation and know when the spec is complete. It is not a template to fill in — it is a reference for what good specs and plans contain.

## Workflow

1. **Spec conversation** — The user describes what they want to build. The agent asks clarifying questions until the spec covers the sections below, then writes `spec/spec.md`.
2. **Plan generation** — The agent reads the spec and produces `spec/plan.md` with implementation strategy.
3. **Scaffolding** — Run `tasks/scaffold-project.md` to set up the project skeleton and tooling.
4. **Implementation** — Build the project according to the plan.

## What a spec should cover

- **Problem** — What problem does this solve? Why does it need to exist?
- **Users** — Who will use this? What do they care about?
- **Core features** — What does the product do? Describe the key user stories or capabilities.
- **Constraints** — Technical constraints, platform requirements, performance targets, compliance needs.
- **Non-goals** — What is explicitly out of scope? This prevents scope creep during implementation.
- **External integrations** — APIs, services, or systems this project talks to.
- **Data** — What data does the project store, process, or move? Rough shape, not schema.

Not every project needs every section. A small CLI tool needs less than a multi-service platform. The agent should judge what is relevant and skip what is not.

## What a plan should cover

- **Tech stack** — Language, runtime, frameworks, and why.
- **Project shape** — Monorepo vs single package, CLI vs API vs library, deployment target.
- **Milestones** — Ordered list of vertical slices that build toward the full product. Each milestone should be independently testable.
- **Key decisions** — Choices that are hard to reverse later (database, auth strategy, API style). Call these out explicitly.
- **Open questions** — Anything unresolved that will need a decision during implementation.

## Questions the agent should ask

These are starting points, not a checklist. Follow the conversation naturally.

- What is this project for? What triggered the need?
- Who is the primary user? Are there secondary users?
- What does success look like? How will you know it works?
- Are there existing systems this needs to integrate with?
- Are there hard constraints (language, platform, timeline, compliance)?
- What have you already decided? What are you unsure about?
- What should this project explicitly *not* do?
