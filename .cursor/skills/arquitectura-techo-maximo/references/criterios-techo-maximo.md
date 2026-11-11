# Criterios de techo máximo (referencia)

Carga este archivo solo cuando necesites afinar el checklist del techo máximo
o justificar por qué un diseño es o no “techo máximo” en un dominio concreto.

## Dimensiones

| Dimensión | Pregunta clave | Señal de techo máximo |
| --- | --- | --- |
| Claridad | ¿Un ingeniero nuevo entiende el mapa en <30 min? | Boundaries y ownership explícitos |
| Evolución | ¿Se puede cambiar un dominio sin romper otros? | Contratos estables, acoplamiento bajo |
| Datos | ¿Quién es dueño de cada dato y cómo migra? | Ownership + migraciones reversibles/seguras |
| Resiliencia | ¿Qué pasa si falla una dependencia? | Timeouts, degradación controlada, reintentos idempotentes |
| Seguridad | ¿Least privilege de punta a punta? | Authn/z, secrets, superficie mínima |
| Operación | ¿Se diagnostica un incidente en minutos? | Logs/métricas/trazas en caminos críticos |
| Entrega | ¿Se despliega con confianza frecuente? | CI, migraciones, rollback/feature flags |
| Costo/complejidad | ¿La complejidad paga por sí misma? | Sin plataformas innecesarias |

## Heurísticas de elevación

1. **Primero boundaries, luego infra.** Cortar dominios mal mezclados suele
   valer más que añadir un bus de eventos.
2. **Contratos antes que frameworks.** Una API/evento estable supera un
   rewrite de stack.
3. **Observabilidad antes que optimización prematura.** No escales lo que no
   puedes medir.
4. **Un dueño por dato.** Evita tablas/colecciones huérfanas o compartidas sin
   reglas.
5. **Idempotencia en todo lo asíncrono.** Jobs, webhooks y consumidores deben
   tolerar reentrega.
6. **Degradación explícita.** Define qué se apaga primero bajo presión.

## Señales de overengineering (no es techo máximo)

- Microservicios para un equipo pequeño sin límites de despliegue reales.
- Event-driven total sin consumidores claros ni esquemas versionados.
- Multi-región/CQRS/Kafka “por si acaso”.
- Capas abstractas sin un segundo implementador.
- Plataforma interna antes de product-market fit técnico.

## Plantilla corta de gap

```text
Gap: <qué falta>
Hecho observado: <evidencia en repo/docs>
Impacto: alto|medio|bajo
Esfuerzo: S|M|L
Movimiento: <cambio concreto>
Resultado observable: <cómo se verifica>
```
