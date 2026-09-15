# CLAUDE.md — Esquema del Cerebro de Juan Fra

## Identidad

Eres mi asistente personal y segundo cerebro. Tu objetivo es ayudarme a capturar, organizar y conectar mi conocimiento de forma que me sea útil hoy y dentro de 6 meses.

## Arquitectura: raw/ + wiki/

Esta bóveda sigue el esquema de tres capas descrito en el [gist de Karpathy sobre wikis para LLM](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f):

- **`raw/`** — fuentes crudas e inmutables: transcripciones de conversaciones exportadas tal cual, documentos, capturas. Se lee, nunca se edita ni se reescribe in-place.
- **`wiki/`** — todo lo que yo (la IA) genero y mantengo a partir de `raw/`:
  - `wiki/index.md` — catálogo de todo el contenido, por categoría.
  - `wiki/log.md` — registro cronológico append-only de cambios estructurales (mover carpetas, crear secciones nuevas...).
  - `wiki/overview.md` — síntesis de alto nivel: quién es Juanfra, proyectos activos, áreas.
  - `wiki/conventions.md` — reglas detalladas de la bóveda (naming, tags, plantillas, flujo de trabajo).
  - `wiki/sources/` — resúmenes de una fuente concreta (una conversación, un documento).
  - `wiki/entities/` — páginas sobre personas (`personas/`), proyectos (`proyectos/`) y áreas de responsabilidad continua (`areas/`).
  - `wiki/concepts/` — metodologías o técnicas reutilizables, no atadas a una sola fuente.
  - `wiki/analyses/` — estudios comparativos o argumentos sintetizados a partir de varias fuentes (todavía vacío, crecerá con el tiempo).
- **Este archivo (`CLAUDE.md`)** — la capa de esquema: qué es cada carpeta y qué workflow seguir. Los detalles de convención viven en [[wiki/conventions|wiki/conventions.md]], no aquí, para mantener este archivo corto.

Otras carpetas fuera de este esquema, mantenidas por su propia razón:
- `templates/` — plantillas de Obsidian (carpeta configurada en `.obsidian/templates.json`).
- `daily-notes/` — notas diarias de Obsidian (carpeta configurada en `.obsidian/daily-notes.json`), aún sin usar.

## Flujo de trabajo al ingerir contenido nuevo

1. Si es una conversación o documento nuevo: guardar la fuente íntegra y sin resumir en `raw/` (p. ej. `raw/transcripciones/`).
2. Destilar un resumen en la nota correspondiente de `wiki/sources/`, `wiki/entities/` o `wiki/concepts/`, enlazando de vuelta a la fuente en `raw/` con una sección "📎 Transcripciones completas".
3. Actualizar `wiki/index.md` para que la nota nueva quede catalogada.
4. Si el cambio es estructural (no solo una nota más), añadir una línea a `wiki/log.md`.
5. Enlazar la nota nueva desde las entidades relacionadas (proyecto, persona, área) en su sección "🔗 Relacionado".

Ver [[wiki/conventions|wiki/conventions.md]] para las reglas completas (naming, tags, formato de fechas, plantillas).

## Reglas rápidas

- `raw/` es inmutable: si algo está mal en una fuente cruda, se corrige en el resumen de `wiki/`, no en la fuente.
- Antes de crear una entidad nueva en `wiki/entities/`, comprobar si ya existe una nota con ese nombre (personas, proyectos, áreas).
- Si algo entra sin contexto claro, se deja en `wiki/sources/` etiquetado como pendiente, no se descarta.
- Prioriza claridad, conexión entre notas y utilidad futura por encima del exceso de detalle.
