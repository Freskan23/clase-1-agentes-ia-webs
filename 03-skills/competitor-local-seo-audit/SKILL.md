---
name: competitor-local-seo-audit
description: Análisis competitivo SEO local exhaustivo. Úsala SIEMPRE que el usuario pida investigar competencia, hacer auditoría comparativa, sacar informe de competidores, analizar competidores en Google Maps o GBP, hacer análisis de mercado local SEO, o frases como "investiga la competencia de X en Y", "auditame los competidores", "informe de competencia para [cliente]", "compara estos negocios con la competencia", "qué hacen mejor los que rankean por encima". También dispara cuando se mencionen ciudades concretas con un sector (ej. "cerrajeros Sabadell", "fisios Hortaleza", "abogados Bilbao"). Genera entregable docx listo para cliente.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# Competitor Local SEO Audit

Workflow completo para análisis competitivo SEO local. Output final: informe docx profesional listo para cliente.

## Inputs esperados

El usuario te dará alguna combinación de:
- **Negocio target**: nombre + URL + ubicación (ej. "SuperTOP Cerrajeros, Sabadell, supertopcerrajeros.com")
- **Keyword principal**: la consulta por la que quieren rankear (ej. "cerrajero 24h Sabadell")
- **Número de competidores a analizar**: si no lo dice, usa **top 10** por defecto

Si falta algo crítico (negocio o keyword), **pregunta antes de empezar**. No inventes.

## Paso 1 — Identificar competidores

Prioriza la fuente más fiable disponible:

**Opción A (preferida): Google Places API**
- Si el usuario tiene `GOOGLE_PLACES_API_KEY` configurada, úsala vía MCP o llamada directa
- Endpoint: `places.googleapis.com/v1/places:searchText`
- Ventaja: estable, no se banea, devuelve `user_ratings_total` y rating

**Opción B: Scraper Maps con Playwright/Patchright**
- Solo si no hay API key disponible
- Usa el código en `~/Documents/Clientes/` como base si existe
- Recuerda: desde febrero 2026 Google muestra "limited view" sin sesión iniciada → navega vía búsqueda en Maps, NO con URL directa de ficha
- Si el scraper devuelve 0 reviews o datos vacíos, es el limited view → cambiar de estrategia, no insistir

**Opción C: SERP scraping**
- Para extraer top 10 orgánico (no GBP), usa SerpAPI o el MCP que tenga el usuario configurado

Para cada competidor recopila como mínimo: nombre, URL, dirección, teléfono, total de reviews, rating medio, categoría GBP principal.

## Paso 2 — Auditoría técnica de cada competidor

Para cada URL competidora, dispara estas comprobaciones en este orden (parar si la URL devuelve 4xx/5xx, anotar y seguir con el siguiente):

**Performance & Core Web Vitals**
- MCP recomendado: `mcp-seo-audit` (GiorgiKemo) o `pagespeed-insights-mcp` (ruslanlap)
- Tool: `lighthouse_audit` con `device=mobile`
- Captura: scores de Performance, Accessibility, Best Practices, SEO; LCP, CLS, TBT, FCP

**On-page SEO**
- Tool: `analyze_on_page_seo` o equivalente
- Captura: title tag, meta description, longitud de contenido (palabras), estructura H1-H6 (anota si hay múltiples H1), imágenes sin alt, ratio internal/external links

**Open Graph y Twitter Cards**
- Comprobar presencia y validez de: `og:title`, `og:description`, `og:image`, `twitter:card`
- Marcar como "fail" cualquier negocio sin OG (suele indicar web sin mantener)

**Schema / Structured Data**
- Detectar tipos JSON-LD presentes: `LocalBusiness`, `Organization`, `Review`, `BreadcrumbList`
- Para SEO local, la ausencia de `LocalBusiness` schema es señal roja

**Sitemap & robots.txt**
- Tool: `check_robots_txt` o `analyze_sitemap`
- Captura: existe sitemap.xml sí/no, número de URLs en sitemap, sitemap referenciado en robots.txt sí/no, hay reglas Disallow problemáticas

**Security headers (opcional pero suma)**
- HTTPS sí/no, HSTS, CSP

## Paso 3 — Cruzar con datos GBP

Para cada competidor, además de la web, audita su ficha de Google Business:
- Nº de fotos
- Nº de posts en últimos 30 días
- Tiene "Productos" / "Servicios" rellenos
- Atributos diferenciadores (ej. "Identifies as women-owned", "Wheelchair accessible")
- Última review hace cuántos días (proxy de actividad)

Esto requiere Places API (Place Details) o scraping autenticado. Si no es viable, **dilo claramente en el informe** y sigue con la auditoría web.

## Paso 4 — Detectar patrones

Una vez recogidos los datos de los 10, busca patrones de comportamiento de Google. Genera estas observaciones:

1. **Reviews threshold**: cuántas reviews medias tienen los top 3 vs top 10. Si hay un escalón claro (ej. top 3 todos >100, top 10 medio 30), es un patrón.
2. **Performance threshold**: score Lighthouse mobile medio del top 3 vs resto.
3. **Contenido**: longitud media de texto en homepage del top 3 vs resto.
4. **Schema**: % de los top 3 con `LocalBusiness` schema bien implementado.
5. **Coincidencias en H1**: qué keywords usan el 70%+ de los top 5 en H1.
6. **Antigüedad de dominio** si está disponible (whois lookup vía MCP).

## Paso 5 — Generar el informe

Usa la skill **`docx`** para crear el documento final. Estructura obligatoria:

1. **Portada**: nombre del negocio target, fecha, keyword analizada, ubicación
2. **Resumen ejecutivo** (máximo 5 bullets): el "qué hacer" para el cliente, escrito en lenguaje de no-técnico
3. **Tabla comparativa principal**: una fila por competidor, columnas con todas las métricas clave (puntúa con 🟢🟡🔴 los scores Lighthouse para que el cliente lo lea de un vistazo)
4. **Patrones de Google detectados**: los 6 puntos del Paso 4 explicados
5. **Top 5 oportunidades concretas** para el target, priorizadas por impacto/esfuerzo
6. **Anexo técnico**: datos crudos de cada competidor para quien quiera profundizar

El informe debe ser legible por un cliente no técnico. **Nada de jerga sin explicar.** Si mencionas "schema LocalBusiness", añade entre paréntesis qué es en una línea.

## Reglas de calidad

- **Nunca inventes datos.** Si una métrica no se pudo extraer, escribe "no disponible" y explica por qué.
- **Cita siempre la fuente** de cada dato (Places API, Lighthouse local, scraper Maps, etc.) en el anexo técnico.
- **Tono profesional pero directo.** El cliente paga por accionables, no por adjetivos.
- **No copies textos** de las webs auditadas. Solo métricas y observaciones.
- Si detectas algo manifiestamente raro en un competidor (ej. sin HTTPS en 2026, o sin sitemap), **destácalo** en oportunidades — es una victoria fácil para el target.

## Workflow resumido

```
1. Confirmar inputs (negocio, keyword, ubicación)
2. Identificar 10 competidores (Places API > scraper > SERP)
3. Auditar cada uno: Lighthouse + On-page + OG + Schema + Sitemap
4. Cruzar con datos GBP
5. Detectar patrones de ranking
6. Generar docx con skill `docx`
7. Presentar al usuario con `present_files`
```

## Avisos

- Si vas a auditar más de 10 competidores, **avisa primero del coste estimado** (cada Lighthouse local tarda ~30s; 10 competidores × 5 checks ≈ 5 min mínimo).
- Si el cliente está en sector regulado (legal, sanitario, financiero), añade una columna "claims arriesgados detectados" en la tabla — útil para asesorar sobre qué NO copiar.
- Si Google bloquea el scraper a mitad de ejecución, **para, guarda lo que tengas y avisa** al usuario antes de seguir intentando con stealth.
