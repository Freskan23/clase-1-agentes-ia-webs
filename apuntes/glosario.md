# Glosario rápido

> Definiciones cortas. Para el detalle ampliado, ver [`01-diccionario/diccionario-conceptos.md`](../01-diccionario/diccionario-conceptos.md).

---

## Caja de herramientas

| Término | Definición corta |
|---------|------------------|
| **CLI** | Línea de comandos. La interfaz “sin botones” donde escribes instrucciones. |
| **Terminal** | Ventana donde corres comandos. La puerta a la CLI. |
| **IDE** | Editor de código integrado (ej. VS Code, Cursor). Texto + tooling + debug en un sitio. |
| **Repo** | Carpeta versionada. Código + historial + instrucciones. |
| **GitHub** | Hospedaje de repos en la nube. Plataforma + colaboración. |
| **Fork** | Copia tuya de un repo ajeno para experimentar. |
| **Branch** | Rama paralela del repo para experimentar sin romper la principal. |
| **Commit** | “Foto” de los cambios. Sirve para volver atrás. |
| **Push / Pull** | Subir / bajar cambios entre tu carpeta local y GitHub. |

## Vocabulario del agente

| Término | Definición corta |
|---------|------------------|
| **LLM** | Modelo de lenguaje. El “cerebro” que genera texto. |
| **Agente** | LLM + herramientas + bucle de trabajo. Hace, no solo responde. |
| **Token** | Unidad mínima de texto (~¾ palabra). Se cobra por entrada y por salida. |
| **Contexto** | Lo que el agente “tiene en cabeza” en cada momento (limitado). |
| **Prompt** | Una instrucción puntual. |
| **Skill** | Procedimiento empaquetado: objetivo + inputs + pasos + herramientas + salida + QA. |
| **MCP** | Conector estándar (USB-C) entre el agente y herramientas externas. |
| **Tool call** | Llamada concreta del agente a una herramienta. |
| **Subagent** | Agente “hijo” que trabaja en una sub-tarea con su propio contexto. |

## Desarrollo web

| Término | Definición corta |
|---------|------------------|
| **Frontend** | Lo que ve el usuario. HTML, CSS, JS. |
| **Backend** | Lo que pasa en el servidor. APIs, base de datos. |
| **Framework** | Esqueleto que da estructura (Next.js, Astro, Remix…). |
| **Stack** | Conjunto de tecnologías que usas. |
| **Dev server** | Servidor local para ver tu web mientras la editas. |
| **Preview** | Pantalla que muestra cambios en tiempo real. |
| **Deploy** | Publicar la web (Vercel, Netlify, Cloudflare Pages…). |
| **DOM** | Árbol de elementos de una página. Lo que manipulas con JS. |
| **DevTools** | Herramientas del navegador para inspeccionar / debug. |
| **Playwright** | Librería para navegar como humano de forma automática. |

## Costes y consumo

| Término | Definición corta |
|---------|------------------|
| **API** | Forma oficial de pedir datos a un servicio. |
| **API key** | Credencial para usar una API. |
| **BYOK** | *Bring Your Own Key*: tú pones la key (y pagas el consumo). |
| **Pay-as-you-go** | Pagas por uso real (tokens / requests). |
| **Suscripción** | Cuota fija mensual con límites. |
| **Prompt caching** | Reutilizar contexto cacheado para abaratar la entrada. |
| **Batch API** | Peticiones agrupadas con descuento. |
| **Crédito** | Saldo prepago para consumir en la plataforma. |

## Conceptos extra

| Término | Definición corta |
|---------|------------------|
| **Open source** | Código abierto, audita y modifica quien quiera. |
| **Vendor lock-in** | Atrapado en un proveedor por dependencias. |
| **SDK** | Kit de herramientas / librería para integrar un servicio. |
| **Sandbox** | Entorno aislado donde algo se ejecuta sin tocar el resto. |
| **Worktree** | Copia de trabajo paralela del repo (varias ramas a la vez). |
| **npm / npx** | Gestor de paquetes JS / ejecutor de paquetes sin instalar. |
| **Modelo local** | LLM corriendo en tu máquina (Ollama, llama.cpp…). |
