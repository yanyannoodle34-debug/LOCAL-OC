# CLAUDE.md — LOCAL-OC

This file provides context and conventions for AI assistants (Claude Code and others) working in this repository.

## Project Overview

| Field       | Value                                              |
|-------------|----------------------------------------------------|
| Name        | LOCAL-OC                                           |
| Description | Generator Oc                                       |
| License     | MIT                                                |
| Owner       | yanyannoodle34-debug                               |
| Repository  | https://github.com/yanyannoodle34-debug/LOCAL-OC   |
| Status      | Initial scaffold — no application code yet         |

The project purpose and domain are not yet defined beyond the stub README. Update this section when the scope is established.

## Repository Structure

```
LOCAL-OC/
├── LICENSE          # MIT license
├── README.md        # Project stub
└── CLAUDE.md        # This file
```

As the project grows, expected top-level directories will include:

```
src/          # Application source code
tests/        # Test files
docs/         # Documentation
```

Update this section whenever the layout changes significantly.

## Development Workflow

### Branches

- **`main`** — default/production branch; never push directly
- **`claude/<description>-<id>`** — AI-generated branches (e.g. `claude/claude-md-docs-1e0abr`)
- **Feature branches** — create from `main`; use descriptive names

### Commits

Write clear, imperative-mood commit messages:

```
docs: add CLAUDE.md with initial project documentation
feat: add user authentication module
fix: handle null pointer in config loader
```

### Push

```bash
git push -u origin <branch-name>
```

### Pull Requests

Do not open a pull request unless explicitly asked. When creating one, check `.github/` for a PR template and follow its structure.

## Technology Stack

> Not yet determined. Update this section when the stack is chosen.

| Concern       | Choice |
|---------------|--------|
| Language      | TBD    |
| Framework     | TBD    |
| Build tool    | TBD    |
| Package mgr   | TBD    |
| Test runner   | TBD    |

## Getting Started

> No setup steps yet. Update this section when dependencies and tooling are added.

Once a stack is chosen, this section should document:

```bash
# Install dependencies
# e.g. npm install / pip install -r requirements.txt

# Start dev server / run the app
# e.g. npm run dev / python -m src.main

# Run tests
# e.g. npm test / pytest
```

## Testing

> No test framework chosen yet.

When tests are added, document here:
- How to run the full test suite
- How to run a single test file
- Where test files live relative to source files
- Any coverage thresholds enforced in CI

## Code Conventions

> No linters or formatters configured yet.

When tooling is added, document the commands here. For example:

```bash
# Lint
# e.g. npm run lint / ruff check .

# Format
# e.g. npm run format / ruff format .
```

Until then, follow these baseline conventions:
- Write no comments unless the WHY is non-obvious (a hidden constraint, a subtle invariant, a workaround)
- Do not explain WHAT the code does — well-named identifiers already do that
- Keep functions small and single-purpose
- Prefer editing existing files over creating new ones

## Environment Variables

> None configured yet.

When environment variables are introduced:
- Store them in `.env` (gitignored — never commit this file)
- Provide a `.env.example` with placeholder values and a comment for each variable
- Document required variables here

## AI Assistant Guidelines

These rules apply to Claude Code and any other AI assistant working in this repository.

### Do
- Work on the designated branch for the task
- Commit with a clear message after completing a task
- Push to the designated branch when done
- Prefer editing existing files over creating new ones
- Ask before creating new top-level directories or introducing new dependencies

### Do not
- Push directly to `main`
- Open a pull request unless explicitly asked
- Add features, refactoring, or abstractions beyond what the task requires
- Add comments that explain WHAT the code does
- Create README or documentation files unless explicitly asked (CLAUDE.md is the exception)
- Add error handling for scenarios that cannot happen
- Leave half-finished implementations

### When in doubt
Ask a clarifying question rather than making a large assumption about intent.
