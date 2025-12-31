# react-vite-tailwind-aidd-template

> **AI-Driven Development (AIDD) Template** for React 19 + TypeScript + Vite + TailwindCSS.

This repository is not just a starter project. It is a **reference implementation of an AIDD-ready frontend codebase**, designed to work seamlessly with AI agents (Cursor / Trae / Kilo) while enforcing **high engineering standards**.

---

## 🎯 Purpose

This template exists to:

* Serve as a **baseline AIDD project** for modern React applications
* Enforce **deterministic, low-risk changes** by AI agents
* Encode **engineering rules as contracts**, not suggestions
* Reduce token usage while increasing output correctness
* Align humans and AI around the same standards

This repo assumes that **AI will actively modify the codebase**.

---

## 🧠 What makes this different from a normal template

Unlike typical Vite or React templates, this project includes:

* A **document hierarchy** optimized for AI reasoning
* Explicit **authority and escalation rules** for decisions
* Strict separation between:

  * technical constraints
  * rendering rules
  * execution discipline
  * contribution standards
* A mechanical rendering contract compatible with **React 19 concurrency**

---

## 📚 Documentation Map (AIDD)

The repository is governed by the following documents:

### 🔹 Primary Authority (AI-first)

1. **`AI_RULES.md`**
   Hard, non-negotiable technical constraints

2. **`RENDERING_RULES_V3.md`**
   Default rendering & performance contract (low-token, mechanical)

3. **`CODING_STANDARDS.md`**
   Engineering quality and refactoring discipline

4. **`ENGINEERING_PRINCIPLES.md`**
   Architecture, boundaries, ownership rules

### 🔹 Agent Behavior

* **`AGENT_EXECUTION_RULES.md`** — iteration loop, failure limits, execution discipline
* **`AGENT_PROTOCOL.md`** — response structure and output discipline
* **`docs/prompts/frontend_agent_prompt_*.md`** — agent role definition

### 🔹 Human-First References

* `PERFORMANCE_GUIDE.md`
* `CONTRIBUTING_AI.md`
* `DESIGN_PATTERNS.md`
* `REPO_CONTEXT.md`

> See **`INDEX.md`** for the authoritative navigation order.

---

## 🏗️ Tech Stack

* **React 19** (hooks + functional components only)
* **TypeScript** (strict)
* **Vite**
* **TailwindCSS** (utility-first, no CSS-in-JS)
* **lucide-react** for all icons

No additional UI frameworks or state libraries are included by default.

---

## 🤖 AI Usage Model

This repository is designed to be used with AI assistants:

* Cursor
* Trae
* Kilo
* Chat-based agents

The agent must:

* Follow `INDEX.md` for document loading
* Obey `AI_RULES.md` and `RENDERING_RULES_V3.md`
* Apply **minimal diffs** only
* Stop after 3 failed iterations

Any response that violates these rules is considered **non-compliant**.

---

## 🚦 Contribution Model

All contributions (human or AI-assisted) must follow:

* `CONTRIBUTING_AI.md`
* `CODING_STANDARDS.md`
* `AGENT_EXECUTION_RULES.md`

This ensures:

* Predictable reviews
* Low-risk refactors
* Stable long-term evolution

---

## 🧪 Intended Use Cases

* Bootstrap an **AIDD-ready frontend project**
* Use as a **golden reference** for AI-assisted refactors
* Teaching or experimenting with **AI-governed codebases**
* Internal templates for teams adopting AI coding workflows

---

## ⚠️ Non-Goals

This template does **not**:

* Provide a full UI kit or design system
* Optimize for rapid prototyping over correctness
* Hide complexity behind generators or magic

Correctness and discipline are preferred over speed.

---

## ✅ Status

This repository represents:

> **AIDD_BASELINE v1.0**

It is safe to clone, extend, and evolve under AI-driven workflows.

---

## 📌 Final Note

If you remove the documents, this becomes a normal React template.

If you keep them, this becomes an **AI-governed engineering system**.

Choose intentionally.
