---
name: local-seo-pattern-aggregator
description: Toma los outputs de local-pack-multi-city, gbp-deep-profile y web-pattern-extractor y detecta qué tienen en común los negocios que dominan el Local Pack frente al resto. Devuelve un "patrón ganador" con hipótesis priorizadas. Úsala SIEMPRE que el usuario pida "qué patrones detectas en el top 3", "qué tienen en común los que rankean", "qué premia Google en este nicho", "agrupa los datos y dime patrones" o tras correr las 3 skills anteriores. Es la skill que convierte datos brutos en hipótesis accionables.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# Local SEO · Pattern Aggregator

Es **la pieza clave del flujo**. Cierra el ciclo de investigación: combina señales de Local Pack + GBP + Web y detecta **qué hace ganar** en este vertical/ciudad.

## Inputs

- `data/local-pack/{kw}/{date}/consolidated.json` ← de `local-pack-multi-city`
- `data/gbp-profiles/_matrix.csv` ← de `gbp-deep-profile`
- `data/web-patterns/{kw}/{date}/matrix.csv` ← de `web-pattern-extractor`
- **Umbral de "top"** · qué consideramos *top* (default: aparición en pack en ≥ 60 % de las ciudades capturadas).

## Proceso

1. **Joinear** los tres datasets por `place_id` (Local Pack ↔ GBP) y por `domain` (GBP web ↔ Web Patterns).
2. **Segmentar:**
   - **Grupo A · Ganadores:** negocios que aparecen en pack en ≥ X ciudades.
   - **Grupo B · Resto:** los demás detectados.
3. **Sobre-representación de features** (Grupo A vs B):
   - Test estadístico simple (chi-cuadrado / diferencia de proporciones) para cada feature booleana.
   - Para numéricas: medianas y percentiles.
4. **Detectar patrones consistentes:**
   - **GBP:** ¿categoría primaria concreta? ¿N atributos mínimos? ¿reviews/mes? ¿posts recientes?
   - **Web:** ¿LocalBusiness schema completo? ¿FAQ con N preguntas? ¿hero con CTA telefónico? ¿`<h1>` con keyword + ciudad? ¿servicios listados ≥ N? ¿LCP < 2.5s?
   - **Cruce:** ¿hay correlación entre `total_reviews` y `pack_appearances`?
5. **Priorizar por impacto + facilidad:**
   - **Impacto:** diferencia de proporción × tamaño del Grupo A.
   - **Facilidad:** ¿es algo replicable en una landing nueva? (las reviews no, el schema sí).
6. **Generar hipótesis ranqueadas.**

## Herramientas

- Python con `pandas` + `scipy.stats` (en sandbox).
- LLM para etiquetar "categoría de hipótesis" y redactar la hipótesis en lenguaje claro.
- Opcional: `data:statistical-analysis` skill para tests de significación.

## Salida

```
data/patterns/{kw}/{date}/
├── group-A-winners.csv          ← negocios ganadores
├── group-B-rest.csv
├── feature-comparison.csv       ← cada feature, % en A, % en B, diff, p-value
├── hypotheses.md                ← hipótesis priorizadas en lenguaje natural
└── summary-card.md              ← resumen ejecutivo de 1 página
```

**`hypotheses.md`** ejemplo:

```
## Hipótesis priorizadas — cerrajero 24h × 5 ciudades

1. [HIGH · easy] El 90 % del top 3 tiene LocalBusiness schema con `openingHoursSpecification`
   completo (24/7). Solo el 35 % del resto. → ACCIONABLE en blueprint.
2. [HIGH · medium] El 80 % del top 3 lista ≥ 8 servicios estructurados. El resto: 3.
3. [MEDIUM · hard] El top 3 tiene rating ≥ 4.7 con > 200 reviews. → no replicable a corto.
4. [MEDIUM · easy] El 70 % del top 3 tiene FAQ on-page con `FAQPage` schema y ≥ 6 preguntas.
5. ...
```

## Calidad / QA

- Si `len(Grupo A) < 5` → muestra demasiado pequeña, advertir al usuario.
- Marcar features con `p-value > 0.1` como "no significativas".
- Excluir features con `coverage < 50 %` (no extraídas en suficientes negocios).
- Pedir confirmación al usuario antes de pasar a `web-blueprint-generator` — el blueprint depende de las hipótesis HIGH.

## Para qué se usa después

→ Las hipótesis HIGH + easy alimentan directamente [`web-blueprint-generator`](../web-blueprint-generator/SKILL.md), que las traduce a estructura de URLs, schema y secciones.
