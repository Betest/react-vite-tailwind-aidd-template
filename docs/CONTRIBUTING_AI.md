#AI & Human Contribution Guidelines

Estas reglas aplican tanto a contribuciones humanas como asistidas por LLM.

1. Principios no negociables

KISS: la solución más simple que funcione.

DRY (rule of 3): no abstraer antes de ver el mismo patrón 3 veces.

Clean Code: nombres claros, componentes pequeños, flujo predecible.

Minimal diff: no cambios colaterales.

No behavior change salvo que se solicite explícitamente.

2. Restricciones del stack (hard rules)
Permitido

React 19 (hooks + functional components)

TypeScript (tipado explícito, sin any implícito)

Vite

TailwindCSS

lucide-react para TODOS los iconos y logos

Prohibido (salvo pedido explícito)

UI frameworks / design systems

Otras librerías de iconos

CSS-in-JS o theming libs

State/query libs adicionales

3. Checklist de PR (obligatorio)

Antes de aprobar o mergear:

Arquitectura & diseño

 Cada componente/hook tiene una sola responsabilidad (SRP)

 No hay abstracciones prematuras

 Se usa composición antes que jerarquías complejas

 Si se usó un patrón, su beneficio es claro y justificado

Código

 Tipos explícitos y legibles

 Componentes pequeños (< ~150 líneas idealmente)

 No lógica compleja en JSX

 No duplicación innecesaria

UI & estilo

 TailwindCSS únicamente

 Clases agrupadas y legibles

 Iconos solo desde lucide-react

Verificación

 El build pasa (npm run build)

 No se afirma que algo funciona sin evidencia (logs/output)

4. Uso de patrones de diseño (guía práctica)

Los patrones NO son obligatorios. Úsalos solo si reducen complejidad.

Patrones aceptados

Composition (default)

Custom Hooks (useX) para lógica reutilizable

Container / Presentational si el componente crece demasiado

Adapter para aislar APIs/IO

Strategy para comportamientos intercambiables

Reducer (useReducer) para estados complejos

Regla de oro

Si no puedes explicar el beneficio del patrón en una frase, no lo uses.

5. Guía de hooks (anti-bugs)

useState para estado simple

useReducer solo si hay transiciones complejas

useEffect:

❌ No para estado derivado

❌ No para lógica principal

✅ Solo para sincronización externa (IO, timers)

Extraer a hook solo si:

Se reutiliza

Mejora legibilidad

## Rendimiento & re-renders (pragmático)

### No es “evitar props”
- Props son normales. Lo importante es evitar:
  - **Prop drilling** (pasar props por muchas capas sin necesidad)
  - **Props inestables** (nuevos objetos/funciones por render sin necesidad)

### Reglas
- Preferir **estado local** cuando solo afecta un componente.
- No “levantar estado” si solo causa re-renders en cascada.
- Dividir componentes grandes para aislar re-renders.
- Pasar **primitivos** y referencias estables cuando sea relevante.
- Usar memoización **solo si hay un beneficio claro**:
  - `React.memo` para componentes puros costosos con props estables
  - `useMemo` para cómputos costosos
  - `useCallback` para handlers que se pasan a hijos memoizados
- Evitar “memo spam” (memoizar todo sin evidencia).

### Listas
- Keys estables (no index si hay reordenamiento o inserciones).
- Evitar crear componentes inline dentro de `.map()` si se vuelve confuso o costoso.

### Context
- No meter valores que cambian frecuentemente en un Context global.
- Si es necesario, **split de context** o mover el estado más cerca.

### Effects
- `useEffect` solo para sincronización externa (IO/timers/subscriptions).
- Dependencias correctas; no silenciar `exhaustive-deps` sin justificación.


6. Convenciones de componentes

Props pequeñas y enfocadas

Evitar boolean props ambiguas (isEnabled, flag)

Preferir enums/unions cuando aplique

No exponer detalles internos vía props

7. Disciplina agentica (LLM)

Cuando un LLM trabaja en este repo:

Protocolo obligatorio

Plan (máx. 4 bullets)

Una acción

Un patch o

Un comando solicitado

Next check

Reglas

❌ No inventar outputs (build, browser, tests)

❌ No instalar dependencias nuevas

❌ No refactors masivos

⛔ Máx. 3 iteraciones fallidas

Luego: resumir evidencia y proponer opciones

8. Señales de over-engineering (red flags 🚨)

Más archivos que antes sin reducción clara de complejidad

Abstracciones usadas una sola vez

“Preparado para el futuro” sin requerimiento actual

Patrones sin beneficio explícito

Lógica difícil de seguir sin comentarios

Si ves alguno → simplifica.

9. Plantilla de request recomendada (para humanos y LLM)
Goal: <qué se quiere lograr>
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
- Provide next check (build/dev)

10. Regla final

La mejor solución es la que otro dev puede entender en 5 minutos sin contexto previo.