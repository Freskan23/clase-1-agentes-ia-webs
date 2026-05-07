# Diccionario de Conceptos — Agentes IA y Desarrollo Web

**Para clase 1 del itinerario YinyangSEO**
Glosario para SEOs y marketers que tocan código a ratos.
Explicaciones poco técnicas con ejemplos cotidianos.

---

## 1. La caja de herramientas (entornos donde corren los agentes)

**CLI** — *Command Line Interface*. La pantalla negra con texto donde escribes comandos en lugar de hacer clics. Es lo que se abre cuando ejecutas `cmd` en Windows o el "Terminal" en Mac. *Ejemplo: en Claude Code escribes `claude` y arrancas el agente desde ahí. No hay botones, escribes lo que quieres.*

**Terminal / Shell / Bash** — Lo mismo que CLI pero con tres nombres distintos según humor del que habla. "Terminal" es la ventana, "shell" es el programa que interpreta lo que escribes, "Bash" es el shell más común en Mac/Linux. Para audiencia SEO/marketer: trátalos como sinónimos.

**IDE** — *Integrated Development Environment*. El programa donde se escribe código con todas las comodidades: coloreado, autocompletado, panel de archivos, terminal integrado. Es a un programador lo que Photoshop a un diseñador. *Ejemplos: VS Code (el más usado), Cursor, Windsurf, Trae.*

**VS Code** — El IDE gratuito de Microsoft. Casi todos los IDEs modernos para IA (Cursor, Windsurf, Trae) son **forks** de VS Code, es decir, copias modificadas. Por eso comparten interfaz y atajos.

**Fork (de software)** — Coger el código abierto de un proyecto y crear tu propia versión modificada. Cursor es un fork de VS Code: misma base, distinto envoltorio. *Analogía SEO: como clonar una plantilla de WordPress y modificarla.*

**Repositorio (repo)** — La carpeta donde vive el código de un proyecto, con historial completo de cambios. Suele estar en GitHub. *Ejemplo: tu repo de vistoenmaps.com en GitHub es eso, un repositorio.*

**Git / GitHub** — Git es el sistema de control de versiones (la lógica del historial). GitHub es la web de Microsoft donde la gente sube sus repos para colaborar. *Analogía: Git es Word con "Control de cambios" puesto siempre; GitHub es Google Drive donde compartes esos documentos.*

**Branch (rama)** — Una copia paralela del código para experimentar sin romper el original. Cuando funciona, "fusionas" (merge) los cambios al original. *Ejemplo: estás en la rama `main`, creas la rama `nueva-home`, pruebas un rediseño, y si te gusta lo metes a `main`.*

**Commit** — Guardar un cambio con un mensaje describiéndolo. Es como hacer "save as" pero dejando una nota explicando qué cambiaste.

**Push / Pull** — Subir tus cambios al servidor (push) o bajar los cambios de otros (pull). *Ejemplo: terminas de trabajar, haces push a GitHub para que tu socio lo vea mañana.*

---

## 2. El vocabulario del agente IA

**LLM** — *Large Language Model*. El "cerebro" del agente: el modelo de IA que genera el texto/código. *Ejemplos: Claude Sonnet 4.6, GPT-5.4, Gemini 2.5 Pro. Todos son LLMs.*

**Agente vs Chat/Asistente** — Un chat (ChatGPT clásico) responde y se calla. Un **agente** además ejecuta acciones: lee archivos, abre el navegador, lanza comandos, escribe código en disco. *Ejemplo: ChatGPT te dice "tendrías que crear un archivo index.html con esto". Claude Code lo crea por ti.*

**Token** — La unidad mínima que el modelo cuenta. No es ni una palabra ni una letra, es un trozo intermedio. "Hola mundo" son ~3 tokens. Importa porque **te facturan por tokens**. *Regla práctica: 1.000 palabras ≈ 1.300 tokens.*

**Context window (ventana de contexto)** — La memoria a corto plazo del modelo: todo lo que es capaz de "ver" a la vez en una conversación. Si tiene 200K tokens de contexto, puede leer ~150.000 palabras de golpe (un libro entero). Cuando se llena, "olvida" lo más antiguo.

**Rate limit** — El tope de uso por ventana de tiempo. Claude Pro te da X tokens cada 5 horas. Si te lo gastas en hora y media, esperas hasta que la ventana se renueve. *Igual que el límite de búsquedas que te da Ahrefs por mes.*

**Prompt** — La instrucción que le das al modelo. Tu mensaje. Cuando alguien dice "prompt engineering" se refiere al arte de redactar buenas instrucciones.

**System prompt** — Las instrucciones invisibles que el sistema mete al inicio de cada conversación, definiendo cómo debe comportarse el agente. Tú no las ves pero están ahí.

**MCP** — *Model Context Protocol*. Un estándar abierto (creado por Anthropic, adoptado por todos) para enchufar herramientas externas al agente. Es el **USB-C de los agentes IA**: una vez que algo soporta MCP, funciona en Claude Code, en Cursor, en Codex, en Windsurf, sin reescribirlo. *Ejemplo: instalas el MCP de Chrome DevTools y de pronto Claude Code puede abrir Chrome, navegar y depurar webs. Es lo que permite que tu agente arranque navegadores.*

**Tool / Tool call** — Una herramienta concreta que el agente puede invocar (leer un archivo, hacer una búsqueda web, abrir una pestaña). Una tool call es cada vez que el agente "tira" de esa herramienta. *Ejemplo: durante una sesión de Claude Code, ves "calling read_file..." → eso es una tool call.*

**Skill** — Concepto de Anthropic: una carpeta con instrucciones especializadas que Claude lee antes de hacer cierto tipo de tarea. *Ejemplo: la skill "docx" le explica a Claude exactamente cómo crear documentos Word de calidad. Cuando le pides un Word, primero lee la skill, luego se pone a crearlo. Es como darle un manual al becario antes de mandarlo a hacer algo.*

**Subagent / sub-agente** — Un agente "hijo" que lanzas dentro de tu sesión para una tarea específica. Trabaja en paralelo, no consume tu ventana de contexto principal. *Ejemplo: "Lanza un subagente que investigue todos los precios de hoteles de Cerceda mientras tú escribes el código del frontend". Tú sigues, él trae resultados.*

**Background agent / Headless agent** — Agente que corre en segundo plano, sin que tú estés mirando. Le delegas una tarea y vuelve cuando ha terminado.

**Vibe coding** — Programar dejándose llevar, dictándole al agente lo que quieres en lenguaje natural sin entrar en el código. Lo acuñó Andrej Karpathy en 2025. *Ejemplo: "hazme una landing con un formulario que mande emails" y dejas que el agente vaya iterando hasta que te guste, sin leer una línea de código.*

**Plan Mode / Builder Mode / SOLO Mode** — Tres etiquetas para lo mismo con matices: el agente primero **piensa un plan**, te lo enseña, y luego ejecuta. Plan Mode (Claude Code, Windsurf) es más conservador: enseña el plan y espera tu OK. Builder Mode / SOLO Mode (Trae) es más agresivo: planifica y ejecuta de tirón.

**Autocompletado / Tab completion** — Mientras escribes, el editor te sugiere el siguiente trozo de código en gris. Pulsas Tab y lo aceptas. Es el feature que hizo famoso a Cursor.

---

## 3. Desarrollo web (lo justo para la clase)

**Frontend / Backend / Full-stack** — Frontend es lo que ve el usuario (HTML, CSS, JS). Backend es la cocina (servidor, base de datos, APIs). Full-stack es quien hace ambos. *Analogía: en una web local SEO, el frontend es la ficha bonita, el backend es el sistema que guarda las reseñas y las muestra.*

**Framework** — Un esqueleto de código preconstruido para no empezar de cero. *Ejemplos: React (de Facebook), Next.js (sobre React, lo que usas), Vue, Astro. Cuando alguien dice "está hecho en Next.js", se refiere al framework.*

**Stack** — La pila de tecnologías que usa un proyecto. *Ejemplo: "el stack de vistoenmaps es Next.js + Tailwind + Vercel".*

**Dev server (servidor de desarrollo)** — Un mini servidor que arrancas en tu propio ordenador para ver tu web mientras la editas, antes de publicarla. Suele correr en `localhost:3000`. *Cuando ejecutas `npm run dev` en Next.js, eso es el dev server.*

**Hot reload** — Cuando guardas un cambio en el código y la web se actualiza sola en el navegador sin tener que refrescar. Magia del dev server moderno.

**Preview / Vista previa** — La capacidad de ver el resultado antes de publicar. Trae SOLO y Windsurf lo tienen integrado dentro del propio agente; con Claude Code abres tú el navegador o usas un MCP.

**Deploy / Despliegue** — Subir tu web al mundo real. *Ejemplos de servicios: Vercel (el más popular para Next.js), Netlify, Cloudflare Pages.*

**DOM** — *Document Object Model*. La estructura de un HTML interpretada como un árbol de elementos. Cuando un agente "selecciona el botón", está navegando el DOM.

**DevTools** — Las herramientas de desarrollador que vienen integradas en Chrome (F12). Permiten inspeccionar HTML, ver errores, medir velocidad, etc. **Chrome DevTools MCP** es un puente para que tu agente IA use esas mismas herramientas en automático.

**Console (consola del navegador)** — La pestaña de DevTools donde aparecen errores y mensajes técnicos del JavaScript de la web. Cuando algo no funciona, lo primero que mira un dev (o un agente) es la consola.

**Headless browser** — Un navegador que corre **sin interfaz visual**, en segundo plano. Útil para que el agente haga pruebas sin abrir ventanas. *Playwright lanza Chrome en modo headless por defecto.*

**Playwright** — Herramienta de Microsoft para automatizar navegadores y hacer tests end-to-end. Es el estándar actual. Vía MCP, tu agente lo usa para "haz clic aquí, rellena este form, comprueba que aparece este texto".

**E2E testing** — *End-to-end testing*. Pruebas que simulan a un usuario real haciendo todo el recorrido (entra, busca, añade al carrito, paga). Lo opuesto a tests unitarios que solo prueban una función aislada.

**Scaffolding** — Cuando el agente te genera de golpe la estructura completa de un proyecto vacío pero funcionando: carpetas, configuración, dependencias instaladas. *El Builder Mode de Trae hace scaffolding cuando le dices "hazme una app de gestión de tareas".*

**Refactor** — Reescribir código existente para que esté mejor (más limpio, más rápido, más mantenible) sin cambiar lo que hace de cara al usuario. *Es donde brilla Claude Code: refactors grandes en monorepos.*

**Debug / Depurar** — Encontrar y arreglar errores. *Ejemplo: "el formulario no envía emails" → debug.*

**Lint / Linter** — Un corrector ortográfico para código. Te avisa de errores y de "cosas mal escritas" antes de que las ejecutes.

---

## 4. La caja registradora (precios y consumo)

**API** — *Application Programming Interface*. La "puerta de servicio" de un programa para que otros programas se conecten. Cuando un agente "usa la API de Anthropic", está hablando con Claude por debajo, sin la interfaz web. *Analogía: en lugar de pedirle a un camarero (la web), entras directo a la cocina y pides al cocinero.*

**API key** — La contraseña/llave que identifica quién está llamando a la API y a quién facturar. *Ejemplo: la `ANTHROPIC_API_KEY` que pegas en tu `.env` para que Claude Code conecte con la API.*

**BYOK** — *Bring Your Own Key*. "Trae tu propia clave". El agente es gratis pero tú pones tu API key y pagas el consumo directo a Anthropic/OpenAI/quien sea. *OpenCode funciona así por defecto.*

**Pay-as-you-go (PAYG)** — Pago por consumo, sin cuota fija. Pagas lo que gastas en tokens. Lo opuesto a una suscripción.

**Suscripción / Tier** — Cuota mensual fija con un cupo de uso incluido. *Ejemplo: Claude Pro $20/mes, Claude Max 5x $100, Max 20x $200.*

**Prompt caching (caché de prompts)** — Truco de optimización: si reenvías el mismo contexto (tu codebase) muchas veces, el sistema lo cachea y te lo cobra al 10% del precio normal. *Por eso una suscripción Max resulta muchísimo más barata que la API equivalente: el cache cuenta como uso normal.*

**Batch API** — Mandas un montón de tareas no urgentes y te las procesan en hasta 24 horas, al 50% del precio. Útil para cosas masivas no interactivas (ej. analizar 10.000 reseñas).

**Crédito** — Unidad abstracta de consumo. OpenAI Codex factura en "créditos" que se mapean a tokens. Cada plan te da un cupo mensual.

---

## 5. Otras palabras que vas a oír sí o sí

**Open source** — Código abierto, cualquiera puede leerlo, copiarlo y modificarlo. *Ejemplos: VS Code, OpenCode, React, Linux.*

**Vendor lock-in** — Quedarte atrapado en un proveedor porque cambiar es muy costoso. *Ejemplo: si construyes todo sobre la API de Anthropic, migrar a OpenAI implica reescribir cosas. OpenCode evita esto siendo agnóstico.*

**LSP** — *Language Server Protocol*. El sistema que avisa de errores y autocompletado en tu IDE en tiempo real (los subrayados rojos). No te hace falta entenderlo más allá de "es lo que hace que VS Code te diga 'esto está mal'".

**SDK** — *Software Development Kit*. Un paquete de código que te facilita conectar con un servicio. *Ejemplo: el SDK de Anthropic es lo que importas en Python para hablar con Claude desde tu propio script.*

**Sandbox** — Entorno aislado y seguro donde el agente puede ejecutar código sin riesgo de romper tu ordenador. *Claude Code corre los comandos peligrosos en sandbox por defecto.*

**Worktree (Git)** — Múltiples copias en paralelo del mismo repositorio para que varios agentes trabajen a la vez sin pisarse. *Lo usa Claude Code para Agent Teams.*

**npm / npx** — npm es el gestor de paquetes de JavaScript (instala dependencias). npx es su primo: ejecuta un paquete una sola vez sin instalarlo permanentemente. *Cuando ves `npx @playwright/mcp@latest`, le estás diciendo "ejecuta esto al vuelo".*

**Ollama / modelo local** — Correr un LLM en tu propio ordenador, sin enviar datos a la nube. Más privado y gratis pero requiere PC potente y la calidad es menor que un modelo frontera.

**Frontier model (modelo frontera)** — Los modelos más potentes disponibles en cada momento. *Hoy: Claude Opus 4.7, GPT-5.4, Gemini 3.x.* Lo opuesto a modelos pequeños/baratos como Haiku o GPT-mini.
