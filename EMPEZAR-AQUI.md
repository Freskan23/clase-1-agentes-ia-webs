# 🚀 Empezar aquí · Guía para alumnos

> 📚 **YinyangSEO Academy · Clase 1 · Webs agénticas y SEO eficiente**

Este repo es **el material del curso**. No tienes que hacer nada técnico complicado — solo descargarlo y dárselo a tu agente como contexto. Esta guía te lleva paso a paso.

---

## Paso 1 · Descarga el repo

Tienes dos formas:

### 🟢 Opción fácil · Descargar ZIP (sin git)

1. Abre <https://github.com/Freskan23/clase-1-agentes-ia-webs>
2. Botón verde **`<> Code`** → **Download ZIP**.
3. Descomprime el ZIP en una carpeta donde te acuerdes (ej. `Documentos/yyseo-academy/`).
4. La carpeta resultante se llamará `clase-1-agentes-ia-webs-main`. Renómbrala si quieres.

### 🟡 Opción para los que tienen git instalado

```bash
git clone https://github.com/Freskan23/clase-1-agentes-ia-webs.git
cd clase-1-agentes-ia-webs
```

> Ventaja: cuando subamos contenido nuevo, basta con `git pull` para actualizar.

---

## Paso 2 · Abre la carpeta con tu agente

El objetivo es que tu agente pueda **leer todo el contenido del repo** mientras te ayuda. La forma cambia según el agente:

### Trae SOLO / Windsurf / Cursor / VS Code

`File → Open Folder` → selecciona la carpeta del repo.

Una vez abierta, tu agente tiene acceso al README, las skills, los apuntes, la presentación, las imágenes y el roadmap.

### Claude Code (terminal)

```bash
cd "ruta/a/clase-1-agentes-ia-webs"
claude
```

### ChatGPT / Gemini / otros (sin acceso a archivos)

Si tu agente no puede abrir carpetas, puedes:

1. Subir los archivos `.md` clave manualmente al chat (README, ROADMAP, alguna SKILL).
2. O usar [Jina Reader](https://r.jina.ai/) para convertir archivos del repo a texto plano y pegárselos.

---

## Paso 3 · Primer prompt al agente

Una vez tienes el repo abierto en tu agente, **pega este prompt** para que se "calibre":

```
Tienes acceso al repositorio "Clase 1 · Agentes IA para SEO y webs hiperoptimizadas"
del itinerario YinyangSEO Academy.

Antes de empezar:

1. Lee README.md y ROADMAP.md.
2. Mira la lista de skills disponibles en 03-skills/ y dime cuáles están MADURAS y
   cuáles son STUB.
3. Resúmeme en 5 puntos qué cubre la Clase 1 y qué viene después.
4. No ejecutes ninguna skill todavía. Solo prepárate.

Cuando termines, dime: "listo, ¿qué hacemos primero?".
```

Si el agente te responde correctamente, **vas bien**.

---

## Paso 4 · Qué pedirle (ejemplos por fase)

A medida que avances con el itinerario, estos son los prompts típicos:

### 🔍 Investigación (Fase 1)

```
Lee 03-skills/local-pack-multi-city/SKILL.md y prepárate para ejecutarla.

Inputs:
- Keyword: "cerrajero 24h"
- Ciudades: Sabadell, Terrassa, Barcelona, Madrid Centro, Valencia
- Top: 3 del Local Pack + 10 orgánico

Antes de lanzar: dime qué herramientas vas a necesitar y cuánto puede costar
(en tokens y créditos de SerpAPI). Espera mi confirmación.
```

### 📊 Análisis (Fase 2)

```
Con el output de local-pack-multi-city, ejecuta gbp-deep-profile y
web-pattern-extractor sobre los negocios únicos detectados. Lee las dos
SKILL.md antes.
```

### 💡 Patrones (Fase 3 · la pieza clave)

```
Ejecuta local-seo-pattern-aggregator con los datos de las fases 1 y 2.
Quiero el archivo hypotheses.md con las hipótesis HIGH·easy priorizadas
para usarlas como input de web-blueprint-generator.
```

### 🏗️ Generación de la web (Fases 4-5-6)

```
Lee web-blueprint-generator/SKILL.md y, a partir de las hipótesis HIGH,
genera el blueprint para nuestro cliente [NEGOCIO] que cubre los servicios
[X, Y, Z] en los barrios [A, B, C, D].

Cuando lo tengas, ejecuta landing-generator-servicio-barrio en modo dry-run
y muéstrame qué páginas se generarían antes de crear archivos.
```

---

## Paso 5 · Mantente al día

El repo se irá actualizando con:

- Skills más maduras (las STUB pasarán a MADURAS).
- Outputs reales de ejemplo.
- Starters Astro listos para clonar.
- Casos prácticos en `data/`.

**Cómo actualizar:**

- Si clonaste con `git clone`: ejecuta `git pull` dentro de la carpeta cuando se anuncie nuevo material.
- Si descargaste el ZIP: vuelve al link de GitHub y descárgalo de nuevo.

---

## Si te bloqueas

1. **Vuelve al [README.md](README.md)** y mira el índice.
2. **[ROADMAP.md](ROADMAP.md)** te dice en qué fase del itinerario estás.
3. **[apuntes/glosario.md](apuntes/glosario.md)** explica cualquier término raro.
4. Si una skill dice 🟡 STUB y la necesitas, **pídele a tu agente que la implemente** usando la propia SKILL.md como especificación. Para eso están escritas.
5. Si nada funciona, abre un *issue* en GitHub o coméntalo en clase.

---

## Lo que NO necesitas (todavía)

- ✗ Saber programar.
- ✗ Tener un servidor.
- ✗ Pagar herramientas caras (puedes hacer Fase 1-3 con tier gratuito de varios servicios).
- ✗ Instalar Playwright local (hay alternativas cloud — ver `recursos/enlaces.md`).

---

## Lo que SÍ recomendamos tener

- ✅ Un agente con preview/navegador integrado (Trae SOLO o Cursor son los más amigables).
- ✅ Una API key de **Google Places** (datos GBP estables).
- ✅ Una API key de **SerpAPI** o **DataForSEO** (SERPs estructuradas).
- ✅ Cuenta gratuita en **Vercel** o **Cloudflare Pages** (para deploy cuando llegue el momento).

Todo en [`recursos/enlaces.md`](recursos/enlaces.md).

---

¡Bienvenido al itinerario! 🎓
