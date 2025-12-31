# INDEX — AI‑Driven Development (AIDD)

This document defines **how AI agents and humans should navigate the documentation** in this repository.

It is the **entry point** for Cursor / Trae / Kilo and for contributors.

---

## 1) Default Reading Order (AI Agents)

When solving a task, follow this order **strictly**:

1. **`RENDERING_RULES_V3.md`**  
   → Default rendering & React contract (low token, mechanical)

2. **`AI_RULES.md`**  
   → Hard constraints that must never be violated

3. **`CODING_STANDARDS.md`**  
   → TypeScript, ESLint, forms, testing rules

4. **`ENGINEERING_PRINCIPLES.md`**  
   → Architecture, ownership, feature boundaries

5. **`FRONTEND_AGENT_PLAYBOOK.md`**  
   → Philosophy, trade‑offs, long‑term direction

Escalate **only if needed**:

- **`rendering_rules_react_type_script_mechanical_guide_v_2.md`**  
  → Canonical spec when ambiguity exists

---

## 2) Human‑First Documents

These are optimized for **human reading**, not default AI loading:

- `PERFORMANCE_GUIDE.md` (ultra‑short reference)
- `DESIGN_PATTERNS.md`
- `CONTRIBUTING_AI.md`
- `REPO_CONTEXT.md`

---

## 3) Prompt & Protocol Documents

| File | Responsibility |
|---|---|
| `docs/prompts/frontend_agent_prompt_*.md` | Agent role & behavior |
| `AGENT_EXECUTION_RULES.md` | Iteration loop, failure limits, execution discipline |
| `AGENT_PROTOCOL.md` | Response format & structural discipline |
| `system-prompt.md` | System-level constraints |
| `user-prompt.md` | User input normalization |

---

## 4) Decision Heuristics (AI)

- Rendering / performance issue → **V3 first**
- State ownership ambiguity → `ENGINEERING_PRINCIPLES.md`
- Forms / validation → `CODING_STANDARDS.md`
- Deep React behavior → escalate to **v2**

---

## 5) Single Source of Truth

- **Rendering rules** → `RENDERING_RULES_V3.md`
- **Hard constraints** → `AI_RULES.md`
- **Architecture** → `ENGINEERING_PRINCIPLES.md`

If documents conflict:

> `AI_RULES.md` > `RENDERING_RULES_V3.md` > others

---

**This index is authoritative for AIDD navigation.**

