---
description: Pasa una idea por el Filtro, enseña veredicto y plan, y si apruebas ejecuta el flujo completo hasta Revisor y Lecciones
argument-hint: <tu idea>
---

Idea de Blake: $ARGUMENTS

Actúas como **Conductor** (ver `CLAUDE.md`). Un subagente no puede lanzar a otros: tú lanzas a cada uno en su orden. Sigue estos pasos:

1. **Lee** `LECCIONES.md` y `DECISIONES.md`. Si `$ARGUMENTS` está vacío, pregunta a Blake cuál es la idea.
2. **Filtro.** Lanza el subagente `filtro` con la idea. Debe evaluarla (Fase 1), registrarla en `IDEAS.md` y, si el veredicto es *adelante*, enrutarla (Fase 2) dejando el plan en `TABLERO.md`. Si la idea es de riesgo alto (dinero, marca, VIP, despliegue), lánzalo con `model: opus`.
3. **Enséñale a Blake** el veredicto y, si lo hay, el plan: agentes, orden, patrón, modelos y dependencias, en pocas líneas. **Para aquí y espera su respuesta.**
   - *Descartar / aparcar:* confirma con Blake y cierra.
   - *Preguntar:* hazle la pregunta concreta y vuelve al paso 2 con su respuesta.
   - *Adelante:* sigue solo si Blake aprueba (también si pide cambios en el plan).
4. **Ejecuta el plan** de `TABLERO.md` en su orden. Antes de cada agente: marca la tarea *en curso*, apúntalo en `ACTIVIDAD.md` (sección "En ejecución ahora") y dile a Blake en una línea qué agente lanzas, con qué modelo y por qué, pásale solo el contexto necesario y su nota de `TRASPASOS/`. Máximo **3 agentes en paralelo**. Tras cada agente, pasa su bloque "Decisiones y motivo" al histórico de `ACTIVIDAD.md`, quítalo de "En ejecución ahora", actualiza el estado de la idea en `IDEAS.md` y comprueba que ha dejado traspaso, memoria y línea en `REGISTRO.md`. Pregunta a Blake antes de cualquier gasto, publicación, borrado, despliegue, cambio en Supabase o activación de Make.
5. **Revisor.** Lanza `revisor` con modelo **igual o superior** al del ejecutor. Si devuelve: reenvía al ejecutor (escalando un nivel de modelo si el Revisor lo indica). **Máximo 3 rondas**; si no hay visto bueno, escala a Blake con el resumen.
6. **Lecciones.** Con el visto bueno (o tras escalar), lanza `lecciones` para convertir los fallos en reglas y revisar el enrutado de modelos con `REGISTRO.md`.
7. **Cierra:** marca la tarea *hecha* en `TABLERO.md` y resume a Blake en pocas líneas qué se hizo, qué entregables hay y qué decisiones quedan pendientes. Registra en `DECISIONES.md` lo que Blake haya decidido.

Terminado = Revisor con visto bueno y entregable que cumple lo pedido.
