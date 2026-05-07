---
name: web-pattern-extractor
description: Escanea en lote N webs de competidores y devuelve una matriz comparativa de patrones — schema usado, headings (H1-H3), FAQ, secciones recurrentes (hero, services, reviews, CTA), internal linking, longitud, lighthouse y entidades léxicas. Úsala SIEMPRE que el usuario pida "analiza estas webs y dime qué tienen en común", "extrae patrones de las webs del top 10", "qué estructura usan los competidores" o tras `local-pack-multi-city`/`gbp-deep-profile` para enriquecer dominios detectados. Es la skill que convierte N webs en datos comparables.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# Web · Pattern Extractor

Si `competitor-local-seo-audit` produce un informe **profundo** de UNA web (formato cliente), esta skill produce una **matriz comparativa** de **N webs** lista para detectar patrones repetibles.

## Inputs

- **Lista de URLs** o dataset `consolidated.json` de `local-pack-multi-city`.
- **Profundidad** · `1` (solo home), `2` (home + servicios), `3` (home + servicios + 1 servicio individual).
- **User-Agent** · `mobile` por defecto (Google indexa mobile-first).
- **Schema fields a verificar** · default: `LocalBusiness`, `Service`, `FAQPage`, `BreadcrumbList`, `Review`, `AggregateRating`, `Organization`, `OpeningHoursSpecification`.

## Proceso

Para **cada URL** (paralelizable):

1. **Render real** con Playwright MCP (mobile, JS habilitado).
2. **Extraer DOM:**
   - `<title>`, `<meta name="description">`, `<link rel="canonical">`.
   - **Headings** completos (H1, H2, H3) con su texto.
   - **JSON-LD** detectado: tipos, propiedades clave, validez.
   - **Microdata / RDFa** si existen.
3. **Detectar bloques recurrentes** (heurística + clasificación con LLM):
   - Hero (presencia + estructura: tagline, CTA, imagen).
   - Services list / grid.
   - Reviews block (testimonios on-page).
   - FAQ (con `<details>` o acordeón).
   - Trust signals (años, certificados, logos clientes).
   - CTA position (top, mid, bottom, sticky).
   - Footer NAP (Name + Address + Phone).
4. **Internal linking:** anchors → URL → categoría (servicio, blog, legal). Ratio internal vs external.
5. **Performance:** Lighthouse mobile (Performance, Accessibility, Best Practices, SEO + LCP, CLS, TBT, FCP).
6. **NLP entidades:** términos repetidos en H1/H2 (sin stop-words). Top 50 n-gramas (1-3).
7. **Pillar map:** árbol de URLs descubiertas a profundidad N.

## Herramientas

- **Playwright MCP** o **Chrome DevTools MCP** (render real).
- **Browserbase / Steel.dev** si se quiere paralelizar en cloud.
- **Firecrawl** (URL → markdown limpio) para alimentar la parte LLM más rápido.
- **PageSpeed Insights MCP** o **Lighthouse MCP**.
- **schema-dts** (TypeScript) si se quiere validar JSON-LD contra tipos oficiales.

## Salida

```
data/web-patterns/{keyword-slug}/{YYYY-MM-DD}/
├── per-domain/
│   ├── example1.com.json   ← extracción completa de ese dominio
│   └── example2.com.json
├── matrix.csv              ← matriz N × M de features
└── ngrams.csv              ← top n-gramas globales
```

**Matriz comparativa (`matrix.csv`)** — columnas mínimas:
`domain, has_localbusiness_schema, has_faq_schema, has_service_schema, schema_completeness_pct, h1_text, h1_keyword_match, h2_count, n_services_listed, has_hero, has_reviews_block, has_faq_block, faq_count, internal_links_count, mobile_lcp_ms, mobile_cls, lighthouse_seo, content_words_count`.

## Calidad / QA

- Saltar URLs que devuelvan 4xx/5xx (anotar en `errors.json`, no parar el batch).
- Si la página requiere JS y no renderiza → reintentar con timeout × 2 antes de marcar como muerta.
- Avisar si > 30 % de los dominios fallan → revisar User-Agent o IP.

## Para qué se usa después

→ Input directo de [`local-seo-pattern-aggregator`](../local-seo-pattern-aggregator/SKILL.md): detecta qué features están **sobre-representadas** en el top 3 vs el resto.
