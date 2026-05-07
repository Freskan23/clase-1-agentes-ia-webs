---
name: serp-pattern-detector
description: Analiza SERPs de Google para una keyword y detecta patrones de cómo Google clasifica resultados. Úsala SIEMPRE que el usuario pida analizar SERP, ver qué prefiere Google, detectar patrones de ranking, hacer ingeniería inversa de un nicho, entender por qué rankean los que rankean, comparar AI Overview con orgánico, o frases como "qué patrones detectas en esta SERP", "por qué rankea X", "cómo está rankeando Google [keyword]", "qué tienen en común el top 10 de [keyword]", "ingeniería inversa de [keyword]", "research de [nicho]". Es la skill para detectar señales de algoritmo y construir hipótesis de ranking.
---

# SERP Pattern Detector

Análisis sistemático de una SERP para detectar patrones de comportamiento del algoritmo de Google. El objetivo: convertir una página de resultados en hipótesis accionables sobre qué está priorizando Google ahora mismo en ese nicho.

## Inputs esperados

- **Keyword**: la consulta a analizar
- **Geo**: país/región/ciudad desde la que medir (importa: la SERP es distinta desde Madrid vs desde México DF)
- **Idioma**: por defecto, deducir del país
- **Dispositivo**: mobile o desktop. Por defecto **mobile** (es el que indexa Google)
- **Número de resultados a analizar**: por defecto top 10 orgánico + top 3 GBP (Map Pack) si aplica

Si la keyword es ambigua (ej. "manzana" → fruta o tecnología), pregunta intent antes.

## Paso 1 — Capturar la SERP completa

Necesitas un snapshot exhaustivo, no solo los 10 azules. Captura:

- **Top 10 orgánico** con: posición, URL, title que muestra Google (puede diferir del HTML), description, tipo de snippet (rich, FAQ, video thumbnail, sitelinks)
- **Map Pack / Local Pack** si aparece: top 3 GBP con name, rating, reviews, categoría
- **AI Overview / SGE** si aparece: texto del resumen, fuentes citadas (URLs)
- **Featured snippet** si aparece: tipo (párrafo, lista, tabla), URL fuente
- **People Also Ask**: las 4-8 preguntas iniciales
- **Related searches** al final
- **Imágenes/Vídeos** intercalados: posición de aparición y origen
- **Anuncios**: cuántos arriba/abajo (señal de comercialidad)

Herramientas por orden de preferencia:
1. **SerpAPI** o **DataForSEO** vía MCP (más estable, devuelve estructura limpia)
2. **Patchright + Playwright MCP** (scraping propio con baja huella)
3. **MCP que el usuario ya tenga configurado** para SERP

Importante: Google muestra SERP distinta según ubicación, idioma del navegador, y a veces señales de cuenta. **Forzar geo via parámetros**, no fiarse del IP.

## Paso 2 — Auditar las 10 URLs orgánicas

Para cada URL del top 10, ejecuta:

**Tipo de página**:
- Homepage / Categoría / Producto / Artículo informacional / Comercial / Listicle / Comparativa / Review / Foro / Wikipedia / Reddit / YouTube

**Métricas técnicas** (con `mcp-seo-audit` o `pagespeed-insights-mcp`):
- Lighthouse mobile: Performance, SEO, Accessibility, Best Practices
- Core Web Vitals: LCP, CLS, INP

**On-page**:
- Longitud del contenido (palabras)
- Estructura H1-H6 (¿cuántos H2? ¿hay TOC?)
- Imágenes (cuántas, todas con alt)
- Videos embebidos sí/no
- Tablas/listas estructuradas

**Schema detectado**:
- Tipos JSON-LD presentes
- Si hay Article, FAQPage, HowTo, Product, Review, BreadcrumbList

**Señales de actualización**:
- Fecha de publicación visible
- Fecha de última actualización
- "Updated YYYY" en title o description

**Autoridad visible**:
- Nombre del autor con bio
- Enlaces a perfiles del autor
- Mención a fuentes/citas externas

## Paso 3 — Detectar patrones

Una vez tienes los 10 análisis, busca **señales fuertes** (>=70% de coincidencia en el top 10) y **señales débiles** (>=50%):

### Tipo de contenido dominante
¿El top 10 son artículos largos o fichas comerciales? ¿Predominan listicles? ¿Hay foros/Reddit (indicio de búsqueda informacional)?

### Longitud media
- ≤500 palabras: nicho informacional rápido
- 500-1500: equilibrado
- 1500-3000: contenido en profundidad
- >3000: SEO de "skyscraper", probablemente competitivo

Anota outliers: si 9 tienen ~2000 palabras y 1 tiene 300, ese 1 está rankeando por otra razón (autoridad de dominio, marca, brand search).

### Patrón de title tags
¿Todos llevan año? ¿Todos llevan número (top X)? ¿Todos mencionan ciudad? ¿Estructura "Keyword | Brand"?

### Patrón de schema
Si 8/10 llevan FAQPage schema, es señal de que Google premia FAQ en esta keyword.

### Patrón de freshness
Si todos los top tienen fecha <12 meses, es nicho que requiere actualización constante. Si conviven artículos viejos con nuevos, probablemente Google prima evergreen.

### Patrón de dominio
¿Cuántos dominios distintos? Si 10/10 son distintos, el nicho está abierto. Si 4 son del mismo dominio, hay un dominante absoluto.

### Patrón de entity / autor
¿Aparecen autores con bio? ¿Citan estudios? Si el nicho es YMYL (salud, finanzas, legal), la presencia de autor + fuentes citadas es señal fuerte de E-E-A-T.

### Tipos de contenido en SERP (no solo URLs)
- Si hay AI Overview → optimizar para ser citado en él (estructura clara, listas, definiciones)
- Si hay Map Pack → keyword tiene intención local
- Si hay PAA con preguntas en lenguaje natural → optimizar para responder esas preguntas literalmente
- Si hay vídeos arriba → considerar producir video (incluso embed de YouTube en la web)
- Si hay imágenes → optimizar imágenes con alt y schema ImageObject

### Cruce SGE/AI Overview
Si hay AI Overview, lista las URLs citadas. **¿Coinciden con el top 10 orgánico?** Si no, Google está usando señales distintas para AIO. Las URLs citadas en AIO suelen tener: respuesta directa al inicio, párrafos cortos, schema bien estructurado.

## Paso 4 — Hipótesis accionables

Convierte los patrones en hipótesis priorizadas para el cliente. Estructura:

```
Patrón detectado: [observación]
Confianza: [Alta / Media / Baja] (basado en % de coincidencia)
Implicación para nuestro contenido: [acción concreta]
Esfuerzo: [bajo / medio / alto]
Impacto estimado: [bajo / medio / alto]
```

Ejemplo:
```
Patrón: 8/10 incluyen FAQPage schema con 5+ preguntas
Confianza: Alta
Implicación: añadir FAQ schema a nuestra página con 6-8 preguntas
Esfuerzo: bajo
Impacto: medio (probabilidad alta de aparecer en PAA)
```

## Paso 5 — Entregable

Genera output en este orden de detalle (de menor a mayor esfuerzo):

**Nivel 1 — Respuesta inline**: si es para una conversación rápida, devuelve un resumen estructurado con tabla y top 5 hipótesis.

**Nivel 2 — Markdown / Notion**: si el usuario quiere documentar internamente, exporta `.md`.

**Nivel 3 — Docx para cliente**: usa skill `docx`. Estructura:
1. Portada (keyword, fecha, geo, dispositivo)
2. Snapshot de la SERP (descripción del paisaje)
3. Tabla con los 10 competidores y métricas clave
4. Patrones detectados (por categoría)
5. Hipótesis priorizadas
6. Plan de acción a 30 días

## Reglas

- **Distingue correlación de causación**. Que el top 10 tenga X no significa que X cause el ranking. Lenguaje correcto: "Google parece premiar X" / "el top 10 comparte X" — NUNCA "necesitas X para rankear".
- **Cita la fecha del análisis**. Las SERPs cambian semanalmente.
- **Si la SERP es muy heterogénea** (ej. mezcla foros, brands grandes, blogs nuevos), explícitamente di "no hay patrón claro, intent ambiguo" — es información valiosa.
- **Detecta canibalización** del propio cliente: si el cliente aparece 2+ veces en el top 50, marca como problema.
- **Si hay AI Overview**, capturalo en text e incluye URLs citadas. Es la señal más importante 2026.

## Workflow resumido

```
1. Confirmar keyword + geo + dispositivo + nº resultados
2. Capturar SERP completa (orgánico + Map Pack + AIO + PAA + medias)
3. Auditar las 10 URLs (Lighthouse + on-page + schema + freshness + autoridad)
4. Detectar patrones (8 categorías)
5. Generar hipótesis priorizadas
6. Entregable según nivel pedido (inline / .md / .docx)
```

## Avisos

- **No confundas "está en top 10" con "está optimizado para SEO"**. A veces algo rankea por brand, autoridad antigua, o bug del algoritmo. Marca outliers como tales.
- Si el nicho es **YMYL**, advierte al cliente que las hipótesis "atajo" son arriesgadas — Google es más conservador en salud/finanzas/legal.
- Si la keyword tiene **alta volatilidad** (cambia mucho semana a semana), recomienda repetir el análisis cada 30 días.
