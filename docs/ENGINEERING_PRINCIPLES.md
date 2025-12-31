# Engineering Principles

## Core
- KISS: simplest solution that meets requirements.
- DRY: reduce duplication only when it’s real duplication (rule of 3).
- Clean Code: clear names, small components, explicit types, predictable flow.
- Prefer composition and small modules over large “god” components.

## SOLID in frontend
- SRP: one component/hook = one responsibility.
- OCP: extend via props/composition, avoid breaking changes.
- ISP: small, focused prop types.
- DIP: isolate IO/API with adapters; UI depends on interfaces, not implementations.

## Refactor rules
- Minimal diff, no drive-by changes.
- No abstraction without benefit.
- Prefer incremental refactors with verification.
