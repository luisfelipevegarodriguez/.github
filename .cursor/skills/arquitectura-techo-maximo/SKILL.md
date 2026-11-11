---
name: arquitectura-techo-maximo
description: >
  Resume la arquitectura actual de un sistema o repositorio y la eleva al techo
  máximo de calidad (claridad, escalabilidad, resiliencia, seguridad y
  mantenibilidad). Usa esta habilidad siempre que el usuario pida resumir
  arquitectura, elevar arquitectura, techo máximo, architecture review,
  architecture summary, mejorar diseño de sistema, auditar arquitectura,
  proponer target architecture, o quiera pasar de un diseño actual a uno
  ideal/best-in-class — aunque no diga explícitamente "techo máximo".
---

# Arquitectura a techo máximo

Convierte una arquitectura real (código, docs, diagramas o descripción) en un
resumen claro y en un plan concreto para llevarla al **techo máximo**: el mejor
diseño viable para el contexto del producto, no un overengineering genérico.

## Objetivo

1. **Resumir** la arquitectura actual con precisión y sin ruido.
2. **Elevar** esa arquitectura hasta el techo máximo: estado objetivo + gaps +
   secuencia de cambios con impacto.

## Entradas

Usa lo que haya disponible, en este orden de preferencia:

1. Código y estructura del repo (árbol, módulos, APIs, deps, infra).
2. Documentación existente (`README`, ADRs, diagramas, runbooks).
3. Descripción verbal del usuario o archivos adjuntos.
4. Si falta contexto crítico (escala, SLOs, presupuesto, equipo), declara
   supuestos explícitos y sigue; no bloquees el resumen.

## Flujo de trabajo

### 1. Explorar

- Identifica límites del sistema, actores, flujos principales y dependencias.
- Detecta capas (UI, API, dominio, datos, jobs, infra) y acoplamientos.
- Localiza riesgos: single points of failure, secrets, deuda estructural,
  inconsistencias de ownership, falta de observabilidad.

### 2. Resumir (estado actual)

Produce un resumen corto y accionable. Evita listas interminables de archivos.

### 3. Definir el techo máximo

El techo máximo es el mejor diseño **viable** para este contexto:

- Cumple requisitos actuales y próximos 1–2 horizontes de crecimiento.
- Reduce riesgo operacional y de cambio.
- Es implementable por el equipo sin reescritura gratuita.
- Prefiere principios comprobados (boundaries claros, contratos estables,
  idempotencia, fallos controlados, observabilidad) sobre moda tecnológica.

No inventes microservicios, event meshes o plataformas si el problema no lo
exige. El techo máximo puede ser un monolito modular bien cortado.

### 4. Elevar

Compara actual vs techo máximo, prioriza gaps por riesgo × valor, y propone una
secuencia incremental (no un big-bang).

## Formato de salida (obligatorio)

Usa exactamente estas secciones:

```markdown
# Arquitectura: resumen y techo máximo

## 1. Resumen ejecutivo
- Qué es el sistema (1–3 frases)
- Nivel de madurez arquitectónica (bajo / medio / alto) y por qué
- Veredicto en una frase: qué bloquearía el techo máximo hoy

## 2. Arquitectura actual
### Vista de contexto
- Actores, sistemas externos, límites de confianza

### Componentes y responsabilidades
- Tabla o bullets: componente → responsabilidad → owner implícito

### Flujos críticos
- 2–5 flujos end-to-end (request/data path)

### Decisiones y trade-offs visibles
- Qué se priorizó hoy (velocidad, costo, simplicidad, etc.)

## 3. Techo máximo (arquitectura objetivo)
### Principios guía
- 4–7 principios concretos para ESTE sistema

### Diseño objetivo
- Componentes, boundaries, contratos, datos, despliegue, observabilidad

### Criterios de techo máximo
Checklist verificable, por ejemplo:
- [ ] Boundaries claros y dependencias unidireccionales
- [ ] Contratos versionados / APIs estables
- [ ] Datos con ownership y migraciones seguras
- [ ] Fallos acotados (timeouts, retries, circuit breakers donde aplique)
- [ ] Observabilidad: logs + métricas + traces en caminos críticos
- [ ] Seguridad: authn/z, secrets, least privilege
- [ ] Capacidad de evolucionar sin reescritura

## 4. Gaps (actual → techo máximo)
Tabla: gap | impacto | esfuerzo | riesgo si no se hace

## 5. Plan de elevación
Ordenado en fases cortas:
### Fase 0 — estabilizar
### Fase 1 — boundaries y contratos
### Fase 2 — resiliencia y datos
### Fase 3 — escala y excelencia operativa
Cada fase: objetivo, cambios concretos, resultado observable.

## 6. Primeros 3 movimientos
Los 3 cambios de mayor apalancamiento para empezar YA.
```

## Reglas de calidad

- Sé específico al repo/sistema; evita consejos genéricos (“usa clean architecture”).
- Nombra módulos, servicios o rutas reales cuando existan.
- Distingue hechos observados de supuestos.
- Si el alcance es enorme, resume por dominios y eleva el dominio más crítico primero.
- Si el usuario solo pide “resumir”, igual incluye un techo máximo breve (sección 3) y
  3 movimientos; si solo pide “elevar”, igual empieza con un resumen corto (sección 1–2).
- Responde en el idioma del usuario.

## Anti-patrones a evitar

- Reescribir todo desde cero sin evidencia.
- Recomendar tecnologías nuevas sin mapearlas a un gap real.
- Diagramas bonitos sin plan de migración.
- “Mejores prácticas” abstractas sin checklist verificable.
- Confundir techo máximo con complejidad máxima.

## Ejemplo rápido

**Input:** “Resume y eleva la arquitectura de este API monolítico Node + Postgres.”

**Output esperado:** resumen del monolito y flujos; techo máximo como monolito
modular con módulos de dominio, cola para jobs, migraciones seguras y
observabilidad; gaps priorizados; fases; 3 movimientos (p. ej. separar
dominios por carpetas/paquetes, introducir outbox, añadir tracing en rutas
críticas).
