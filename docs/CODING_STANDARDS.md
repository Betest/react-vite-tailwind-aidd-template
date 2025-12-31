# CODING_STANDARDS — Engineering Quality Rules

These standards apply to **all code changes**, whether authored by humans or assisted by AI.
They are designed to maximize **clarity, safety, and long-term maintainability** while remaining pragmatic.

---

## 1) General Principles

* **Clarity over cleverness**: readable code is preferred to smart but obscure solutions.
* **Minimal surface change**: do not modify public APIs, props, or contracts unless explicitly requested.
* **Small units**: functions, hooks, and components should be small, focused, and testable.
* **Predictability**: code flow should be easy to follow without hidden side-effects.

---

## 2) Error Handling

* **Fail fast**: surface errors as early as possible.
* **Be explicit**: error messages should clearly describe what went wrong.
* **Preserve contracts**: existing error types, messages, and semantics must not change unless explicitly requested.
* **No silent failures**: swallowing errors without handling or reporting is forbidden.

---

## 3) Testing Standards

* **Tests are required** for:

  * new behavior
  * bug fixes
  * refactors that change internal logic

* **Prefer unit tests** for pure logic (utilities, reducers, schemas).

* **Use integration tests** when behavior spans multiple layers.

* **Tests must be deterministic**:

  * no reliance on timing, randomness, or external state
  * mocks and fixtures must be explicit

---

## 4) Refactoring Discipline

Refactors must be **incremental and controlled**:

1. Add or update tests (when tests exist)
2. Refactor internal implementation
3. Preserve public APIs and observable behavior

Rules:

* ❌ No large rewrites disguised as refactors
* ❌ No stylistic-only refactors
* ✅ Each refactor step must compile and be reviewable

---

## 5) Code Review Expectations

Before submitting or approving changes:

* The change solves the stated problem and nothing more
* The diff is minimal and focused
* Naming is clear and consistent with existing code
* Edge cases are considered or explicitly deferred

---

## 6) AI-Assisted Contributions

When code is generated or modified with AI assistance:

* The output must follow these standards exactly
* Assumptions must be stated explicitly
* If unsure, prefer asking **one targeted question** rather than guessing

---

## 7) Final Rule

> A correct solution is one that another engineer can understand and safely modify **within minutes**, without additional context.

---

**This document is authoritative for coding quality and review decisions.**
