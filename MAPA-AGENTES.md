# MAPA-AGENTES

Actualizado: 2026-10-12. Todos los agentes leen al empezar `CLAUDE.md`, `LECCIONES.md`, `DECISIONES.md` y su `memoria/<agente>.md`, y escriben al terminar su memoria + `REGISTRO.md`. Las fichas de rama son borradores hasta que Blake aporte las instrucciones de sus Proyectos. Skills: ninguna instalada todavía (ver `SKILLS.md`).

## Enrutado de modelos
- **Haiku:** buscar, formatear, renombrar, resumir logs, extraer datos, clasificar.
- **Sonnet:** redactar, editar, código normal, tests.
- **Opus:** arquitectura, bugs difíciles, revisión final, dinero, marca, clientela VIP.
- Empezar por el más barato razonable; subir un nivel solo si el Revisor rechaza. Revisor ≥ ejecutor. A los baratos, solo el contexto necesario.

## Transversales

### Filtro (`filtro`)
- **Produce:** veredicto de cada idea (`IDEAS.md`) y plan de ejecución (`TABLERO.md`).
- **Necesita de otros:** nada; consulta `IDEAS.md`, `DECISIONES.md`, este mapa.
- **Suele pasar a:** Conductor → Blake (aprobación) → agentes del plan.
- **Skills que usa:** ninguna aún.
- **Lee al empezar:** `CLAUDE.md`, `LECCIONES.md`, `DECISIONES.md`, `IDEAS.md`, `MAPA-AGENTES.md`, su memoria.
- **Escribe al terminar:** `IDEAS.md`, `TABLERO.md`, `REGISTRO.md`, su memoria.
- **Modelo por defecto:** Sonnet (Opus si riesgo alto).

### Revisor (`revisor`)
- **Produce:** visto bueno o devolución con lista de fallos; entradas en `LECCIONES.md`.
- **Necesita de otros:** el entregable, la petición original y el traspaso.
- **Suele pasar a:** el ejecutor (si devuelve) o Lecciones (si cierra).
- **Skills que usa:** ninguna aún.
- **Lee al empezar:** `CLAUDE.md`, `LECCIONES.md`, `DECISIONES.md`, `CONTEXTO/negocio.md`, `TABLERO.md`, traspaso, su memoria.
- **Escribe al terminar:** `LECCIONES.md`, `TABLERO.md`, `REGISTRO.md`, su memoria.
- **Modelo por defecto:** igual o superior al del ejecutor (Sonnet mínimo; Opus en dinero, marca y VIP).

### Lecciones (`lecciones`)
- **Produce:** reglas claras, ajustes del enrutado de modelos, consolidación mensual de memorias.
- **Necesita de otros:** `LECCIONES.md` y `REGISTRO.md` rellenados por Revisor y ejecutores.
- **Suele pasar a:** Blake (propuestas de cambio de modelo), todos los agentes (reglas nuevas).
- **Skills que usa:** ninguna aún.
- **Lee al empezar:** `CLAUDE.md`, `LECCIONES.md`, `REGISTRO.md`, `DECISIONES.md`, `memoria/*.md`.
- **Escribe al terminar:** `LECCIONES.md`, `MAPA-AGENTES.md` (enrutado, tras aprobación), memorias, `REGISTRO.md`.
- **Modelo por defecto:** Haiku (Sonnet para síntesis amplia).

### Taller (`taller`)
- **Produce:** `TECNOLOGIA.md`, skills en `.claude/skills/`, `SKILLS.md`, artifacts y apps aprobados.
- **Necesita de otros:** briefing de la tarea (Conductor); necesidades de skills detectadas por otros agentes.
- **Suele pasar a:** Revisor, y a quien vaya a usar la skill.
- **Skills que usa:** las que cree y pruebe.
- **Lee al empezar:** `CLAUDE.md`, `LECCIONES.md`, `DECISIONES.md`, `TECNOLOGIA.md`, `SKILLS.md`, su memoria.
- **Escribe al terminar:** `TECNOLOGIA.md`, `SKILLS.md`, skills, su memoria, `REGISTRO.md`.
- **Modelo por defecto:** Sonnet (Haiku en búsquedas; Opus en arquitectura o bugs difíciles). Tiene web.

## Ramas del negocio

### Setter / Cierre (`setter-cierre`)
- **Produce:** perfiles de lead, lead scoring, seguimientos para llegar a la llamada, guiones de cierre, respuestas a objeciones.
- **Necesita de otros:** oferta definida (Educación/Producto), cómo se cuenta (Contenido); precio y estructura (Marketing).
- **Suele pasar a:** Contenido y Educación/Producto (objeciones reales); Blake (casos dudosos).
- **Skills que usa:** lead scoring (candidata, pendiente de recibir).
- **Lee al empezar:** lo común + `CONTEXTO/precios.md`, `CONTEXTO/negocio.md` (embudo).
- **Escribe al terminar:** su memoria, `REGISTRO.md`, traspasos.
- **Modelo por defecto:** Sonnet (Opus en cierres de alto valor o casos delicados).

### Marketing / Brand (`marketing-brand`)
- **Produce:** posicionamiento, media kit, estrategia de colaboraciones, plan SEO de blakebraider.com, decisiones de precio y estructura de producto.
- **Necesita de otros:** oferta (Educación/Producto), mensaje (Contenido), datos de audiencia (Blake).
- **Suele pasar a:** Contenido, Setter/Cierre, Educación/Producto.
- **Skills que usa:** ninguna aún.
- **Lee al empezar:** lo común + `CONTEXTO/marca.md`, `CONTEXTO/precios.md`.
- **Escribe al terminar:** su memoria, `REGISTRO.md`, traspasos, `DECISIONES.md` (si Blake decide).
- **Modelo por defecto:** Sonnet (Opus en precio y marca).

### Contenido (`contenido`)
- **Produce:** calendario de 8 pilares, guiones, carruseles, checklist de grabación.
- **Necesita de otros:** oferta (Educación/Producto), objeciones (Setter), coherencia (Marketing), detalles personales reales (Blake).
- **Suele pasar a:** Marketing, Setter/Cierre.
- **Skills que usa:** plan de 8 pilares, checklist de grabación, guion con 3 frameworks (candidatas).
- **Lee al empezar:** lo común + `CONTEXTO/marca.md`, `CONTEXTO/negocio.md` (contenido).
- **Escribe al terminar:** su memoria, `REGISTRO.md`, traspasos.
- **Modelo por defecto:** Sonnet (Haiku para formatear/calendarizar).

### Educación / Producto (`educacion-producto`, incluye Asesorías)
- **Produce:** diseño de formaciones, curso online, mini-curso, formación de formadores, diplomas, análisis de dudas recurrentes, asesorías (Digital Twin, auditoría de precios, entregables en dos documentos).
- **Necesita de otros:** objeciones (Setter), precios y estructura (Marketing), transcripciones (Blake).
- **Suele pasar a:** Contenido, Marketing, Setter/Cierre.
- **Skills que usa:** Digital Twin y auditoría de precios, entregables de asesoría, diplomas (candidatas).
- **Lee al empezar:** lo común + `CONTEXTO/negocio.md`, `CONTEXTO/precios.md`.
- **Escribe al terminar:** su memoria, `REGISTRO.md`, traspasos.
- **Modelo por defecto:** Sonnet (Opus en diseño de producto nuevo o fórmula de precios).

### Operaciones Salón (`operaciones-salon`)
- **Produce:** agenda y logística del salón y de la clientela de élite.
- **Necesita de otros:** políticas de Blake (aún vacías); precios de salón desde Legacy.
- **Suele pasar a:** Blake (toda confirmación).
- **Skills que usa:** ninguna.
- **Lee al empezar:** lo común + `CONTEXTO/clientes-vip.md`.
- **Escribe al terminar:** su memoria, `REGISTRO.md`.
- **Modelo por defecto:** Sonnet (Opus si afecta a VIP).

### Visión / Legado (opcional, más adelante)
Sin crear. Se activará cuando Blake lo pida.
