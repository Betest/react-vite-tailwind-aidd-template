# CONTRIBUTING_AI — AI & Human Contribution Guidelines

These rules apply to **both human contributors and LLM-assisted contributions**.
They are **enforceable**, **pragmatic**, and optimized for **AI‑Driven Development (AIDD)**.

---

## 1) Non‑Negotiable Principles

* **KISS**: the simplest solution that works comes first.
* **DRY (rule of three)**: do not abstract until the same pattern appears at least three times.
* **Clean Code**: clear names, small components, predictable flow.
* **Minimal diff**: no collateral or unrelated changes.
* **No behavior changes** unless explicitly requested.

---

## 2) Stack Constraints (Hard Rules)

### Allowed

* React 19 (hooks + functional components only)
* TypeScript (explicit typing, no implicit `any`)
* Vite
* TailwindCSS
* `lucide-react` for **all** icons and logos

### Forbidden (unless explicitly requested)

* UI frameworks / design systems
* Additional icon libraries
* CSS‑in‑JS or theming libraries
* Additional state or query libraries

---

## 3) Pull Request Checklist (Mandatory)

Before approval or merge:

### Architecture & Design

* Each component or hook has a **single responsibility (SRP)**
* No premature abstractions
* Composition is preferred over complex hierarchies
* If a design pattern is used, its benefit is **clear and justified**

### Code Quality

* Explicit, readable types
* Small components (≈150 LOC or less when possible)
* No complex logic inside JSX
* No unnecessary duplication

### UI & Styling

* TailwindCSS only
* Class names are grouped and readable
* Icons exclusively from `lucide-react`

### Verification

* Build passes (`npm run build`)
* No claim that something works without evidence (logs / output)

---

## 4) Design Patterns (Practical Guidance)

Patterns are **not mandatory**. Use them **only if they reduce complexity**.

### Accepted Patterns

* Composition (default)
* Custom Hooks (`useX`) for reusable logic
* Container / Presentational split when complexity justifies it
* Adapter for isolating APIs or IO
* Strategy for interchangeable behaviors
* Reducer pattern (`useReducer`) for complex state transitions

**Golden rule**:
If you cannot explain the benefit of the pattern in **one sentence**, do not use it.

---

## 5) Hooks Usage Guidelines (Anti‑Bug Rules)

* `useState` for simple state
* `useReducer` only for complex transitions

### `useEffect`

* ❌ Not for derived state
* ❌ Not for core business logic
* ✅ Only for external synchronization (IO, timers, subscriptions)

Extract logic into a custom hook **only if**:

* It is reused
* It improves readability

---

## 6) Performance & Re‑Renders (Pragmatic)

### This is NOT about “avoiding props”

Props are normal. Avoid instead:

* **Prop drilling** (passing props through unnecessary layers)
* **Unstable props** (new objects/functions created per render without need)

### Rules

* Prefer **local state** when it affects only one component
* Do not lift state if it causes cascading re‑renders
* Split large components to isolate re‑renders
* Prefer **primitives and stable references** when relevant
* Use memoization **only when there is a clear benefit**:

  * `React.memo` for expensive pure components with stable props
  * `useMemo` for expensive computations
  * `useCallback` for handlers passed to memoized children
* Avoid **memo spam** (memoizing everything without evidence)

### Lists

* Use stable keys (never index keys if reorder/insert/remove is possible)
* Avoid inline component definitions inside `.map()` when they reduce clarity or performance

### Context

* Do not put frequently‑changing values into global Context
* Split Contexts or move state closer when necessary

### Effects

* `useEffect` only for external synchronization
* Dependencies must be correct; do not silence `exhaustive-deps` without justification

---

## 7) Component Conventions

* Small, focused props
* Avoid ambiguous boolean props (`isEnabled`, `flag`)
* Prefer enums or union types when appropriate
* Do not expose internal details via props

---

## 8) Agent Discipline (LLMs)

When an LLM works in this repository:

### Mandatory protocol

1. Plan (max 4 bullets)
2. One action

   * one patch **or**
   * one requested command
3. Next check

### Rules

* ❌ Do not invent outputs (builds, browser behavior, tests)
* ❌ Do not install new dependencies
* ❌ No massive refactors
* ⛔ Maximum of **3 failed iterations**

After 3 failures:

* Summarize evidence
* Propose options

---

## 9) Over‑Engineering Signals (🚨 Red Flags)

* More files without a clear reduction in complexity
* Abstractions used only once
* “Future‑proofing” without a current requirement
* Patterns with no explicit benefit
* Logic that is hard to follow without comments

If you see any of these → **simplify**.

---

## 10) Recommended Request Template (Humans & LLMs)

```text
Goal: <what you want to achieve>

Constraints:
- React hooks only
- TailwindCSS only
- lucide-react for icons/logos
- No new packages

Quality:
- KISS first, DRY after rule-of-3
- SOLID where it reduces coupling

Verification:
- Minimal diff
- Provide next check (build / dev)
```

---

## 11) Final Rule

The best solution is the one **another developer can understand in 5 minutes without prior context**.

---

**This document is authoritative for both human and AI contributions.**
