---
name: landing-generator-servicio-barrio
description: Genera en lote las páginas servicio × barrio de la web a partir del blueprint, escribiendo archivos en el repo (Astro/MDX), añadiendo el schema JSON-LD, el internal linking y el sitemap. Úsala SIEMPRE que el usuario pida "genera las landings", "crea las páginas servicio × barrio", "monta las URLs del blueprint", "expande la web por zonas" o tras `web-blueprint-generator`. Es la skill que convierte el plano en código real, commiteable.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# Landing Generator · Servicio × Barrio

Toma el blueprint y produce **archivos físicos** en el repo de la web del cliente. **Astro** por defecto (rutas de archivo simples, SSG por defecto, ideal SEO), pero el output puede adaptarse a Next.js o MDX puro.

## Inputs

- `blueprint/{negocio-slug}/` ← de `web-blueprint-generator`.
- **Carpeta destino** · `src/pages/` (Astro) o `app/` (Next.js).
- **Locale** · default `es-ES`.
- **Modo** · `dry-run` (lista qué se generaría) o `apply` (escribe + commit).

## Proceso

1. **Cargar blueprint** y validar que existen `url-map.yaml`, page-templates y schema-templates.
2. **Por cada combinación servicio × barrio** del `url-map.yaml`:
   - Resolver variables (`{servicio}`, `{barrio}`, `{ciudad}`, etc.) con datos reales del negocio.
   - Inyectar **contenido único** mínimo por barrio (NO duplicar; ver QA).
   - Añadir **schema JSON-LD** correspondiente.
   - Calcular **internal links** según `internal-linking.yaml`.
   - Escribir archivo en la ruta correcta del repo.
3. **Generar páginas pillar** (`/servicios/{slug}/`) con listado de barrios cubiertos.
4. **Generar `sitemap.xml`** (o configurar `@astrojs/sitemap`) con prioridades.
5. **Generar `robots.txt`** consistente.
6. **Commitear cambios** en una rama nueva: `feat/landings-{servicio}-{N}-barrios`.
7. **Mostrar resumen:** N páginas creadas, peso total HTML, schema validado, dry-run o aplicado.

## Herramientas

- File system (Read/Write/Edit) sobre el repo del cliente.
- Git para commits.
- **Astro** + `@astrojs/sitemap` + `astro-seo`.
- LLM para generar el bloque de contenido único por barrio (con guardrails de longitud y unicidad).
- **schema-dts** para validar JSON-LD antes de escribir.

## Salida

```
src/pages/{servicio}/{barrio}.astro      ← una por combinación
src/pages/servicios/{servicio}.astro     ← pillar
src/data/areas-served.json               ← fuente de verdad de zonas
public/sitemap.xml                       ← regenerado
public/robots.txt
```

Y un commit limpio con el mensaje:

```
feat(landings): generar N landings servicio × barrio

- Servicio: cerrajero-24h
- Barrios: 12
- Pillar actualizada
- Sitemap regenerado (entradas: 13)
- Schema JSON-LD validado con schema-dts
```

## Calidad / QA

- **Unicidad de contenido:** cada landing debe tener ≥ 30 % de tokens distintos a sus hermanas (similitud Jaccard < 0.7). Si no, regenerar el bloque variable.
- **Validación schema:** ningún archivo se escribe si el JSON-LD no valida.
- **Internal linking obligatorio:** cada landing tiene mínimo 3 enlaces internos a otros barrios del mismo servicio + 1 al pillar.
- **Lighthouse budget:** se delega a `landing-qa-runner` post-generación.
- **Coste/tiempo:** avisar si > 50 combinaciones en una sola ejecución.

## Para qué se usa después

→ Input de [`landing-qa-runner`](../landing-qa-runner/SKILL.md) que pasa Playwright + Lighthouse-CI sobre todas las URLs generadas y bloquea el merge si no cumplen el budget heredado del top 3.
