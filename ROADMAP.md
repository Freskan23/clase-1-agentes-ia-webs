# Roadmap del itinerario · Webs agénticas y SEO eficiente

> 📚 **YinyangSEO Academy · Itinerario completo**
> Este documento dibuja el flujo end-to-end desde *"investigar el Local Pack en N ciudades"* hasta *"web hiperoptimizada en producción"*.
> Las skills marcadas como **STUB** son placeholders que se irán desarrollando en clases siguientes.

---

## El flujo en una imagen mental

```
┌─────────────────────────────────────────────────────────────────────┐
│ 1) INVESTIGACIÓN          2) ANÁLISIS           3) AGREGACIÓN       │
│                                                                     │
│   local-pack-multi-city → gbp-deep-profile  →   local-seo-          │
│   serp-pattern-detector   web-pattern-          pattern-aggregator  │
│                           extractor             (PATRONES)          │
│                           competitor-local-                         │
│                           seo-audit                                 │
└──────────────────────────────┬──────────────────────────────────────┘
                               ▼
┌─────────────────────────────────────────────────────────────────────┐
│ 4) BLUEPRINT              5) GENERACIÓN         6) QA + DEPLOY      │
│                                                                     │
│   web-blueprint-       →  landing-generator- →  landing-qa-runner → │
│   generator               servicio-barrio       (Playwright +       │
│                                                  Lighthouse-CI)     │
│                                                                     │
│                                                  ↓                  │
│                                                Vercel /             │
│                                                Cloudflare           │
└─────────────────────────────────────────────────────────────────────┘
```

---

## Fases y skills

### Fase 1 · Investigación

| Skill | Estado | Descripción |
|-------|:-:|-------|
| [`local-pack-multi-city`](03-skills/local-pack-multi-city/SKILL.md) | 🟡 STUB | Captura SERP + Local Pack para keyword × N ciudades. |
| [`serp-pattern-detector`](03-skills/serp-pattern-detector/SKILL.md) | ✅ MADURA | Patrones de UNA SERP. |
| [`gbp-grid-extractor`](03-skills/gbp-grid-extractor/SKILL.md) | ✅ MADURA | Grid geográfico de rankings. |

### Fase 2 · Análisis profundo

| Skill | Estado | Descripción |
|-------|:-:|-------|
| [`gbp-deep-profile`](03-skills/gbp-deep-profile/SKILL.md) | 🟡 STUB | Ficha GBP completa por negocio. |
| [`web-pattern-extractor`](03-skills/web-pattern-extractor/SKILL.md) | 🟡 STUB | Matriz comparativa de N webs. |
| [`competitor-local-seo-audit`](03-skills/competitor-local-seo-audit/SKILL.md) | ✅ MADURA | Auditoría profunda 1 a 1, formato cliente. |

### Fase 3 · Agregación de patrones

| Skill | Estado | Descripción |
|-------|:-:|-------|
| [`local-seo-pattern-aggregator`](03-skills/local-seo-pattern-aggregator/SKILL.md) | 🟡 STUB | **Pieza clave.** Detecta qué hacen distinto los ganadores del Local Pack. |

### Fase 4 · Blueprint

| Skill | Estado | Descripción |
|-------|:-:|-------|
| [`web-blueprint-generator`](03-skills/web-blueprint-generator/SKILL.md) | 🟡 STUB | De patrones a arquitectura de URLs + schema + secciones. |

### Fase 5 · Generación

| Skill | Estado | Descripción |
|-------|:-:|-------|
| [`landing-generator-servicio-barrio`](03-skills/landing-generator-servicio-barrio/SKILL.md) | 🟡 STUB | Genera N páginas servicio × barrio en Astro. |

### Fase 6 · QA + Deploy

| Skill | Estado | Descripción |
|-------|:-:|-------|
| [`landing-qa-runner`](03-skills/landing-qa-runner/SKILL.md) | 🟡 STUB | Playwright + Lighthouse-CI batch. Bloquea deploy si no pasa. |
| `deploy-vercel-cloudflare` | ⏳ pendiente | Doc/skill para deploy con previews. Llegará en clase posterior. |

---

## Estado de las skills

| Símbolo | Significado |
|:-:|---|
| ✅ MADURA | Lista para usar con un caso real. Entregable definido. |
| 🟡 STUB | Estructura completa (objetivo, inputs, proceso, outputs) lista para que tu agente la implemente. Iremos puliéndolas en clase. |
| ⏳ pendiente | Aún sin SKILL.md. Llegará en clase posterior. |

---

## Calendario (tentativo)

| Clase | Foco | Skills tocadas |
|-------|------|----------------|
| **1 · Setup** *(esta clase)* | Vocabulario, agentes, skills, MCPs, repos. Repo descargable como contexto. | (todas como referencia) |
| 2 · Investigación | Lanzar `local-pack-multi-city` y `serp-pattern-detector` reales. | Fase 1 |
| 3 · Análisis profundo | Ejecutar `gbp-deep-profile` + `web-pattern-extractor`. | Fase 2 |
| 4 · Patrones | El "wow factor": `local-seo-pattern-aggregator`. Lectura de hipótesis. | Fase 3 |
| 5 · Blueprint | Diseñar la arquitectura de la web con `web-blueprint-generator`. UX y components. | Fase 4 |
| 6 · Generación | Crear las landings reales con `landing-generator-servicio-barrio`. | Fase 5 |
| 7 · QA + deploy | `landing-qa-runner` + Vercel/Cloudflare. Cierre del ciclo. | Fase 6 |
| 8 · Mantenimiento | Skills de monitoreo continuo, refresco de patrones, A/B. | Por definir |

---

## Cómo evoluciona este repo

Cada clase actualiza este repo con:

- Skills nuevas que aparezcan en el itinerario.
- Versiones más maduras de las STUB.
- Outputs reales de ejemplo en `data/` (cuando ejecutemos casos).
- Templates de starter Astro en `starters/` (cuando lleguemos a Fase 4-5).

> 🔄 Para tener siempre la última versión: `git pull` (si lo clonaste) o vuelve a descargar el ZIP desde GitHub.

---

## Para contribuir o reportar erratas

- Issue en GitHub describiendo el caso.
- Pull request si quieres proponer un cambio concreto.
- O directamente abrir tema en clase.

---

## Stack recomendado por defecto

**Web:** Astro + `@astrojs/sitemap` + `astro-seo` + Tailwind + schema-dts.
**Agentes:** Trae SOLO o Cursor con MCP.
**Investigación:** Browserbase + Firecrawl + SerpAPI/DataForSEO + Google Places API.
**QA:** Playwright MCP + Lighthouse-CI (GitHub Action).
**Deploy:** Vercel (previews) o Cloudflare Pages.
**Analytics:** Plausible o Umami.

> Todos los enlaces oficiales en [`recursos/enlaces.md`](recursos/enlaces.md).
