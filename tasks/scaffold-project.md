# Task: Scaffold Project

## Prerequisites

- `spec/spec.md` and `spec/plan.md` must exist before running this task.
- Read both documents fully before making any scaffolding decisions.

## Objective

Initialize the project directory with the appropriate tooling, configuration, and structure derived from the spec and plan. The result should be a working project skeleton where format, lint, typecheck, and test commands all pass on the first run.

## Steps

### 1. Determine tech stack and project shape

Read the spec and plan to identify:

- Primary language(s) and runtime (e.g., TypeScript/Node, Python, Rust, Go)
- Project shape: monorepo vs single package, CLI vs API vs library, etc.
- Key dependencies and integration points mentioned in the spec
- Deployment targets if specified (affects build tooling choices)

### 2. Initialize project structure

- Set up the project in the `<project_name>/` directory (rename to actual project name if not already done)
- Create the package manifest (package.json, pyproject.toml, Cargo.toml, go.mod, etc.)
- Create the directory layout appropriate to the stack and project shape
- Do not create placeholder source files beyond what is needed for tooling to pass

### 3. Set up code quality tooling

Choose tools appropriate to the stack. Prefer single-tool solutions over multi-tool stacks where available.

| Concern | TypeScript | Python | Rust | Go |
|---|---|---|---|---|
| Formatting | Prettier | Ruff | rustfmt | gofmt |
| Linting | ESLint | Ruff | Clippy | go vet / staticcheck |
| Type checking | tsc | Pyright or mypy | (compiler) | (compiler) |
| Testing | Vitest or Node test runner | pytest | cargo test | go test |
| Package mgmt | pnpm (preferred) | uv (preferred) | cargo | go modules |

These are defaults -- deviate if the spec or plan calls for something specific.

Configure each tool with sensible defaults:

- Formatter: use the tool's defaults or the community standard config. Do not add cosmetic overrides.
- Linter: start with the recommended rule set. Enable `max-lines` or equivalent file-length warnings if the stack supports it (e.g., 300 warn / 500 error for source files).
- Type checking: strict mode where practical.

### 4. Wire up verification commands

Create an umbrella command that runs all checks in sequence (format check, lint, typecheck, test). This should be the single command an agent or developer runs to verify correctness.

Examples:

- **TypeScript/pnpm**: `pnpm check` that runs `format:check && lint && typecheck && test`
- **Python/uv**: a `Makefile` or script with a `check` target
- **Rust**: `cargo fmt --check && cargo clippy -- -D warnings && cargo test`
- **Go**: `gofmt -l . && go vet ./... && staticcheck ./... && go test ./...`

The specific mechanism (package.json scripts, Makefile, just, shell script) should follow the stack's conventions.

### 5. Set up environment and secrets handling

- Add `.env` to `.gitignore` if not already present
- Create `.env.example` listing any environment variables the spec mentions, with placeholder values and brief comments
- If no environment variables are known yet, create an empty `.env.example` with a comment explaining its purpose

### 6. Set up minimal passing state

- Ensure all verification commands pass with zero warnings on the empty/minimal project
- If the test runner requires at least one test file to not error, add a single trivial test (e.g., `assert true`) with a comment indicating it is a bootstrap placeholder

### 7. Update CLAUDE.md

Append a project-specific verification section to CLAUDE.md with:

- The exact commands to run for format, lint, typecheck, test, and the umbrella check
- Any stack-specific conventions the agent chose (e.g., "using Ruff for both formatting and linting")

Do not remove or rewrite existing CLAUDE.md content -- only append the project-specific section.

## Constraints

- Do not add dependencies beyond what is needed for the quality tooling itself. Application dependencies come later during implementation.
- Do not create source files for features described in the spec. This task only sets up the skeleton and tooling.
- Do not add git hooks (pre-commit, husky, etc.) unless the spec explicitly requests them.
- Prefer tools with minimal configuration over tools that require extensive setup.
- If a choice is ambiguous and the spec does not constrain it, pick the most common community default and note the choice in CLAUDE.md.
