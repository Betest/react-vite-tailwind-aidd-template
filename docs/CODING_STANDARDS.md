# Coding Standards

## General
- Prefer clarity over cleverness.
- Avoid changing public interfaces unless requested.
- Keep functions small and testable.

## Error handling
- Fail fast with clear errors.
- Preserve existing error types/messages unless asked.

## Testing
- Add tests for new behavior and bug fixes.
- Prefer unit tests; integration tests when necessary.
- Tests should be deterministic.

## Refactors
- Refactor in small steps:
  1) Add/adjust tests
  2) Refactor internals
  3) Keep public API stable
