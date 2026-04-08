# agentic-project-template

Opinionated project template for agent-driven software development. Spec-first workflow, two-repo structure, and automated scaffolding.

## What this is

A starter template for projects where AI agents (e.g., Claude Code) do most of the implementation work. It provides:

- A **spec-first workflow** — define what you're building before writing code
- A **two-repo structure** — workspace coordination (specs, tasks, agent instructions) lives separately from implementation code
- **Automated scaffolding** — an agent-readable task that initializes the project with the right tooling for any tech stack
- **Agent instructions** (`AGENTS.md`) — shared rules for commits, testing, architecture, and multi-agent coordination

## Structure

```
.
├── AGENTS.md              # Agent instructions (symlinked as CLAUDE.md)
├── spec/
│   └── GUIDE.md           # Reference for spec and plan conversations
├── tasks/
│   ├── README.md          # Workflow overview
│   └── scaffold-project.md  # Scaffolding task (run after spec/plan)
└── <project_name>/        # Project code (its own git repo)
```

## Workflow

1. **Spec** — Converse with an agent to define the project. Produces `spec/spec.md`.
2. **Plan** — Agent generates `spec/plan.md` from the spec (tech stack, milestones, key decisions).
3. **Scaffold** — Agent runs `tasks/scaffold-project.md` to initialize the project directory with tooling, quality guardrails, and verification commands appropriate to the chosen stack.
4. **Implement** — Build the project according to the plan.

## Usage

```bash
# GitHub template
gh repo create my-project --template gasoved/agentic-project-template --clone
cd my-project

# Or with degit
npx degit gasoved/agentic-project-template my-project
cd my-project
```

Then start a conversation with your agent to define the spec.

## Tech stack agnostic

The template itself contains no language-specific tooling. The scaffolding task reads the spec and plan to determine the right stack, then sets up formatting, linting, type checking, testing, and an umbrella verification command accordingly.

## License

MIT
