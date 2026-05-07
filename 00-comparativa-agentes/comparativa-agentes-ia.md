# Comparativa de Agentes IA para Diseño Web

**Para clase 1 del itinerario YinyangSEO** · Audiencia: SEOs/marketers que tocan código a ratos
**Datos verificados a:** mayo 2026

---

## Criterio para la audiencia

La barrera principal no es el modelo, es la **superficie**. CLI puro (Claude Code, Codex CLI, OpenCode) intimida a quien no vive en terminal. IDE con preview y navegador integrado (Trae SOLO, Windsurf, Cursor) gana en facilidad.

El ganador para SEOs/marketers existe y se llama **Trae SOLO** — encapsula editor + terminal + navegador + docs en una UI única, justo el flujo del demo de browser testing.

---

## Tabla comparativa

| Agente | Precio entrada | Modelos | MCP/Skills navegador | Vista previa | Navegador embebido para test | Curva SEO/marketer |
|---|---|---|---|---|---|---|
| **Claude Code** | $20/mes Pro · $100-200 Max | Sonnet 4.6, Opus 4.7 | ✅ Maduro (Playwright, Chrome DevTools, Claude in Chrome) | ❌ No nativa (sirve dev server) | Vía MCP externo | Alta (CLI puro) |
| **OpenAI Codex** | $20/mes (ChatGPT Plus) · $200 Pro | GPT-5.4, GPT-5.3-Codex, mini variants | ✅ MCP soportado (Playwright, Chrome DevTools) | ⚠️ En Codex Cloud/IDE; CLI no | Vía MCP | Media (CLI + IDE + Web + App) |
| **Trae SOLO** | Gratis · Lite $3 · Pro $10 | Claude 3.7/4, GPT-4o/5.4, DeepSeek, Gemini | ✅ MCP nativo + agentes custom | ✅ **Sí, integrada** | ✅ **Sí, integrado** | **Baja** |
| **OpenCode** | Gratis (BYOK) · Go $5→$10/mes | 75+ providers (BYOK) o modelos open vía Go | ✅ MCP local y remoto | ❌ No nativa | Vía MCP | Muy alta (TUI terminal) |
| **Cursor** | Gratis · Pro $20 · Ultra $200 | Claude, GPT, Gemini, Composer 2 propio | ✅ MCP maduro + Design Mode | ⚠️ Limitada | Vía MCP | Media (IDE) |
| **Windsurf** | Gratis · Pro $20 · Max $200 | SWE-1.5 propio + frontier models | ✅ MCP + agent-browser nativo | ✅ **Preview pane integrado** | ✅ **Sí, agent browser** | Media (IDE) |

---

## Fichas detalladas

### Claude Code

CLI nativo, sin IDE propio (extensión para VS Code/JetBrains). El comando `claude mcp add chrome-devtools` o `claude mcp add playwright` es el patrón estándar para que Claude abra Chrome, navegue, capture, lea la consola, e itere.

**Stack recomendado por la comunidad:**
- Chrome DevTools MCP (debug/performance)
- Claude in Chrome (sesiones autenticadas, requiere plan de pago)
- Playwright MCP (cross-browser)

**Precios:**
- Pro $20/mes (Claude Code en terminal, web y desktop)
- Max 5x $100/mes
- Max 20x $200/mes
- API pay-as-you-go: Sonnet 4.6 $3/MTok input, $15/MTok output

**Avisos para clase:**
- En abril 2026 hubo lío de precios (Anthropic intentó subir Claude Code solo a Max, dieron marcha atrás en horas).
- Aún hay regresión de tokens en v2.1.100+ — recomendar v2.1.34 o instalar vía npm.

---

### OpenAI Codex

Familia de productos (CLI, IDE extension, Web, app móvil) bajo un mismo paraguas. Incluido en ChatGPT Plus $20, Pro $200, Business $30/usuario.

Desde 2 abril 2026 pasó de pricing por mensaje a pricing por **tokens (créditos)**, lo cual lo acerca al modelo Anthropic.

**Promo activa:** Pro tiene 2x rate limit hasta 31 mayo 2026.

Soporta MCP, incluyendo Chrome DevTools MCP y Playwright:
```bash
codex mcp add chrome-devtools -- npx chrome-devtools-mcp@latest
```

**Punto fuerte:** si tu audiencia ya paga ChatGPT Plus, lo tiene incluido sin coste extra.
**Punto débil:** la fragmentación entre superficies (CLI, IDE, Web, App) puede confundir.

---

### Trae SOLO (ByteDance) — **Candidato estrella para clase**

SOLO mode integra editor + terminal + **navegador** + documentación en un workspace único. Genera PRD, código frontend/backend, lo prueba en su propio browser embebido, y permite "Select & Edit" visual sobre la página renderizada (clic + lenguaje natural sobre el elemento). Despliegue a Vercel desde dentro.

**Precios:**
- Gratis (con modelos premium incluidos: Claude, GPT-4o, DeepSeek)
- Lite $3/mes
- Pro $10/mes

**Caveat crítico para mencionar en clase:**
- ByteDance retiene datos personales 5 años tras cierre de cuenta.
- Telemetría sin opt-out.
- Sin certificaciones enterprise.
- Para proyectos personales y formación está bien, para código de cliente sensible no.

---

### OpenCode

Open source, agnóstico de proveedor. CLI con TUI (interfaz textual). BYOK (trae tu propia clave API) o suscripción **Go $5 primer mes / $10/mes** con acceso a 12+ modelos open-source (DeepSeek V4, Kimi K2, Qwen3, GLM-5.1, MiniMax).

Soporta MCP local y remoto, también agentes personalizados vía archivos markdown.

**Para audiencia SEO/marketer:** descártalo salvo como mención de "alternativa libre/sin lock-in". Curva de aprendizaje alta, no tiene preview ni navegador integrado de fábrica.

---

### Cursor

IDE fork de VS Code. Pro $20, Ultra $200. Composer 2 propio (200 tok/s). MCP maduro, Design Mode visual añadido en Cursor 3 (abril 2026).

Sigue siendo la elección por defecto para muchos devs. Para SEOs es una opción decente pero menos integrado que Trae SOLO.

---

### Windsurf

Otro IDE fork de VS Code, ahora propiedad de Cognition (los de Devin) tras el drama OpenAI/Google de 2025.

**Tiene panel de preview nativo y agent-browser** que envía logs y elementos directamente al agente Cascade (cumple los 4 requisitos sin instalar MCPs adicionales). $20/mes Pro, modelo SWE-1.5 a 950 tok/s gratis durante promoción.

Buen candidato secundario para clase.

---

## Recomendación de orden para presentación

De **menor a mayor fricción**, que es como lo van a entender los asistentes:

1. **Trae SOLO** — "Todo en uno, gratis, baja barrera". Demo en vivo del flujo: prompt → PRD → código → preview → ajuste visual → deploy. Es el wow factor.
2. **Windsurf** — "Igual de visual, marca occidental, sin la pega de ByteDance". Punto medio para quien tiene reparos con datos en China.
3. **Cursor** — "El estándar del sector si decides especializarte".
4. **Claude Code + Chrome DevTools MCP** — "Cuando quieras potencia y control total" (tu setup). Aquí hablas del MCP de navegador, que cubre la capacidad de arrancar navegadores con los 3 MCPs canónicos: Chrome DevTools (debug), Playwright (E2E), Claude in Chrome (sesiones logadas).
5. **OpenAI Codex** — "Si ya pagas ChatGPT Plus, lo tienes incluido".
6. **OpenCode** — Mención breve como "opción libre/BYOK para perfil técnico".

---

## Mapa rápido de los 4 requisitos técnicos

| Requisito | Quien lo cumple |
|---|---|
| **Skills/MCP de navegador** | Todos. Maduros: Claude Code, Cursor, Codex. Nativo sin instalar: Trae SOLO, Windsurf. |
| **Generación de código web** | Todos cumplen. Trae SOLO y Cursor inclinados a Next.js/React; Claude Code agnóstico. |
| **Vista previa nativa** | Solo **Trae SOLO** y **Windsurf**. El resto requiere arrancar dev server manualmente. |
| **Navegador para pruebas** | Nativo en **Trae SOLO** y **Windsurf**. En Claude Code es excelente vía Chrome DevTools MCP. |

---

## Aviso para repasar antes de clase

Los precios cambian rápido. Anthropic ha tocado el pricing dos veces en 30 días, OpenAI cambió a token-based el 2 de abril 2026, Trae cambió a token-based en febrero 2026.

**Confirma el día anterior** los tres puntos de precio: Claude Pro $20, ChatGPT Plus $20, Trae Pro $10.
