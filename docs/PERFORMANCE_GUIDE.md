# Performance Guide (React)

## Defaults
- Prefer clarity first (KISS). Optimize only when it matters.
- Props are OK. Avoid unstable references and unnecessary rerender cascades.

## Stable props
Prefer:
- primitives (string/number/boolean)
- stable objects via useMemo (only if needed)
- stable callbacks via useCallback (only if passed to memoized children or expensive trees)

Avoid:
- `{...}` inline objects in JSX for memoized children
- inline arrow functions passed deep into memoized trees (when it causes churn)

## Component boundaries
- Split large components so only the changing piece rerenders.
- Keep state close to where it is used.
- Avoid lifting state unless multiple siblings truly need it.

## Context
- Do not store fast-changing values in a broad Context.
- Split contexts by volatility.

## useEffect
- Only for external sync.
- Correct dependencies; no blanket disabling eslint rules.

## When to use memoization
- React.memo: expensive pure components + stable props + frequent rerenders.
- useMemo: expensive computation.
- useCallback: stable handler identity for memoized children.
Never memoize “by habit”.
