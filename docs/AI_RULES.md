# AI_RULES — Primary Constraints

These rules are **non‑negotiable**.  
If a solution violates any rule below, it is **invalid**, even if it works.

---

## 1) Primary Rendering Authority

- **`RENDERING_RULES_V3.md`** is the **default and primary rendering contract**.
- Agents must follow V3 rules **by default**.
- Escalation to `rendering_rules_react_type_script_mechanical_guide_v_2.md` is allowed **only when ambiguity exists**.

---

## 2) State Ownership

- Server state **must** use TanStack Query.
- Global client state **must** use Zustand or Redux Toolkit.
- Server responses are **forbidden** in global stores.

---

## 3) React Safety

- No side‑effects during render.
- No assumptions about render count.
- All effects must be idempotent.

---

## 4) Identity Stability

- Inline `{}` / `[]` / `() => {}` passed to memoized children are forbidden.
- Volatile values in broad context providers are forbidden.

---

## 5) Forms

- Forms **must** use React Hook Form.
- Schema validation is mandatory.
- Field‑level `useState` is forbidden unless explicitly justified.

---

## 6) TypeScript

- `any` is forbidden.
- Unsafe casts are forbidden.
- Prefer inference, narrowing, discriminated unions.

---

## 7) Feature Boundaries

- Deep imports from feature internals are forbidden.
- Features communicate only through public APIs (`index.ts`).

---

## 8) Conflict Resolution

If documents conflict, the order of authority is:

1. `AI_RULES.md`
2. `RENDERING_RULES_V3.md`
3. `CODING_STANDARDS.md`
4. `ENGINEERING_PRINCIPLES.md`

---

**Violations must be reported explicitly.**

