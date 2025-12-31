# Design Patterns (Use Only When Justified)

## Preferred patterns
- Composition: build UI via small components.
- Container/Presentational: split stateful vs presentational if complexity grows.
- Custom Hook: reuse stateful logic with clear API (useX()).
- Adapter: isolate API/IO and map DTO ↔ UI models.
- Strategy: switch behavior via injected function/object (formatters/validators).
- Reducer: useReducer for complex state transitions.

## Avoid
- Over-abstraction, unnecessary layers, premature “frameworks”.
- Patterns that add indirection without reducing complexity.
