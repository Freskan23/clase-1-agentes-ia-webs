---
name: local-pack-multi-city
description: Captura el Local Pack y el orgánico de Google para una keyword en N ciudades distintas y consolida los negocios únicos detectados. Úsala SIEMPRE que el usuario pida "investiga el local pack de [keyword] en estas ciudades", "qué negocios aparecen en [keyword] en Madrid, Barcelona, Valencia", "extrae rivales locales por ciudad", "snapshot SERP por ciudad" o cuando dé una lista de ciudades. Es el primer paso del flujo de investigación competitiva local.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# Local Pack · Multi-City Snapshot

Skill de **investigación masiva**: ejecuta la misma keyword en N ciudades, captura Local Pack + top orgánico de cada una y devuelve un dataset consolidado de negocios únicos para alimentar las siguientes skills (`gbp-deep-profile`, `web-pattern-extractor`).

## Inputs

- **Keyword** · la consulta a evaluar (ej. *"cerrajero 24h"*).
- **Ciudades** · lista (ej. *Sabadell, Terrassa, Barcelona, Madrid Centro, Valencia*).
- **País / idioma** · por defecto deduce del primer item.
- **Dispositivo** · `mobile` por defecto.
- **Top X orgánico** · por defecto 10.
- **Top Y Local Pack** · por defecto 3 (Map Pack estándar) + 7 si hay *"see more places"*.

Si falta keyword o lista de ciudades → preguntar antes de empezar. No inventar.

## Proceso

1. **Resolver geo de cada ciudad** → coordenadas + UULE / `gl/hl/near` parameter para forzar localización en SERP.
2. **Capturar SERP por ciudad** en este orden de preferencia:
   1. **SerpAPI / DataForSEO** (si hay key). Estable.
   2. **Tavily / Perplexity Search** para datos textuales rápidos.
   3. **Playwright MCP / Browserbase** (navegación headful con perfil geolocalizado) si hace falta el render real.
3. **Por cada SERP, extraer:**
   - Top 10 orgánico: posición, URL, title, description, dominio, tipo de snippet.
   - Top Y Local Pack: nombre GBP, lat/lng, rating, total reviews, categoría, snippet, place_id si disponible.
   - AI Overview / Featured snippet / PAA / Related (snapshot completo).
4. **Consolidar:** dedupe por `place_id` (Local Pack) y por `dominio` (orgánico).
5. **Marcar overlap:** qué negocios aparecen en ≥ N ciudades (señal fuerte de cadena / dominio multi-ciudad).
6. **Guardar dataset** en `data/local-pack/{keyword-slug}/{YYYY-MM-DD}/` con estructura JSON + CSV.

## Herramientas

- SerpAPI / DataForSEO (preferidas).
- Tavily / Perplexity Search API (alternativa).
- Playwright MCP / Browserbase (fallback con render).
- Google Places API si hay que enriquecer el `place_id`.

## Salida

```
data/local-pack/cerrajero-24h/2026-05-07/
├── raw/
│   ├── sabadell.json
│   ├── terrassa.json
│   └── barcelona.json
├── consolidated.json   ← negocios únicos con apariciones por ciudad
├── consolidated.csv    ← idem en tabular
└── overlap-report.md   ← qué negocios dominan ≥ N ciudades
```

Cada negocio único trae: `name`, `place_id`, `domain`, `categories[]`, `cities_seen[]`, `avg_rating`, `total_reviews`, `pack_positions`.

## Calidad / QA

- Verificar que cada ciudad devolvió Local Pack (si 0, marcar `local_pack_missing: true`).
- Si `total_reviews == 0` → probable *limited view* de Google → reintenta con sesión iniciada o cambia de fuente.
- Limitar a ≤ 30 ciudades por ejecución (coste/tiempo).
- Avisar al usuario del coste estimado (tokens + créditos SerpAPI) **antes de lanzar**.

## Salida típica para alimentar siguiente skill

`consolidated.json` → input directo para [`gbp-deep-profile`](../gbp-deep-profile/SKILL.md) (extraer ficha completa de cada negocio único) y [`web-pattern-extractor`](../web-pattern-extractor/SKILL.md) (analizar dominios únicos).
