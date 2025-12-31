# Rendering Rules — React + TypeScript (Mechanical Guide v2)

> **Goal:** minimize accidental rerenders and rendering cascades **without** falling into “props fear”.  
> **Rule of thumb:** optimize only where it matters, but prevent the most common mistakes **by default**.

This guide is **mechanical**, **enforceable**, and **LLM-friendly**. It is intended to be used as:
- A coding standard
- A PR review reference
- A mental model for React 18/19
- A base document for AI agents

---

## 0) Definitions (LLM‑friendly, TS‑aware)

**Stable value**  
A primitive (`string | number | boolean`) or a reference whose identity does **not** change between renders.

**Unstable value**  
Objects, arrays, or functions created inline (`{}`, `[]`, `() => {}`) that produce a new identity on every render.

**Client State**  
Local or global UI state (filters, toggles, modals, drafts).

**Server State**  
Remote, async, cacheable data (API responses).

**Volatile context**  
A Context provider value that changes frequently (mouse position, timers, websocket ticks).

**Prop drilling**  
Passing props through **2+ layers** that do not use them.

---

## 1) Golden Rules (Mechanical)

1. ✅ Props are OK — **avoid prop drilling** and **avoid unstable props**.
2. ✅ Keep state **as local as possible**, but **never duplicate state**.
3. ✅ Split components so **only the changing piece rerenders**.
4. ✅ Memoize **selectively** (no memo spam):
   - `React.memo` → only for expensive, pure components with stable props.
   - `useMemo` → only for expensive calculations or to stabilize values passed to memoized children.
   - `useCallback` → only when handler identity matters.
5. ✅ Context values must be **stable**.
6. ❌ Do **NOT** put fast‑changing values in broad context.
7. ✅ Lists must use **stable keys**.
8. ✅ `useEffect` is for **external synchronization only**.

---

## 2) Inline Objects / Arrays in JSX

❌ **Not allowed** — inline object/array passed to a child (unstable identity)

```tsx
<Chart options={{ stacked: true, smooth: true }} />
<List items={[...items].sort(sortFn)} />
```

✅ **Allowed** — constant outside component

```tsx
const CHART_OPTIONS = { stacked: true, smooth: true } as const;

export function Screen() {
  return <Chart options={CHART_OPTIONS} />;
}
```

✅ **Allowed** — `useMemo` ONLY if needed

```tsx
export function Screen({ stacked }: { stacked: boolean }) {
  const options = useMemo(() => ({ stacked, smooth: true }), [stacked]);
  return <Chart options={options} />;
}
```

✅ **Allowed** — inline object used locally only

```tsx
export function Screen() {
  const style = { display: 'flex' }; // OK if not passed down
  return <div style={style}>...</div>;
}
```

---

## 3) Inline Callbacks / Handlers

❌ **Not allowed** — inline arrow passed to memoized child

```tsx
const Item = memo(({ onClick }: { onClick: () => void }) => ...);
<Item onClick={() => doThing(id)} />
```

✅ **Allowed** — inline callback if child is NOT memoized and list is small

```tsx
<Item onClick={() => doThing(id)} />
```

✅ **Allowed** — stable handler with `useCallback`

```tsx
export function Screen({ id }: { id: string }) {
  const onClick = useCallback(() => doThing(id), [id]);
  return <Item onClick={onClick} />;
}
```

✅ **Preferred list pattern** — pass primitive + stable handler

```tsx
const Item = memo(
  ({ id, onClickId }: { id: string; onClickId: (id: string) => void }) => (
    <button onClick={() => onClickId(id)}>Open</button>
  )
);
```

---

## 4) Prop Drilling vs Composition

❌ **Not allowed** — passing props through layers that don’t need them

```tsx
<App user={user}>
  <Layout user={user}>
    <Header user={user} />
  </Layout>
</App>
```

✅ **Allowed** — composition via slots / children

```tsx
<Layout header={<Header user={user} />}>
  <Content />
</Layout>
```

✅ **Allowed** — local context for small subtrees

```tsx
const UserCtx = createContext<User | null>(null);
```

---

## 5) Context Volatility (High‑Impact Rule)

❌ **Not allowed** — volatile values in broad context

```tsx
<UiContext.Provider value={{ mouseX, mouseY, now: Date.now() }}>
  <WholeApp />
</UiContext.Provider>
```

✅ **Allowed** — split contexts by volatility

```tsx
<ThemeContext.Provider value={theme}>
  <AuthContext.Provider value={auth}>
    <WholeApp />
  </AuthContext.Provider>
</ThemeContext.Provider>
```

---

## 6) Lists & Keys

❌ Index as key when list can reorder

```tsx
items.map((it, idx) => <Row key={idx} />)
```

✅ Stable unique key

```tsx
items.map((it) => <Row key={it.id} />)
```

---

## 7) Effects (`useEffect`)

❌ **Not allowed** — computing derived UI state

```tsx
useEffect(() => setFullName(first + ' ' + last), [first, last]);
```

✅ **Allowed** — derive during render

```tsx
const fullName = `${first} ${last}`;
```

✅ **Allowed** — external sync only

```tsx
useEffect(() => {
  const id = setInterval(refresh, 10_000);
  return () => clearInterval(id);
}, [refresh]);
```

---

## 8) State Ownership & Shape

### Local State
- Local to a component or hook

### Global Client State
- **Zustand / RTK** only
- UI, auth, preferences

### Server State
- **TanStack Query only**
- Caching, retries, background refresh

❌ Do NOT mix server data into global stores

---

## 9) Forms (React Hook Form)

❌ **Not allowed** — `useState` per field

✅ **Required** — React Hook Form + schema validation

```tsx
const form = useForm<FormValues>({ resolver: zodResolver(schema) });
```

---

## 10) Custom Hooks

Create a hook when:
- Logic is reused
- Side‑effects exist
- Multiple hooks are composed

Rules:
- Stable return API
- Typed generics
- No hidden side‑effects

---

## 11) Observables & Streams

Preferred:
- `rxjs`
- `@react-rxjs/core`

❌ Do NOT subscribe manually in components

---

## 12) Memoization Rules (No Memo Spam)

Use `React.memo` **only if ALL apply**:
- Component is pure
- Parent rerenders often
- Render is expensive or list is large
- Props are stable

```tsx
// memo: rows list (500+), stable props
export const Row = memo(function Row() { ... });
```

---

## 13) React 19 / Concurrent Rendering Rules

- Rendering is interruptible
- Components may render multiple times before commit

Rules:
- ❌ No side‑effects during render
- ❌ No assumptions about render count
- ✅ Effects must be idempotent

---

## 14) Mechanical Review Checklist (PR / LLM)

Before merging:

- [ ] Any `{}` / `[]` / `() => {}` passed to a child?
- [ ] Inline callbacks passed to memoized children?
- [ ] Volatile context values?
- [ ] Index used as key?
- [ ] `useEffect` computing UI state?
- [ ] `React.memo` without justification?

If **any answer is YES**, refactor before merge.

---

## 15) React 19 APIs (Practical Usage)

### `use()` for async boundaries

✅ Use `use()` only inside Server Components or framework-managed boundaries.

```ts
const data = use(fetchResource());
```

Rules:
- ❌ Never call `use()` conditionally
- ❌ Never wrap `use()` in try/catch inside render

---

### `useOptimistic()`

Use for optimistic UI tied to server mutations.

```ts
const [optimisticItems, addOptimistic] = useOptimistic(items, (state, item) => [...state, item]);
```

Rules:
- Must be idempotent
- Must be reversible

---

### `useTransition()`

```ts
const [isPending, startTransition] = useTransition();
```

Rules:
- Use for non-urgent state updates
- Never rely on `isPending` for business logic

---

### `cache()`

```ts
const getUser = cache(async (id: string) => fetchUser(id));
```

Rules:
- Pure functions only
- No side effects

---

**End of guide — enforceable standard.**

