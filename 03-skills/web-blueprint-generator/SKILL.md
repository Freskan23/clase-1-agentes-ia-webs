---
name: web-blueprint-generator
description: Convierte las hipótesis del local-seo-pattern-aggregator en un blueprint de la web — arquitectura de URLs, schema JSON-LD por tipo de página, secciones recurrentes, headings y plan de internal linking. Es el plano antes de generar páginas. Úsala SIEMPRE que el usuario pida "diseña la arquitectura", "qué páginas debería tener", "cómo estructuro la web", "blueprint para [keyword]" o tras `local-seo-pattern-aggregator`. Output: archivos planos listos para que `landing-generator-servicio-barrio` los ejecute.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# Web Blueprint Generator

De **patrones detectados** a **plano de la web**. Antes de generar páginas, define qué páginas, con qué estructura, qué schema y qué internal linking. Sin esta capa, el agente improvisa cada landing y el resultado es inconsistente.

## Inputs

- `data/patterns/{kw}/{date}/hypotheses.md` ← de `local-seo-pattern-aggregator`.
- **Negocio target** · nombre, NAP, USP, lista de servicios reales, lista de zonas a cubrir.
- **Stack** · default **Astro** (también: Next.js, MDX puro).
- **Restricciones** · idioma, número máximo de páginas, presupuesto Lighthouse.

## Proceso

1. **Mapa de URLs** desde patrones + zonas:
   - Home (`/`)
   - Servicios pillar (`/servicios/{slug}/`)
   - Servicio × barrio (`/{servicio}/{barrio}/`) — el corazón del SEO local
   - Sobre nosotros, contacto, legales
   - Blog (opcional)
2. **Para cada tipo de página, definir:**
   - **Title pattern** y **meta description pattern** (con variables: `{servicio}`, `{barrio}`, `{ciudad}`, `{telefono}`).
   - **H1, H2, H3 pattern.**
   - **Secciones obligatorias** (extraídas de las hipótesis HIGH del aggregator).
   - **Schema JSON-LD** por tipo:
     - Home → `LocalBusiness` + `Organization`.
     - Servicio pillar → `Service` + `BreadcrumbList`.
     - Servicio × barrio → `Service` con `areaServed: PostalAddress` + `BreadcrumbList` + `FAQPage`.
   - **CTA** (telefónico siempre visible si los ganadores lo tienen).
3. **Plan de internal linking:**
   - Home → todos los servicios pillar.
   - Pillar → todos sus barrios.
   - Servicio × barrio → otros barrios del mismo servicio + servicio pillar + servicios relacionados.
   - Bloque `nearby areas` consistente.
4. **Plan de contenido mínimo** por página: longitud, FAQ obligatoria, prueba social, NAP.
5. **Lighthouse budget** (heredado de los patrones del top 3): LCP, CLS, TBT, JS bundle.

## Herramientas

- LLM para redactar patterns con variables.
- **schema-dts** para validar JSON-LD contra tipos oficiales.
- **astro-seo** o `next-sitemap` (referencia para generar sitemaps automáticos).

## Salida

```
blueprint/{negocio-slug}/
├── url-map.yaml                 ← lista completa de URLs a generar
├── page-templates/
│   ├── home.md                  ← plantilla con vars {{...}}
│   ├── service-pillar.md
│   └── service-area.md
├── schema-templates/
│   ├── home.jsonld
│   ├── service-pillar.jsonld
│   └── service-area.jsonld
├── internal-linking.yaml
├── lighthouse-budget.json
└── README.md                    ← cómo se usa este blueprint
```

**`url-map.yaml`** ejemplo:

```yaml
home: /
services:
  - slug: cerrajero-24h
    barrios: [centro, sant-oleguer, can-rull, gracia]
  - slug: aperturas-puertas
    barrios: [centro, sant-oleguer, can-rull]
legales:
  - aviso-legal
  - politica-privacidad
  - cookies
```

## Calidad / QA

- Verificar que cada `service-area` queda alcanzable en ≤ 3 clics desde la home.
- No generar combinaciones servicio × barrio que excedan el límite del usuario (avisar y pedir priorizar).
- Validar JSON-LD con schema-dts **antes** de pasar al generador.

## Para qué se usa después

→ Input directo de [`landing-generator-servicio-barrio`](../landing-generator-servicio-barrio/SKILL.md) (genera el código real) y [`landing-qa-runner`](../landing-qa-runner/SKILL.md) (que verifica el budget).
