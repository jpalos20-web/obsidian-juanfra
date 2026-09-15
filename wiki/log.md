---
title: Log
tags:
  - log
---

# 📜 Log

Registro cronológico y append-only de cambios estructurales en la bóveda. No se reescribe el historial, solo se añaden entradas nuevas al final.

## 2026-09-15 — Reestructuración a esquema raw/wiki

Se reorganizó toda la bóveda siguiendo el esquema de tres capas descrito en [gist de Karpathy](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f): fuentes crudas inmutables en `raw/`, contenido curado en `wiki/`, y este `CLAUDE.md` como capa de esquema.

Cambios concretos:

- `transcripciones/` → `raw/transcripciones/` (37 conversaciones, sin tocar contenido).
- `00_Dashboard.md` → `raw/00_Dashboard-original.md` (archivado como referencia histórica, no se borró).
- `research/`, `resources/` (excepto la guía de prompting) e `ideas/`, `inbox/` → `wiki/sources/`.
- `resources/guia-prompting-claude.md` → `wiki/concepts/` (es una técnica reutilizable, no el resumen de una fuente puntual).
- `personas/` + `resources/perfil-juanfra.md` → `wiki/entities/personas/`.
- `proyectos/` → `wiki/entities/proyectos/`.
- `02_Areas/Tecnologia-Desarrollo/Claude-Code/` (subsistema sincronizado automáticamente) → `wiki/entities/proyectos/claude-code/`. **Si hay una tarea programada apuntando a la ruta antigua, hay que actualizarla.**
- Notas de área (`Gestion-Personal`, `Fotografia-Profesional`, `Tecnologia-Desarrollo`) → `wiki/entities/areas/`.
- `03_Recursos/Plantillas/Plantilla-Cliente.md` → `templates/plantilla-cliente.md` (ya era la carpeta de plantillas configurada en Obsidian).
- Carpetas PARA vacías eliminadas (`01_Proyectos/`, `04_Archivo/`, `02_Areas/`, `03_Recursos/`, `proyectos/`, `research/`, `resources/`, `personas/`, `ideas/`, `inbox/`) y `Garantias.md` (0 bytes, sin contenido).
- `daily-notes/` y `templates/` se mantienen porque están configuradas como tal en `.obsidian/`.
- `wiki/analyses/` queda vacío a propósito: se irá llenando con análisis comparativos a medida que crezca la bóveda.
- Se creó `wiki/index.md`, `wiki/overview.md`, `wiki/conventions.md` y se reescribió `CLAUDE.md` como capa de esquema.
