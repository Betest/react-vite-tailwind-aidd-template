# RENDERING_RULES_V3 — React + TypeScript (AIDD‑Optimized)

> **Purpose**: default rendering contract for AI‑driven development (AIDD).  
> **Scope**: fast, mechanical rules with minimal tokens.  
> **Escalation**: if ambiguity exists, consult **Rendering Rules — Mechanical Guide v2**.

This document is intentionally **compact**, **non‑narrative**, and **enforceable**.

---

## 0) Core Definitions

- **Stable value**: primitive or reference with stable identity across renders.
- **Unstable value**: inline `{}` / `[]` / `() => {}` created during render.
- **Volatile context**: context value that changes frequently.
- **Server state**: remote async data (API responses).
- **Client state**: UI / interaction state.

---

## 1) Golden Defaults

- Props are OK. **Avoid prop drilling** and **avoid unstable identities**.
- Keep state **local by default**; never duplicate state.
- Split components so **only the changing part rerenders**.
- Memoization is **opt‑in**, never default.

---

## 2) Identity Rules (High Impact)

**Rule**: Inline objects, arrays, or functions passed to children are **forbidden** if the child is memoized or part of a large tree.

- **Reason**: unstable identity → rerender cascades.
- **Fix**: hoist constant, `useMemo`, or refactor API.

---

## 3) Callbacks

**Rule**: Inline callbacks are allowed **only** when identity does not matter.

- If child is memoized → use `useCallback` or pass primitive + handler.
- Lists prefer: `(id) => handler(id)` pattern.

---

## 4) Component Boundaries

**Rule**: Components must be split by volatility.

- Fast‑changing state stays low in the tree.
- Stable parents must not rerender due to volatile children.

---

## 5) Context Usage

**Rule**: Broad contexts must contain **stable values only**.

- Volatile data → local state or dedicated subtree.
- Split contexts by volatility.

---

## 6) Lists & Keys

**Rule**: List keys must be stable and semantic.

- ❌ index as key when reorder/insert/remove is possible.
- ✅ unique domain identifier.

---

## 7) Effects (`useEffect`)

**Rule**: Effects are for **external synchronization only**.

- ❌ computing derived UI state in effects.
- ✅ IO, subscriptions, timers.
- Deps must be correct; no blanket eslint disables.

---

## 8) State Ownership

**Rule**: each state has a single owner.

- **Server state** → TanStack Query only.
- **Global client state** → Zustand / RTK (cross‑cutting only).
- **Local state** → component or hook.

❌ Never store server responses in global stores.

---

## 9) Forms

**Rule**: Forms must use **React Hook Form + schema validation**.

- ❌ field‑level `useState` by default.
- Controlled inputs only when required by external libs.

---

## 10) Custom Hooks

**Rule**: Hooks encapsulate logic, not UI.

- Stable return API.
- Typed generics.
- Side‑effects must be explicit.

---

## 11) Observables

**Rule**: Use Observables only for real streams.

- Prefer `rxjs` + `@react-rxjs/core`.
- ❌ manual `subscribe()` inside components.

---

## 12) Memoization

**Rule**: `React.memo` is allowed **only if ALL apply**:

- component is pure
- parent rerenders frequently
- render is expensive or list is large
- props are stable

Memo must include a **1‑line justification comment**.

---

## 13) React 19 / Concurrency

**Rule**: Rendering is interruptible.

- ❌ side‑effects during render.
- ❌ assumptions about render count.
- ✅ effects must be idempotent.

---

## 14) Mechanical Check (Fast)

Before accepting a change:

- Unstable identities passed down?
- Inline callbacks in memoized trees?
- Volatile context values?
- Index used as key?
- `useEffect` computing UI state?
- `React.memo` without justification?

If **any YES**, refactor.

---

**Default AIDD contract. Escalate to v2 only when necessary.**

