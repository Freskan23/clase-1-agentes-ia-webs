# Clase 1 · Agentes IA para SEO y webs hiperoptimizadas

Material maestro de la primera clase del **itinerario de Agentes IA de YinyangSEO**.
Audiencia: SEOs y marketers que tocan código a ratos.

> No vamos a aprender nombres de IAs.
> Vamos a aprender a montar un **sistema** para investigar, crear, probar y optimizar webs con agentes.

---

## Índice rápido

| Sección | Contenido |
|---------|-----------|
| [00 · Comparativa de agentes](00-comparativa-agentes/) | Trae SOLO, Windsurf, Cursor, Claude Code, Codex, OpenCode. Tabla y criterio de elección. |
| [01 · Diccionario técnico](01-diccionario/) | Repo, branch, MCP, tokens, skill, dev server, deploy, BYOK, sandbox… |
| [02 · Investigación de competidores](02-investigacion-competidores/) | Stack en 5 niveles + repos stealth + advertencia ética. |
| [03 · Skills custom](03-skills/) | `competitor-local-seo-audit`, `gbp-grid-extractor`, `serp-pattern-detector`. |
| [Apuntes de la clase](apuntes/apuntes-clase.md) | Recorrido en prosa por las 25 diapositivas. |
| [Glosario](apuntes/glosario.md) | Definiciones rápidas. |
| [Ejercicio del grupo (10 min)](apuntes/ejercicio.md) | Caso “web local por servicio + barrio”. |
| [Checklist pre-construcción](apuntes/checklist.md) | Lo mínimo claro antes de la práctica. |
| [Notas del instructor](apuntes/notas-instructor.md) | Speaker notes y timings. |
| [Recursos y enlaces](recursos/enlaces.md) | Herramientas, repos, APIs y lecturas. |
| [Presentación (.pptx)](presentacion/clase_1_agentes_ia_webs_hiperoptimizadas_v2_con_notas.pptx) | El deck con notas. |

---

## Idea central

La clase no va solo de “qué agente usar”. La idea es que el alumno entienda **cómo se monta un sistema de trabajo con agentes**:

1. **Elegir la superficie** adecuada: chat, CLI, IDE o builder visual.
2. **Entender el vocabulario** técnico mínimo.
3. **Usar repositorios** de GitHub como contexto, plantilla y código reutilizable.
4. **Conectar herramientas** mediante MCPs, APIs y navegador.
5. **Convertir procesos repetibles** en *skills*.
6. **Aplicarlo a un caso real**: investigación de competidores locales.

Narrativa: de **menor a mayor complejidad** — primero seguridad y claridad, después herramientas, después automatización, y al final el “wow factor” de una skill custom.

---

## Mapa visual

| | |
|--|--|
| ![Comparativa](00-comparativa-agentes/comparativa.png) | ![Stack 5 niveles](02-investigacion-competidores/stack-clase-5-niveles.png) |
| Comparativa de agentes | Stack de investigación · 5 niveles |

---

## Recorrido recomendado

### 0 · Apertura (5 min)
Presentar el objetivo. Bajar ansiedad: hoy no se construye, hoy se entiende. Material: el deck + `00-comparativa-agentes/comparativa.png`.

### 1 · Comparativa de agentes (15 min)
Elegir agente **según perfil y fricción**, no según moda.
→ [`00-comparativa-agentes/comparativa-agentes-ia.md`](00-comparativa-agentes/comparativa-agentes-ia.md)
> *La barrera principal no es el modelo. Es la superficie: CLI, IDE, navegador, preview y facilidad de prueba.*

### 2 · Diccionario técnico mínimo (15 min)
Para que nadie se pierda con repo, branch, MCP, tool call, dev server o deploy.
→ [`01-diccionario/diccionario-conceptos.md`](01-diccionario/diccionario-conceptos.md)

Bloques:

- Caja de herramientas (CLI, IDE, fork, repo, GitHub, branch, commit, push/pull).
- Vocabulario del agente (LLM, agente vs chat, token, contexto, prompt, MCP, tool call, skill, subagent).
- Desarrollo web (frontend, backend, framework, dev server, preview, deploy, DOM, DevTools, Playwright).
- Costes (API, API key, BYOK, pay-as-you-go, suscripción, prompt caching, batch API, crédito).
- Conceptos extra (open source, vendor lock-in, SDK, sandbox, worktree, npm/npx, modelo local).

### 3 · GitHub y repositorios (10 min)
Un repo no es solo código: es **memoria técnica del proyecto**.

Ideas clave:

- Guarda código, historial, instrucciones, decisiones y scripts.
- Permite **plantillas, aprendizaje y punto de partida**.
- Un agente puede leer un repo para entender el proyecto antes de tocarlo.
- Commits → vuelves atrás. Ramas → experimentas sin romper.

> Para un agente, GitHub es una **biblioteca de patrones** y una **memoria de proyecto**.

### 4 · Repos, MCPs y APIs para investigación SEO (15 min)
→ [`02-investigacion-competidores/investigacion-skills-repos-mcps.md`](02-investigacion-competidores/investigacion-skills-repos-mcps.md)

Capas del stack (de suave a pro):

1. **SiteAudit MCP hospedado** — apertura suave, cero instalación. Lighthouse + robots + links.
2. **`mcp-seo-audit` self-hosted** — profundidad técnica con GSC, CrUX, PageSpeed, sitemap, on-page.
3. **Playwright MCP + Chrome DevTools MCP** — navegación agéntica, clicks, capturas, consola.
4. **Nodriver / Patchright / Camoufox** — cuando Google bloquea. Con explicación ética.
5. **Skill custom** — cierre demostrativo con proceso empaquetado.

### 5 · Qué es una skill (10 min)
Una skill no es un prompt largo. Es **una forma de trabajar empaquetada**.

Una skill define:

- **Objetivo** · qué tarea resuelve.
- **Inputs** · qué datos necesita.
- **Proceso** · pasos ordenados + decisiones.
- **Herramientas** · APIs, navegador, terminal, MCPs.
- **Restricciones** · qué no debe hacer.
- **Salida** · entregable y formato.
- **Calidad** · cuándo se considera terminado.

> *Un prompt pide una respuesta. Una skill define un procedimiento.*

### 6 · Skills custom de la clase (15 min)
→ [`03-skills/`](03-skills/)

| Skill | Qué hace | Salida |
|-------|----------|--------|
| [`competitor-local-seo-audit`](03-skills/competitor-local-seo-audit/SKILL.md) | GBP + auditoría web + PageSpeed + schema + sitemap. | Informe DOCX. |
| [`gbp-grid-extractor`](03-skills/gbp-grid-extractor/SKILL.md) | Grid geográfico de rankings GBP (estilo Local Falcon / GEOGRIDS). | Mapa + JSON. |
| [`serp-pattern-detector`](03-skills/serp-pattern-detector/SKILL.md) | Patrones de SERP: Map Pack, PAA, AI Overview, schema, freshness. | Hipótesis accionables. |

> *Las skills convierten conocimiento interno en capacidad repetible. Eso es lo que hace que el sistema escale.*

### 7 · Cierre (5 min)
Ejercicio en grupo + checklist + dudas.
→ [`apuntes/ejercicio.md`](apuntes/ejercicio.md) · [`apuntes/checklist.md`](apuntes/checklist.md)

---

## Demo recomendada (orden sugerido)

1. Comparativa de agentes.
2. Abrir el diccionario, explicar repo / GitHub / MCP / skill.
3. Stack de 5 niveles.
4. Ejecutar (o simular) **SiteAudit MCP** con un competidor.
5. Si necesitamos más profundidad → **mcp-seo-audit**.
6. Navegación agéntica con **Playwright / Chrome DevTools**.
7. Cierre con una skill custom: `serp-pattern-detector` o `competitor-local-seo-audit`.

> La demo no debe prometer magia. Debe transmitir **criterio**: cuándo usar API oficial, cuándo MCP, cuándo navegador, cuándo no merece la pena hacer scraping y cuándo conviene empaquetar el proceso como skill.

---

## Filosofía

> *El stack se vuelve obsoleto cada 3 meses. Por eso el valor no es “este script”. El valor es tener **criterio + sistema** para adaptar herramientas sin perderte.*
>
> *El agente acelera; el criterio lo pones tú.*

---

## Material para entregar a los asistentes

- PDF del diccionario.
- Imagen del stack de 5 niveles.
- Tabla comparativa de agentes.
- ZIP con las tres skills custom.
- Mini-guía: *prompt vs skill vs MCP vs API*.

---

## Pendientes de mejora (TODO interno)

- Convertir el diccionario en PDF limpio.
- Slide específica para “MCP = USB-C de los agentes”.
- Slide específica para “API oficial vs scraping”.
- Añadir ejemplo real de output de cada skill.
- Probar las tres skills con un cliente real antes de usarlas como demo.

---

## Licencia

Material formativo del itinerario **YinyangSEO**. Consulta [`LICENSE`](LICENSE).

🤖 ¿Erratas o propuestas? Abre un *issue* o un *pull request*.
