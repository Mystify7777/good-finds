# Contributing

Thanks for contributing to Good Finds.

## Before changing code

- Read the [PRD](docs/product/PRD.md).
- Review the [architecture overview](docs/architecture/README.md).
- Check existing issues and ADRs before proposing new behavior.
- Keep changes aligned with MVP scope.

## Workflow

1. Create or select a GitHub issue for the work.
2. Confirm acceptance criteria and dependencies.
3. Create a focused branch from `main`.
4. Implement the smallest complete change.
5. Add or update tests for behavior and failure cases.
6. Run formatting, linting, type checking, and relevant tests.
7. Open a pull request linking the issue.
8. Explain design choices, risks, and validation performed.

## Engineering expectations

- TypeScript strictness should be enabled.
- Validate data at trust boundaries.
- Enforce authorization server-side; never rely on hidden UI controls.
- Keep marketplace provider types behind adapter boundaries.
- Preserve provenance for externally sourced data.
- Avoid logging secrets or unnecessary personal information.
- Add migrations for schema changes and test relevant access policies.
- Prefer explicit domain types and deterministic tests.
- Do not add dependencies without a clear need.

## Pull requests

PRs should include:
- Summary and linked issue.
- User-visible behavior.
- Implementation notes where non-obvious.
- Tests and commands run.
- Screenshots for meaningful UI changes.
- Security/privacy implications.
- Migration or configuration steps.

## Scope

Do not add future-phase features to the MVP without an explicit issue/scope decision.
