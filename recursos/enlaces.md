# Recursos y enlaces

> Curado para esta clase. Mezcla de:
> - 🎓 Mencionados en el .pptx / material interno.
> - 🛠️ Recursos extra recomendados (oficiales).

---

## Agentes y entornos de desarrollo

| 🎓 | [Trae AI](https://trae.ai/) | All-in-one con preview y navegador. Generó el deck. |
| 🎓 | [Trae SOLO](https://www.trae.ai/solo) | Modo agente del propio Trae. |
| 🎓 | [Windsurf](https://windsurf.com/) | IDE con preview y agent-browser. |
| 🎓 | [Cursor](https://cursor.com/) | Standard IDE con MCP maduro. |
| 🎓 | [Claude Code](https://www.anthropic.com/claude-code) | CLI agéntica de Anthropic. |
| 🎓 | [OpenAI Codex](https://openai.com/codex/) | Coding agent de OpenAI dentro de ChatGPT. |
| 🎓 | [OpenCode](https://opencode.ai/) | Alternativa libre / BYOK. |
| 🛠️ | [Aider](https://aider.chat/) | Pair programming con LLMs en CLI. |
| 🛠️ | [Cline](https://cline.bot/) | Extensión VS Code. |

## MCPs SEO (mencionados en la clase)

| 🎓 | [SiteAudit MCP](https://github.com/cyberagiinc/DevDocs) | Hospedado, cero instalación. Lighthouse + robots + links. |
| 🎓 | [mcp-seo-audit (GiorgiKemo)](https://github.com/GiorgiKemo/mcp-seo-audit) | Self-hosted con GSC, CrUX, PageSpeed, sitemap. |
| 🎓 | [PageSpeed Insights MCP (ruslanlap)](https://github.com/ruslanlap/pagespeed-insights-mcp) | PSI por API oficial. |
| 🎓 | [Lighthouse MCP Server](https://github.com/danielsogl/lighthouse-mcp-server) | Auditorías Lighthouse desde el agente. |
| 🎓 | [Playwright MCP](https://github.com/microsoft/playwright-mcp) | Navegación agéntica. Microsoft oficial. |
| 🎓 | [Chrome DevTools MCP](https://github.com/ChromeDevTools/chrome-devtools-mcp) | DevTools como tool calls. Google oficial. |

## Repos stealth / antibloqueo (con criterio ético)

> ⚠️ Usar solo con contexto, permisos y límite claro. Priorizar APIs oficiales cuando existan.

| 🎓 | [Nodriver](https://github.com/ultrafunkamsterdam/nodriver) | Sucesor de undetected-chromedriver, basado en CDP. |
| 🎓 | [Camoufox](https://github.com/daijro/camoufox) | Firefox stealth con perfilado anti-fingerprinting. |
| 🎓 | [Patchright](https://github.com/Kaliiiiiiiiii-Vinyzu/patchright) | Fork stealth de Playwright. |
| 🎓 | [undetected-chromedriver](https://github.com/ultrafunkamsterdam/undetected-chromedriver) | Histórico, todavía referencia. |
| 🎓 | [SeleniumBase UC Mode](https://github.com/seleniumbase/SeleniumBase) | Modo evasivo dentro de SeleniumBase. |
| 🎓 | [Crawlee](https://github.com/apify/crawlee) | Framework de scraping responsable. |

## Navegadores cloud para agentes (sin instalación local)

> Útiles cuando la audiencia no técnica no quiere instalar Playwright. El navegador corre en cloud y el agente lo controla por API.

| 🛠️ | [Browserbase](https://www.browserbase.com/) | Navegador cloud + MCP para Claude/Cursor. Live View para ver al agente trabajando. |
| 🛠️ | [Steel.dev](https://steel.dev/) | Open source + cloud. API simple para agentes. |
| 🛠️ | [Hyperbrowser](https://hyperbrowser.ai/) | Headless browser as a service con anti-detection. |
| 🛠️ | [Browser Use](https://github.com/browser-use/browser-use) | Librería que hace al navegador "agent-friendly". |

## Web → markdown para alimentar al agente

> Convierte URLs en contexto limpio para LLMs. Más barato y rápido que renderizar todo con Playwright.

| 🛠️ | [Firecrawl](https://www.firecrawl.dev/) | URL → markdown estructurado. Tiene MCP oficial. |
| 🛠️ | [Jina Reader](https://r.jina.ai/) | Pones `https://r.jina.ai/` delante de cualquier URL. Gratis. |
| 🛠️ | [Tavily Search API](https://tavily.com/) | Búsqueda web + extracción optimizada para LLMs. |
| 🛠️ | [Perplexity Sonar API](https://docs.perplexity.ai/) | Búsqueda con razonamiento integrado. |
| 🛠️ | [Apify](https://apify.com/) | Marketplace de actores de scraping con MCP. |
| 🛠️ | [Bright Data MCP](https://github.com/brightdata-com/brightdata-mcp) | Proxies y scraping a escala con MCP. |

## APIs oficiales (preferir cuando existan)

| 🛠️ | [Google Places API](https://developers.google.com/maps/documentation/places/web-service/overview) | Datos GBP estables. |
| 🛠️ | [Google Search Console API](https://developers.google.com/webmaster-tools/v1/api_reference_index) | Cobertura, impresiones, queries. |
| 🛠️ | [PageSpeed Insights API](https://developers.google.com/speed/docs/insights/v5/get-started) | Core Web Vitals + Lighthouse por URL. |
| 🛠️ | [Chrome UX Report (CrUX)](https://developer.chrome.com/docs/crux/api) | Datos reales de campo. |
| 🛠️ | [SerpAPI](https://serpapi.com/) | SERPs estructuradas (de pago). |
| 🛠️ | [DataForSEO](https://dataforseo.com/) | API de datos SEO con créditos. |

## Modelos y plataformas

| 🛠️ | [Anthropic API](https://www.anthropic.com/api) | Claude Opus / Sonnet / Haiku. |
| 🛠️ | [OpenAI API](https://platform.openai.com/) | GPT-5, ChatGPT Plus, Codex. |
| 🛠️ | [Google AI for developers](https://ai.google.dev/) | Gemini API. |
| 🛠️ | [Ollama](https://ollama.com/) | LLMs locales open source. |
| 🛠️ | [LM Studio](https://lmstudio.ai/) | LLMs locales con UI. |

## Web dev y deploy (stack recomendado: Astro)

| 🛠️ | [Astro](https://astro.build/) | Framework estático, ideal para SEO local. **Stack por defecto del curso.** |
| 🛠️ | [accessible-astro-starter](https://github.com/markteekman/accessible-astro-starter) | Starter accesible y rápido. Buen punto de partida. |
| 🛠️ | [@astrojs/sitemap](https://docs.astro.build/en/guides/integrations-guide/sitemap/) | Sitemap automático para Astro. |
| 🛠️ | [astro-seo](https://github.com/jonasmerlin/astro-seo) | Componentes SEO/Open Graph para Astro. |
| 🛠️ | [Next.js](https://nextjs.org/) | Alternativa con React (SSR/SSG). |
| 🛠️ | [next-sitemap](https://github.com/iamvishnusankar/next-sitemap) | Sitemap automático para Next. |
| 🛠️ | [Vercel](https://vercel.com/) | Deploy + previews por PR. |
| 🛠️ | [Cloudflare Pages](https://pages.cloudflare.com/) | Deploy estático con red global. |
| 🛠️ | [Netlify](https://www.netlify.com/) | Deploy + functions. |

## Componentes UI y schema

| 🛠️ | [schema-dts](https://github.com/google/schema-dts) | Tipos TypeScript oficiales de schema.org. **Para validar JSON-LD antes de escribirlo.** |
| 🛠️ | [Schema.org Validator](https://validator.schema.org/) | Validador online de JSON-LD. |
| 🛠️ | [Local Business Schema templates](https://schema.org/LocalBusiness) | Referencia oficial de tipos. |
| 🛠️ | [Tailwind UI](https://tailwindui.com/) | Patterns de hero, services, FAQ, CTA. |
| 🛠️ | [DaisyUI](https://daisyui.com/) | Componentes Tailwind open source. |
| 🛠️ | [shadcn/ui](https://ui.shadcn.com/) | Componentes React copy-paste de alta calidad. |

## Performance y QA

| 🛠️ | [Lighthouse CI](https://github.com/treosh/lighthouse-ci-action) | GitHub Action: budgets de Core Web Vitals en cada PR. |
| 🛠️ | [Lighthouse npm](https://github.com/GoogleChrome/lighthouse) | Lighthouse local programable. |
| 🛠️ | [Web Vitals JS](https://github.com/GoogleChrome/web-vitals) | Mide INP, LCP, CLS reales en producción. |

## Analytics privacy-friendly (alternativa GA4)

| 🛠️ | [Plausible](https://plausible.io/) | Self-hostable o SaaS. Sin cookies. |
| 🛠️ | [Umami](https://umami.is/) | Open source. Self-host fácil. |

## Lecturas útiles

| 🛠️ | [MCP spec](https://modelcontextprotocol.io/) | Especificación oficial de MCP. |
| 🛠️ | [Anthropic docs · Claude Code](https://docs.claude.com/en/docs/claude-code) | Documentación oficial. |
| 🛠️ | [Awesome MCP servers](https://github.com/modelcontextprotocol/servers) | Catálogo oficial. |
| 🛠️ | [GitHub Skills](https://skills.github.com/) | Aprender Git/GitHub paso a paso. |

---

## Convención de iconos

- 🎓 Mencionado en la clase / .pptx / material interno.
- 🛠️ Recurso extra recomendado (oficial).
