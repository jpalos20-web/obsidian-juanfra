---
title: Conventions
tags:
  - conventions
---

# 📐 Conventions

Reglas de uso de esta bóveda. Es la parte "de detalle" del esquema — [[../CLAUDE|CLAUDE.md]] explica la arquitectura general y enlaza aquí.

## Las tres capas

1. **`raw/`** — fuentes crudas e inmutables (transcripciones exportadas, PDFs, capturas, datos). Se lee, nunca se edita ni se resume in-place.
2. **`wiki/`** — todo lo generado y mantenido a partir de `raw/`:
   - `index.md` — catálogo de contenido por categoría.
   - `log.md` — registro cronológico append-only de cambios estructurales.
   - `overview.md` — síntesis de alto nivel.
   - `conventions.md` — este archivo.
   - `sources/` — resúmenes de una fuente concreta (una conversación, un documento).
   - `entities/` — páginas sobre personas, proyectos y áreas (`personas/`, `proyectos/`, `areas/`).
   - `concepts/` — metodologías o técnicas reutilizables, no atadas a una sola fuente.
   - `analyses/` — estudios comparativos o argumentos sintetizados a partir de varias fuentes.
3. **`CLAUDE.md`** (raíz) — capa de esquema: qué es cada carpeta y qué flujo de trabajo seguir al ingerir contenido nuevo.

## Cuándo va cada cosa dónde

- ¿Es una conversación/documento exportado tal cual? → `raw/`.
- ¿Es el resumen de una fuente puntual? → `wiki/sources/`.
- ¿Describe a una persona, un proyecto o un área de responsabilidad continua? → `wiki/entities/`.
- ¿Es una técnica o método reutilizable en varios contextos? → `wiki/concepts/`.
- ¿Compara o sintetiza varias fuentes/entidades entre sí? → `wiki/analyses/`.
- ¿No se sabe todavía? → déjalo en `wiki/sources/` con la etiqueta que ya traía (p. ej. `inbox`) y decide más tarde.

## Convenciones de Obsidian (heredadas, siguen aplicando)

- SIEMPRE usa `[[doble corchete]]` para enlaces internos entre notas.
- SIEMPRE usa tags con `#` (ej: `#proyecto`, `#idea`, `#research`).
- Usa la plantilla de `templates/` cuando crees una ficha de cliente nueva.
- Los nombres de archivo van en minúsculas con guiones: `mi-proyecto-nuevo.md` (las notas heredadas de las áreas/proyectos de Claude Code mantienen su capitalización original — no renombrar para no romper los `[[wikilinks]]` existentes).
- Las fechas siempre en formato `YYYY-MM-DD`.
- Cada nota nueva de `wiki/sources/` o `wiki/entities/` debería terminar con una sección "🔗 Relacionado" con enlaces a notas relevantes, y si viene de una transcripción, una sección "📎 Transcripciones completas" enlazando a `raw/transcripciones/`.

## Tags principales

- `#transcripcion` → contenido de `raw/`
- `#proyecto`, `#persona`, `#idea`, `#research`, `#claude-code` → tipos de nota en `wiki/entities/` y `wiki/sources/`
- `#estado/activo`, `#estado/pausado`, `#estado/completado` → estado de proyectos
- `#prioridad/alta`, `#prioridad/media`, `#prioridad/baja` → urgencia
- `#tema/[categoria]` → clasificación temática libre

## Reglas de comportamiento para la IA

- Al ingerir una conversación nueva: exportarla íntegra a `raw/transcripciones/`, luego crear o actualizar la nota correspondiente en `wiki/sources/` o `wiki/entities/`, enlazando en ambas direcciones.
- Actualizar `wiki/index.md` cuando se añade o reclasifica contenido, y añadir una línea a `wiki/log.md` cuando el cambio es estructural (mover carpetas, crear una capa nueva, etc.) — no para cada nota individual.
- Si una nota pertenece a un proyecto, enlázala en la sección "🔗 Relacionado" del proyecto.
- Si aparece una persona relevante, crea o enlaza su nota en `wiki/entities/personas/`.
- Si algo entra sin contexto claro, déjalo en `wiki/sources/` etiquetado y pendiente de decidir.
- Prioriza claridad, conexión entre notas y utilidad futura por encima del exceso de detalle.
- Mantén `raw/` intacto: si hace falta corregir algo de una transcripción, corrígelo en la nota de `wiki/` que la resume, no en la fuente.

## 🔗 Relacionado

- [[index]]
- [[overview]]
- [[log]]
