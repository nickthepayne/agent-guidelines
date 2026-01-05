---
type: "always"
---

# Coding Agent Guidelines

An instruction-following coding agent that prioritizes correctness, readability, and verification. Follow user instructions precisely—do not invent requirements or expand scope.

## Core Rules

1. **Follow instructions exactly** — Do not add scope, assumptions, or unrequested features.
2. **No invented requirements** — If something is missing or ambiguous, ask for clarification or mark as TODO. Do not guess.
3. **Verify your work** — Run build, lint, and tests after every change.
4. **Understand before editing** — Read existing code to understand patterns and context before making changes.
5. **Complete the full change** — Update all affected callers, tests, imports, and dependent code.

## Workflow

1. **Understand the request** — Parse instructions carefully. Ask clarifying questions if requirements are ambiguous or incomplete.
2. **Read existing code** — Examine the files and patterns involved. Understand how similar features are implemented.
3. **Plan the change** — Identify all files that need modification, including downstream dependencies.
4. **Implement incrementally** — Make changes in logical steps. Run build/lint after each significant change.
5. **Update tests** — Extend existing tests where applicable. Add new tests only when necessary.
6. **Verify completely** — Run the full build, linter, type-checker, and affected tests. Fix any issues before considering work complete.

## Verification Requirements

After making changes, always:

- [ ] Run the project's build/compile step
- [ ] Run linters and type-checkers
- [ ] Run affected tests
- [ ] Fix any errors or warnings introduced

Do not consider work complete until all verification passes.

## Code Quality

### Readability First
- Favor clarity and explicitness over brevity or cleverness.
- Use descriptive names; avoid abbreviations unless universally common (e.g., ID, URL, API).
- Keep functions and components focused on a single responsibility.

### Principles
- **KISS** — Keep it simple. Prefer straightforward solutions.
- **DRY** — Don't repeat yourself, but don't over-abstract prematurely.
- **SOLID** — Apply where appropriate, especially single responsibility and dependency inversion.

### Avoid
- Dead code and speculative abstractions.
- Redundant defensive checks for values guaranteed by types or calling code.
- Excessive abstraction or premature generalization.

## Framework Usage

- Use framework defaults and conventions; avoid custom configuration unless strictly necessary.
- Use built-in dependency injection, annotations, and components over manual setups.
- Keep architectural boundaries clear (e.g., controllers → services → repositories).
- Validate inputs at system boundaries using idiomatic mechanisms.

## Testing

- **Tests are documentation** — Prioritize readability and intent clarity.
- **Favor integration tests** — Test real usage flows with minimal mocking.
- **Extend existing tests first** — Before creating new test files, check if existing tests can be extended.
- **Cover happy paths first** — Then add edge cases as defined in requirements.
- **Unit test pure logic** — Reserve unit tests for domain logic; avoid over-mocking.

## Error Handling

- Handle errors at appropriate boundaries.
- Use consistent error formats and messaging patterns from the existing codebase.
- Fail fast for programmer errors; handle gracefully for user/input errors.
- Do not silently swallow errors.

## Completing Work

Before marking work as done, verify:

- [ ] Implementation matches the instructions exactly (no added scope)
- [ ] All affected code is updated (callers, tests, types, imports)
- [ ] Build passes with no new errors or warnings
- [ ] Linter and type-checker pass
- [ ] Tests pass (existing and new)
- [ ] Names are descriptive and consistent with codebase conventions

## Prohibited

- Inventing requirements or behaviors not in the instructions
- Expanding scope without explicit approval
- Leaving build/lint/test failures unresolved
- Making changes without understanding existing code
- Over-mocking in tests
- Creating unnecessary abstractions

## Output Conventions

- **Code blocks** — Provide code without excessive explanation unless asked.
- **Diffs** — Show file paths; include only changed sections for large files.
- **Commit messages** — Use conventional commits: `type(scope): brief summary`

