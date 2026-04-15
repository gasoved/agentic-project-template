# Workspace Notes

## Repository structure

This workspace uses two separate git repositories:

- **Workspace repo** (this directory) — tracks coordination files: `AGENTS.md`, `spec/`, `tasks/`, and any workspace-level documentation. The project subdirectory is gitignored here.
- **Project repo** (the project subdirectory) — tracks all implementation code, its own tooling config, and its own `.gitignore`. Initialized by the scaffold task.

Keep commits in the correct repo. Do not mix workspace documentation commits with project implementation commits unless explicitly asked.

## Commits

- Work in small, atomic commits; each commit should do one coherent thing.
- Use one-line commit messages by default.
- If a bounded slice is implemented and verified, commit it without asking first unless there is contract tension, risky scope uncertainty, or a meaningful tradeoff that needs review.
- When handing off completed work that was committed, include the commit id in the hand-off message.

## Verification

- Verify each slice before committing when practical.
- Run the project's format, lint, typecheck, and test commands before committing. If the project defines a single umbrella check command, prefer that.

## Testing

- Add the smallest relevant tests in the same commit as each behavior change when practical. If a commit intentionally has no tests, say why.
- Start testing early; do not defer all testing.
- Test observable outcomes (CLI output, API responses, state changes), not internal representation shapes.
- Do not replace placeholder tests with fake-value tests; add real tests when behavior exists, otherwise keep an explicit temporary no-test stub.

## Code style and tooling

- Let the formatter own code style; do not hand-format or add style-only lint rules that fight the formatter.
- Follow existing conventions unless there is a clear reason to introduce a new pattern.
- When adding tooling, keep it lean and justify the maintenance cost; avoid hooks, rules, or automation that slow early development without clear payoff.
- If a new lint or type rule reveals real code issues, fix those in the same commit as the rule when practical.
- Add short intent-preserving comments for non-obvious boundaries, seams, or invariants that could be lost during refactors. Do not comment self-explanatory code.

## Architecture and design

- Progress is measured by working product behavior, not architecture coverage. Every commit should be on the shortest path to making the core user story work.
- Prove the end-to-end user story works with the simplest code before refining internal module boundaries. A working vertical slice beats polished horizontal layers.
- Build for the concrete case first. Extract an interface or generalize only when a second real consumer or implementation arrives.
- Start with fewer, larger modules. Split only when a module has genuinely independent consumers, release cadence, or deployment targets -- not for conceptual cleanliness alone.
- Do not create wrapping modules that only forward calls; inline delegation until real behavior justifies the boundary.
- Do not define types, interfaces, or API contracts for features with no implementation. Do not write placeholder functions that return "not implemented yet". Build scaffolding when the implementation is ready.
- Prefer the simplest type that expresses the intent; avoid overcomplicated conditional or inferred types when a direct shared type already works.
- A function's parameter surface should match what it actually uses today, not what it might need later.
- If data flows through more than two transformation shapes between input and output, justify each shape. Overlapping fields between adjacent shapes signal unnecessary splitting.
- One module should own each piece of logic. If two packages need the same function, move it to shared rather than duplicating it.
- Do not encode documentation, limitations, or known issues as exported typed constants. Use comments or markdown.

## Dependencies

- Pull a dependency only when it displaces more code than it imports, its transitive tree is small and audited, and the hand-rolled alternative would require rediscovering a domain's known edge cases.

## Spec and plan discipline

- If the project has a spec or plan document, load them into working context before planning or implementation.
- Do not drift from the spec or plan during implementation unless there is a clear reason. If implementation pressure suggests a change, stop and get explicit user approval before proceeding.

## Multi-agent coordination

- When coordinating parallel agents, review actual commits (not just summaries) when commit ids are available.
- Periodically re-estimate which agents are ready to launch and how many lead-owned tasks remain before each blocked agent becomes safe to launch. Re-check after each meaningful merge, each worker return, and before starting a new wave.
- After each worker hand-off, suggest the next atomic step for yourself when other lanes are blocked, or the next steps for all currently unblocked lanes when parallel work is available.

## Judgment

- Push back when an idea weakens simplicity, safety, portability, or maintainability. Explain briefly and propose a better alternative.
- Prefer self-contained implementation docs.

## Environment and secrets

- Never commit secrets, API keys, or credentials. Use environment variables or `.env` files (gitignored) for sensitive configuration.
- Document required environment variables in a `.env.example` file.

## Local environment blockers

- If a task is blocked by a local environment constraint that requires human intervention (e.g. Docker needing `sudo`, a missing system dependency, required credentials, or a permission issue), stop and notify the human immediately rather than attempting workarounds. Describe the blocker clearly and what action is needed to unblock it.
