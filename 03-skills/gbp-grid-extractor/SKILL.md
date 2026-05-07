---
name: gbp-grid-extractor
description: Extrae rankings de Google Business Profile en cuadrícula geográfica (grid) para una keyword y zona. Úsala SIEMPRE que el usuario pida hacer un grid, geogrid, mapa de calor de rankings, ver visibilidad GBP por zonas, analizar variación geográfica de posiciones, o frases como "haz un grid de [keyword] en [ciudad]", "cómo rankea [negocio] por la zona", "mapa de visibilidad local", "geogrid para [cliente]". También para detectar áreas de oportunidad y radio efectivo de un GBP. Es la skill que replica el trabajo de herramientas tipo Local Falcon, Map Labs o GEOGRIDS de forma agéntica.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# GBP Grid Extractor

Genera un grid de búsquedas geolocalizadas para medir cómo varía el ranking de un negocio (y su competencia) según el punto desde el que se busca.

## Concepto

Un grid es una cuadrícula de N×N puntos centrada en una ubicación. En cada punto se ejecuta una búsqueda de Google Maps simulando estar físicamente ahí. Para cada punto se anotan los top 3 (o top X) resultados de Maps. El resultado: un mapa de calor de visibilidad por zonas.

## Inputs esperados

- **Keyword**: la consulta a evaluar (ej. "cerrajero 24h")
- **Negocio target**: nombre o Place ID del negocio cuyo ranking quieres medir
- **Centro del grid**: dirección, coordenadas, o nombre del lugar (ej. "Plaça Catalunya, Sabadell")
- **Tamaño del grid**: 5×5 (25 puntos), 7×7 (49), 9×9 (81). Por defecto **7×7**
- **Radio total**: distancia desde el centro al borde. Por defecto **3 km** (típico negocio urbano local)
- **Top X a capturar**: por defecto **top 3** de Maps en cada punto

Si falta alguno, pregunta. Especialmente keyword y centro: sin ellos no hay grid.

## Paso 1 — Generar las coordenadas del grid

Calcular las N×N coordenadas (lat, lng) distribuidas uniformemente alrededor del centro.

**Código Python de referencia** (úsalo o adáptalo):

```python
import math

def generate_grid(center_lat, center_lng, grid_size=7, radius_km=3):
    """Genera grid_size × grid_size puntos alrededor del centro."""
    points = []
    # 1° latitud ≈ 111 km. 1° longitud ≈ 111 × cos(lat)
    deg_per_km_lat = 1 / 111
    deg_per_km_lng = 1 / (111 * math.cos(math.radians(center_lat)))
    
    step_km = (2 * radius_km) / (grid_size - 1)
    
    for i in range(grid_size):
        for j in range(grid_size):
            offset_lat = (i - (grid_size - 1) / 2) * step_km * deg_per_km_lat
            offset_lng = (j - (grid_size - 1) / 2) * step_km * deg_per_km_lng
            points.append({
                'row': i,
                'col': j,
                'lat': center_lat + offset_lat,
                'lng': center_lng + offset_lng
            })
    return points
```

## Paso 2 — Buscar en cada punto

Para cada punto del grid, ejecuta una búsqueda Maps localizada. Tres opciones por orden de robustez:

**Opción A (preferida): Google Places API Nearby Search**
- Endpoint: `places.googleapis.com/v1/places:searchNearby`
- Parámetros: `locationRestriction.circle.center` con lat/lng del punto, `radius=200` (sub-radio pequeño para forzar localización), `textQuery` con la keyword
- Ventaja: oficial, no se banea, devuelve Place IDs estables
- Coste: ~$32 por 1000 llamadas → grid 7×7 son 49 llamadas → ~$1.6 por grid

**Opción B: Scraping de Maps con Patchright + parámetro `!3d{lat}!4d{lng}`**
- URL: `https://www.google.com/maps/search/{keyword}/@{lat},{lng},15z`
- Capturar top X de la columna izquierda
- Recordar el limited view de febrero 2026: navegar siempre vía búsqueda, nunca URL directa de ficha
- Riesgo: puede romper en cualquier momento por cambios de Google

**Opción C: SerpAPI Local**
- Si el usuario tiene cuenta SerpAPI, usar el endpoint `google_local` con coordenadas
- Más caro pero más estable que scraping propio

## Paso 3 — Almacenar resultados

Estructura de datos por celda:

```json
{
  "row": 3,
  "col": 4,
  "lat": 41.5478,
  "lng": 2.1042,
  "results": [
    {"rank": 1, "name": "Cerrajero X", "place_id": "ChIJ...", "rating": 4.8, "reviews": 145},
    {"rank": 2, "name": "Cerrajero Y", "place_id": "ChIJ...", "rating": 4.5, "reviews": 89},
    {"rank": 3, "name": "Cerrajero Z", "place_id": "ChIJ...", "rating": 4.9, "reviews": 230}
  ],
  "target_rank": 7,
  "target_in_top_3": false
}
```

Guarda el JSON completo del grid en disco antes de generar la visualización. Si el proceso se rompe, debe ser reanudable.

## Paso 4 — Calcular métricas

Sobre el grid completo:

- **AVR (Average Rank)**: media de la posición del target en los puntos donde aparece
- **ATGR (Average Top 3 Rank)**: % de puntos donde el target aparece en top 3
- **SoLV (Share of Local Voice)**: % medio de visibilidad ponderado
- **Radio efectivo**: distancia al centro hasta la cual el target aparece en top 3
- **Competidores dominantes**: top 3 negocios que aparecen en más celdas del grid

## Paso 5 — Visualizar

Genera dos outputs:

**Visual 1: Mapa de calor**
- HTML con grid de N×N celdas
- Color por celda según ranking del target: verde top 3, amarillo top 10, rojo no aparece
- Tooltip al pasar: muestra los top 3 reales de esa celda
- Usa SVG o el visualizer de Claude

**Visual 2: Tabla resumen**
- Métricas (AVR, ATGR, SoLV, radio efectivo)
- Top 5 competidores que aparecen en más celdas
- Recomendación: zonas geográficas donde el target tiene gap → contenido localizado, ajuste de service area, etc.

## Paso 6 — Entregable

Si el usuario lo pide o si el contexto sugiere entregable a cliente, genera **docx** con la skill `docx` que incluya:
- Portada con keyword, fecha, centro del grid
- Imagen del mapa de calor (renderizar el SVG a PNG primero)
- Tabla de métricas
- Análisis competitivo de los top 5 dominantes
- Recomendaciones accionables

## Reglas

- **Nunca dispares un grid >9×9 sin avisar del coste**. Un 11×11 son 121 llamadas, sale caro y tarda mucho.
- **Si usas Places API**, advierte del coste estimado antes de ejecutar.
- **Si usas scraping**, mete delays aleatorios entre 3-7 segundos por celda. Sin delays, ban garantizado.
- **Cachea resultados**: si el mismo grid se repite en 24h, reusa el JSON guardado a menos que el usuario pida `--force-refresh`.
- **Place IDs > nombres**: identifica negocios por Place ID, no por nombre. Los nombres tienen variaciones ("S.L.", "&", emojis) que rompen comparaciones entre celdas.

## Workflow resumido

```
1. Confirmar keyword, target, centro, tamaño y radio
2. Estimar coste (si API) o tiempo (si scraping). Confirmar.
3. Generar coordenadas N×N
4. Iterar puntos: buscar, capturar top X, guardar
5. Calcular métricas (AVR, ATGR, SoLV, radio efectivo)
6. Visualizar: mapa de calor + tabla
7. Si se pide: docx final con `present_files`
```

## Notas de integración con GEOGRIDS

Si el usuario tiene proyecto GEOGRIDS (Claude Code) en disco, **lee primero el código existente** antes de implementar de cero. Probablemente ya tenga la lógica del grid y quiera reutilizar/mejorar, no reescribir. Pregunta: "¿integro esto con tu proyecto GEOGRIDS o lo hago como skill independiente?"
