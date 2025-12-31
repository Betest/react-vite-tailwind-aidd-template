# PR Checklist

## Funcionalidad
- [ ] Cumple el objetivo solicitado
- [ ] No cambia comportamiento no solicitado
- [ ] Maneja estados básicos (loading / empty / error si aplica)

## Código
- [ ] Componentes pequeños y legibles
- [ ] Tipos explícitos (no any implícito)
- [ ] No duplicación innecesaria
- [ ] No abstracciones prematuras

## UI
- [ ] TailwindCSS únicamente
- [ ] Clases legibles y agrupadas
- [ ] Iconos solo desde lucide-react

## Calidad
- [ ] KISS primero
- [ ] DRY solo si hay repetición real (rule of 3)
- [ ] Patrones usados solo si reducen complejidad

## Performance (when relevant)
- [ ] No prop drilling innecesario
- [ ] No props inestables (objetos/funciones recreadas) sin motivo
- [ ] Memoización usada solo si aporta (no “memo spam”)
- [ ] Keys estables en listas

## Verificación
- [ ] `npm run build` pasa
