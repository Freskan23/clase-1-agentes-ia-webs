---
name: gbp-deep-profile
description: Extrae la ficha completa de Google Business Profile de un negocio o lista de negocios — categorías primaria y secundarias, atributos, fotos, posts, productos/servicios, FAQ, horarios, descripción, reviews y respuestas. Úsala SIEMPRE que el usuario pida "analiza la ficha GBP de X", "qué tiene en su GBP", "extrae datos de GBP", "compara fichas", o tras `local-pack-multi-city` para enriquecer cada negocio detectado. Va más allá del ranking: captura el contenido del GBP.
---

> 📚 **Itinerario YinyangSEO Academy · Clase 1** — Webs agénticas y SEO eficiente.
> Esta skill forma parte del repo de la Clase 1. Clona o descarga el repo entero y dáselo a tu agente como contexto antes de ejecutarla. El repo se actualiza durante el curso.

# GBP · Deep Profile Extractor

Mientras `gbp-grid-extractor` mide **dónde** rankea un negocio, esta skill captura **qué hay dentro** de su ficha. Es la materia prima para detectar patrones de qué Google premia en el Local Pack.

## Inputs

- **Place IDs** (recomendado) o lista de URLs/`@coordenadas` de Google Maps.
- O bien: dataset `consolidated.json` de [`local-pack-multi-city`](../local-pack-multi-city/SKILL.md).
- **Idioma de captura** · por defecto el del país (`es-ES`).
- **Profundidad de reviews** · top N reviews (default: 30 más recientes + 30 más antiguas + 30 con respuesta del owner).

## Proceso

1. **Resolver place_id** vía Google Places API si solo hay nombre + ciudad.
2. **Por cada negocio, capturar:**
   - **Identidad:** nombre, descripción, web, teléfono, dirección.
   - **Categoría primaria + secundarias** (clave para detectar patrones).
   - **Atributos** (ej. *Servicio 24h*, *Aceptan tarjeta*, *Accesible silla de ruedas*).
   - **Horarios** (incluyendo *special hours* si las hay).
   - **Productos / Servicios** definidos en la ficha.
   - **Fotos:** total, ratio interior/exterior/equipo, fecha de la última subida.
   - **Posts:** últimos 10, fecha, tipo (oferta, evento, novedad), longitud.
   - **Q&A / FAQ** del GBP.
   - **Reviews:** total, rating medio, distribución 1-5★, longitud media, % con respuesta del owner.
   - **Booking link / Reservation provider** si aplica.
3. **Inferir señales de mantenimiento:**
   - `last_post_age_days`
   - `last_photo_age_days`
   - `owner_response_rate_30d`
   - `review_velocity_30d` (reviews/mes)
4. **Guardar ficha completa** en `data/gbp-profiles/{place_id}.json`.

## Herramientas

- **Google Places API v1** (`places.googleapis.com/v1/places/{place_id}`) → preferida. Estable.
- **GBP scraping con Playwright/Patchright** → solo si la API no devuelve algún campo (posts, Q&A) y con conciencia del *limited view* desde feb 2026.
- **DataForSEO Business Data API** → alternativa con créditos.

## Salida

```
data/gbp-profiles/
├── ChIJxxxxxxxx-1.json      ← ficha completa de cada place_id
├── ChIJxxxxxxxx-2.json
└── _matrix.csv              ← matriz comparativa (categorías, atributos, señales)
```

`_matrix.csv` columnas mínimas:
`place_id, name, primary_category, secondary_categories, n_photos, last_post_age_days, total_reviews, avg_rating, owner_response_rate, has_services, has_qa, attributes_count`.

## Calidad / QA

- Si `total_reviews == 0` → posible limited view. Anotar y no incluir como "frío".
- Validar que la categoría primaria está en el listado oficial de Google.
- Avisar si > 40 % de los negocios tienen `last_post_age_days > 365` → es señal de que ese vertical no usa Posts.
- Coste: si > 100 negocios, avisar antes de lanzar (créditos Places API).

## Para qué se usa después

→ Junto con [`web-pattern-extractor`](../web-pattern-extractor/SKILL.md), es el input de [`local-seo-pattern-aggregator`](../local-seo-pattern-aggregator/SKILL.md), que detecta *"qué tiene en común el top 3"*.
