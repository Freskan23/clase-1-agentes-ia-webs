# Ejercicio · Traduce un caso a “piezas” (10 min)

> Objetivo: que el grupo practique el vocabulario sin escribir código.

---

## El caso

> *“Quiero una web para un negocio local que **genere páginas por servicio + barrio**, se **edite fácil** y **cargue rápido**.”*

---

## En grupos, responded:

1. **¿Qué parte es repo / template?**
   ¿De dónde sale la base? ¿Hay alguna plantilla en GitHub o en TickHat que sirva de punto de partida?

2. **¿Qué parte es API (datos oficiales)?**
   ¿Qué datos podemos pedir a APIs oficiales en lugar de scrapear? Pista: PageSpeed, Search Console, Google Places…

3. **¿Qué parte es MCP / navegador (verificación)?**
   ¿Qué tendríamos que **mirar con ojos humanos / agente** para validar el resultado? PageSpeed, Playwright, Chrome DevTools…

4. **¿Qué convertirías en skill?**
   Lo que se repite cada vez que lanzas una nueva combinación servicio × barrio. Pista: generar páginas y QA.

---

## Pistas (no leer hasta haberlo intentado)

<details>
<summary>Posibles respuestas</summary>

- **Repo / template:** plantilla en Astro o Next con generación estática + esquema FAQ + `landingPages` data-driven (Markdown / Sheets / Airtable).
- **API:** Google Places (datos del negocio), PageSpeed Insights (rendimiento por URL), Search Console (cobertura e impresiones).
- **MCP / navegador:** Playwright MCP para verificar render, capturar screenshots y revisar Lighthouse en mobile.
- **Skill:** `landing-generator-servicio-barrio` (input: servicio + lista de barrios → output: páginas + sitemap + QA + commit).

</details>

---

## Dinámica recomendada

- **6–7 min** de discusión en grupos.
- **3 min** de puesta en común guiada.

> Busca respuestas tipo: CMS / Sheets, PageSpeed, Playwright QA, skill de generación de páginas + QA.
