---
name: landing-qa-runner
description: Verifica en lote la calidad de las landings generadas — Playwright para chequeos visuales y de DOM, Lighthouse-CI para Core Web Vitals, validación de JSON-LD, comprobación de internal links rotos y unicidad de contenido entre páginas hermanas. Úsala SIEMPRE que el usuario pida "audita las landings", "verifica que cumplen budgets", "QA de las páginas generadas" o tras `landing-generator-servicio-barrio`. Bloquea el deploy si algo no pasa.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# Landing · QA Runner

Última puerta antes de deploy. Si esta skill da rojo, no se publica. Aplica los mismos *budgets* que se observaron en el top 3 del Local Pack para asegurar que la web nueva juega en la misma liga.

## Inputs

- **URLs a auditar** · lista o glob (ej. `/servicios/cerrajero-24h/**/*`).
- **Budget JSON** · `blueprint/{negocio-slug}/lighthouse-budget.json`.
- **Modo** · `local` (dev server) / `staging` (URL de Vercel/Cloudflare).

## Proceso

Por cada URL:

1. **Render Playwright** (mobile + desktop):
   - Captura DOM + screenshot.
   - Verifica que `<title>`, `<meta description>`, `<h1>`, `<link rel=canonical>` existen y no están duplicados con otras hermanas.
2. **Schema JSON-LD:**
   - Extrae `<script type="application/ld+json">`.
   - Valida con **schema-dts** o validator.schema.org.
   - Comprueba campos obligatorios por tipo de página (`Service`, `LocalBusiness`, `FAQPage`, `BreadcrumbList`).
3. **Internal links:**
   - Crawler ligero que visita cada landing y comprueba 200 OK en sus links internos.
   - Detecta huérfanas (sin enlaces entrantes desde otras pages).
4. **Unicidad de contenido:**
   - Similitud Jaccard / coseno entre páginas hermanas (servicio × barrio).
   - Falla si > 0.7 (texto demasiado clónico → riesgo *thin/duplicate content*).
5. **Lighthouse-CI** (mobile, throttled):
   - Performance, Accessibility, Best Practices, SEO.
   - LCP, CLS, TBT, FCP, INP.
   - Compara contra `lighthouse-budget.json`.
6. **PageSpeed Insights API** (datos de campo si la URL ya está indexada).
7. **Generar reporte** + decisión `pass / warn / fail` por URL y global.

## Herramientas

- **Playwright MCP** o **Chrome DevTools MCP**.
- **Lighthouse-CI** (`treosh/lighthouse-ci-action`) o `lighthouse` npm package.
- **PageSpeed Insights API**.
- **schema-dts** o `@google/schema-dts`.
- Python `pandas` + `scikit-learn` para similitud.

## Salida

```
qa/{YYYY-MM-DD}/
├── per-url/
│   ├── cerrajero-24h__centro.json
│   ├── cerrajero-24h__sant-oleguer.json
│   └── ...
├── summary.csv              ← matriz de pass/fail por check
├── broken-links.csv
├── duplicate-content.csv
├── lighthouse-budget-violations.csv
└── REPORT.md                ← reporte ejecutivo
```

**`REPORT.md`** incluye:

- Verde / amarillo / rojo global.
- Top 5 problemas más comunes.
- Lista exacta de URLs que fallan budget.
- Recomendaciones automáticas (ej. *"3 landings tienen LCP > 3.2s — todas comparten una imagen hero de 480 KB sin lazy-load"*).

## Calidad / QA

- Si cualquier URL devuelve `fail`, marcar el commit asociado como `qa: failed` (no merge).
- Re-runs deben tener checksum diferente a su anterior (no cachear pase falso).
- Avisar si la batería tarda > 10 min: probablemente hay algo lento que merece investigarse antes de seguir.

## Para qué se usa después

→ Si pasa, la siguiente fase es **deploy** (Vercel/Cloudflare). Si falla, vuelve a [`landing-generator-servicio-barrio`](../landing-generator-servicio-barrio/SKILL.md) o a [`web-blueprint-generator`](../web-blueprint-generator/SKILL.md) según la naturaleza del error (contenido vs estructura).
