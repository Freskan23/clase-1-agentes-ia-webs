# Investigación de Competidores SEO Local con Agentes IA

**Para clase 1 del itinerario YinyangSEO** · Bloque 3: investigación de competidores
**Datos verificados a:** mayo 2026

Stack completo para que un SEO/marketer pueda usar agentes IA para hacer análisis competitivo local con profundidad. Desde la apertura suave hasta el caso "Google nos bloquea, ¿qué hacemos?".

---

## 1. Repositorios de GitHub para scraping con baja detección

Lo que necesitas para que Google no te bloquee al sacar profundidad de SERPs y fichas. Ordenado de mayor a menor relevancia para perfil de SEO local.

### Nodriver
**Repo:** `https://github.com/ultrafunkamsterdam/nodriver`

Sucesor de undetected-chromedriver, escrito por el mismo autor. Lo más potente que hay ahora mismo porque no usa WebDriver: habla directamente con Chrome por DevTools Protocol, así que no deja las huellas que los anti-bot detectan. Pasa Cloudflare donde Patchright falla. Async-only (Python).

**Para clase:** este es el que enseñas como "estado del arte 2026".

### Camoufox
**Repo:** `https://github.com/daijro/camoufox`

Firefox modificado a nivel C++ con el fingerprint "real" de un Firefox legítimo. Pasa CreepJS al 0% en headless y con virtual display.

Si necesitas máxima invisibilidad y no te importa usar Firefox, este es el rey. Lockeado a Firefox, no Chrome.

### Patchright
**Repo:** `https://github.com/Kaliiiiiiiiii-Vinyzu/patchright`

Drop-in replacement de Playwright que aplica parches stealth automáticamente. **Ventaja para Edu:** si ya tienes código Playwright (y lo tienes en `~/Documents/Clientes/`), cambias el import y listo. Es el upgrade inmediato y de mínima fricción al scraper de Maps que ya tienes.

### undetected-chromedriver
**Repo:** `https://github.com/ultrafunkamsterdam/undetected_chromedriver`

El clásico. Selenium parcheado contra Cloudflare, DataDome, Imperva. Sigue funcionando para casos no extremos y es el que más tutoriales tiene en español.

**Si tu audiencia es marketer principiante, empezarías por este** en clase porque hay infinita documentación.

### SeleniumBase UC Mode
**Repo:** `https://github.com/seleniumbase/SeleniumBase`

Framework completo sobre Selenium con UC Mode incluido. Más alto nivel, menos boilerplate. Bueno para perfiles que no quieren pelearse con configuración de drivers.

### Crawlee
**Repo:** `https://github.com/apify/crawlee`

De Apify (Node.js y Python). No es stealth puro pero gestiona pools de proxies, sesiones, retries y rate limits de serie. Lo que buscas si vas a hacer scraping a escala.

### Bonus — para el caso específico de Google Maps tras el "limited view"

- **google-reviews-scraper-pro** — Bypassan el limited view navegando vía búsqueda en lugar de URL directa. Patrón de inspiración más que código a copiar tal cual.
- **Google Places API oficial** — No es stealth pero el campo `user_ratings_total` lo da sin restricción y sin riesgo de baneo. Para muchos análisis de competidores locales, **es la opción correcta** que parece "menos hacker" pero es la que un cliente firmaría sin pestañear.

---

## 2. MCPs listos para enchufar

Estos los instalas en Claude Code con `claude mcp add ...` y de pronto el agente puede hacer las tareas sin escribir código.

### SiteAudit MCP
**Repo:** `https://github.com/vdalhambra/siteaudit-mcp`

El más completo y vivo. Tres herramientas: `lighthouse_audit`, `check_links`, `check_robots_txt`.

Versión hospedada gratis (100 audits/mes) en MCPize, o self-hosted ilimitado.

```json
{
  "mcpServers": {
    "siteaudit": {
      "url": "https://siteaudit-mcp.mcpize.run/mcp"
    }
  }
}
```

*"Run a Lighthouse audit on competitor.com"* y te lo da. Para clase es ideal porque no requiere instalación.

### mcp-seo-audit (GiorgiKemo)
**Repo:** `https://github.com/GiorgiKemo/mcp-seo-audit`

**El que mejor encaja con análisis de competidores.** 30 herramientas:
- Google Search Console
- Indexing API
- Chrome UX Report (CrUX)
- PageSpeed Insights
- Lighthouse local
- robots.txt
- **sitemap analysis**
- **on-page SEO con Open Graph y Twitter Cards**
- crawl audits
- detección de canibalización de keywords
- "striking distance keywords"

Cubre todos los puntos del análisis (sitemaps, OG, PageSpeed, click en URLs) en un único MCP. Se instala en Python con uv/pip.

### PageSpeed Insights MCP (ruslanlap)
**Repo:** `https://github.com/ruslanlap/pagespeed-insights-mcp`

Especializado en performance. Devuelve scores Lighthouse, Core Web Vitals, screenshots de la timeline, network waterfall y recomendaciones priorizadas.

Útil cuando solo te interesa la parte de velocidad.

### Lighthouse MCP Server (Daniel Sogl)
**Repo:** `https://github.com/danielsogl/lighthouse-mcp-server`

13+ tools, comparativas mobile vs desktop, security audits, budget audits, soporte de perfiles persistentes (puedes auditar dashboard logado del cliente).

```json
{
  "mcpServers": {
    "lighthouse": {
      "command": "npx",
      "args": ["@danielsogl/lighthouse-mcp@latest"]
    }
  }
}
```

### Playwright MCP + Chrome DevTools MCP

Lo básico para "haz clic en URLs y arranca navegador". Combinarlo con SiteAudit MCP da el mejor de los dos mundos: el agente decide cuándo navega manualmente vs cuándo lanza una auditoría completa.

```bash
claude mcp add playwright -s user -- npx @playwright/mcp@latest
claude mcp add chrome-devtools -s user -- npx chrome-devtools-mcp@latest
```

---

## 3. Skills custom para la clase

Tres skills creadas específicamente para el flujo de YinyangSEO. Están en `../03-skills/`:

### Skill A — `competitor-local-seo-audit`
Dado un negocio local, extrae top 10 competidores en GBP, audita PageSpeed, OG tags, schema, sitemap y robots de cada uno, y genera informe comparativo en docx.

### Skill B — `gbp-grid-extractor`
Para una keyword y ubicación, lanza un grid de búsquedas (estilo GEOGRIDS), captura las top 3 en cada celda y devuelve mapa de calor + JSON de resultados.

### Skill C — `serp-pattern-detector`
Dada una keyword + zona geográfica, analiza top 10 SERPs orgánicos + top 3 de Maps + AI Overview si lo hay. Detecta patrones de cómo está clasificando Google.

**Esta es la que mejor demuestra el primer punto de la clase: "detectar patrones de comportamiento de Google".**

---

## 4. Stack recomendado para el demo en directo

Ver diagrama: `stack-clase-5-niveles.png`

5 niveles ordenados de menor a mayor complejidad:

1. **SiteAudit MCP hospedado** — Apertura suave, zero install
2. **mcp-seo-audit self-hosted** — Profundidad técnica, 30 herramientas
3. **Playwright MCP + Chrome DevTools MCP** — Navegación agéntica
4. **Nodriver / Patchright / Camoufox** — Cuando Google bloquea, narrativa
5. **Skill custom** — El cierre WOW factor

---

## 5. Avisos para clase

- Los repos stealth (Nodriver, Camoufox, Patchright) son **zona gris**. Si los enseñas, marca claramente la diferencia entre uso ético (analítica competitiva, propio sitio) vs uso prohibido por términos. La audiencia te creerá más si lo dejas explícito.
- El "limited view" de Google Maps de febrero 2026 sigue activo. Es un buen ejemplo en clase de **por qué los stacks se quedan obsoletos cada 3 meses**.
- La Google Places API oficial cuesta ~$17 por 1.000 llamadas Place Details. Para muchos casos compensa frente a montar un scraper.
- Las skills custom **están sin probar todavía**. Recomendado: una pasada esta semana con un cliente real (SuperTOP, por ejemplo) antes de la clase.

---

## 6. Comparativa de herramientas tradicionales vs stack agéntico

Para vender la propuesta a la audiencia, esta tabla ayuda:

| Tarea | Herramienta tradicional | Coste mensual | Stack agéntico (Claude Code + MCPs) |
|---|---|---|---|
| Auditoría técnica web | Screaming Frog Pro | ~17€/mes | mcp-seo-audit (gratis self-hosted) |
| Análisis competencia SERP | Ahrefs Lite | ~99€/mes | serp-pattern-detector skill |
| Grid de rankings local | Local Falcon | ~24€/mes | gbp-grid-extractor skill |
| Auditoría Lighthouse | Manual o GTmetrix | 0-15€/mes | SiteAudit MCP (gratis) |
| Análisis competidores GBP | BrightLocal | ~35€/mes | competitor-local-seo-audit skill |

**Total tradicional:** ~190€/mes en suscripciones SaaS
**Total agéntico:** Claude Pro $20/mes + APIs según uso (~$10-30 estimado)

El argumento no es "más barato" (que también) sino "más adaptable". Las herramientas SaaS te dan lo que ofrecen. El stack agéntico te da lo que pidas, en el formato que pidas, integrado con tu proceso real.
