# Cómo publicarlo en GitHub

> El repo ya está inicializado con `git init`, todos los archivos versionados y un primer commit.
> Solo falta crear el repo en GitHub y hacer `push`.

---

## Opción A · GitHub web + 3 comandos (recomendado)

### 1 · Crea el repo vacío en GitHub

1. Entra en <https://github.com/new>.
2. **Repository name:** `clase-1-agentes-ia-webs` (o el que prefieras).
3. Description (opcional): *Material maestro de la Clase 1 del itinerario YinyangSEO de Agentes IA.*
4. Public o Private (a tu gusto).
5. **❗ NO marques** “Initialize with README / .gitignore / LICENSE” (ya los tenemos).
6. Click **Create repository**.

GitHub te mostrará una URL del tipo `https://github.com/<tu-usuario>/clase-1-agentes-ia-webs.git`.

### 2 · Conecta y empuja

Abre PowerShell o Git Bash en la carpeta del repo:

```bash
cd "C:\Users\panoj\Documents\Clientes\YYS\itinerario agentes\clase 1\repo-github"

git remote add origin https://github.com/<tu-usuario>/clase-1-agentes-ia-webs.git
git push -u origin main
```

> Si te pide credenciales: usa tu usuario de GitHub y un **Personal Access Token** (Settings → Developer settings → Personal access tokens → Fine-grained, scope: repo).

### 3 · ¡Listo!

Abre `https://github.com/<tu-usuario>/clase-1-agentes-ia-webs` y verás todo navegable, con el README como portada.

---

## Opción B · GitHub CLI (`gh`)

Si tienes [GitHub CLI](https://cli.github.com/) instalado y autenticado (`gh auth login`):

```bash
cd "C:\Users\panoj\Documents\Clientes\YYS\itinerario agentes\clase 1\repo-github"

gh repo create clase-1-agentes-ia-webs --public --source=. --remote=origin --push --description "Material maestro · Clase 1 · Agentes IA para webs hiperoptimizadas (YinyangSEO)"
```

Un solo comando: crea, conecta y publica.

---

## Opción C · GitHub Desktop

1. Abre [GitHub Desktop](https://desktop.github.com/).
2. **File → Add Local Repository** → selecciona la carpeta `repo-github`.
3. **Publish repository** → elige nombre y visibilidad.
4. Listo.

---

## Antes de publicar (opcional pero recomendado)

### Reemplazar placeholders de URLs internas

En [`recursos/enlaces.md`](recursos/enlaces.md) hay 5 placeholders del tipo `<URL...>` para repos / webs YYS. Reemplázalos por las URLs reales:

```bash
# Git Bash en Windows
cd "C:\Users\panoj\Documents\Clientes\YYS\itinerario agentes\clase 1\repo-github"
# edita recursos/enlaces.md a mano o con sed
git add recursos/enlaces.md
git commit -m "docs: añadir URLs internas YYS / TickHat"
```

### Decidir visibilidad

- **Public:** ideal si quieres que cualquier alumno entre con un link.
- **Private:** si el material es solo para alumnos del itinerario; luego añades a los alumnos como colaboradores (Settings → Collaborators).

### Si vas a aceptar contribuciones

Considera añadir más adelante:

- `CONTRIBUTING.md` (cómo proponer mejoras).
- *Issue templates* para erratas o sugerencias.
- GitHub Actions para validar enlaces rotos.

---

## Estructura final del repo

```
repo-github/
├── README.md                              ← portada
├── LICENSE                                ← CC BY-SA 4.0
├── .gitignore
├── HOW-TO-PUBLISH.md                      ← este archivo (puedes borrarlo después)
│
├── 00-comparativa-agentes/
│   ├── comparativa-agentes-ia.md
│   └── comparativa.png
│
├── 01-diccionario/
│   ├── diccionario-conceptos.md
│   └── diccionario-parte-1..5.png
│
├── 02-investigacion-competidores/
│   ├── investigacion-skills-repos-mcps.md
│   ├── stack-clase-5-niveles.png
│   └── stack-clase-5-niveles.svg
│
├── 03-skills/
│   ├── competitor-local-seo-audit/SKILL.md
│   ├── gbp-grid-extractor/SKILL.md
│   └── serp-pattern-detector/SKILL.md
│
├── apuntes/
│   ├── apuntes-clase.md
│   ├── glosario.md
│   ├── ejercicio.md
│   ├── checklist.md
│   └── notas-instructor.md
│
├── presentacion/
│   └── clase_1_agentes_ia_webs_hiperoptimizadas_v2_con_notas.pptx
│
└── recursos/
    └── enlaces.md
```

24 archivos versionados · ~40 MB.
