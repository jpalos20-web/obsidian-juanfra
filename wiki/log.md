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

## 2026-09-15 — Procesado el backlog de raw/

Se revisaron todos los `raw/transcripciones/` y se confirmó que las 36 conversaciones ya estaban enlazadas desde alguna nota de `wiki/`. El único pendiente real era `wiki/sources/consultas-sueltas-2026.md` (7 conversaciones cortas sin clasificar). Se repartieron en:

- `wiki/sources/`: [[limitaciones-tiktok]], [[reparar-zip-corrupto]], [[reconciliacion-gastos-notion]]
- `wiki/concepts/` (técnicas reutilizables): [[recuperar-app-bloqueada-gatekeeper-macos]], [[gestionar-consumo-claude-proyectos]], [[flujo-trabajo-fotografo-bodas]]

Cada nota nueva quedó enlazada desde su área correspondiente (`Fotografia-Profesional`, `Tecnologia-Desarrollo`, `Gestion-Personal`) y desde `wiki/index.md`. `consultas-sueltas-2026.md` se dejó como nota puente (no se borró, solo se vació su contenido a las notas de arriba) apuntando a las nuevas ubicaciones.

## 2026-09-15 — raw/clippings/ y 4 fuentes nuevas

Aparecieron 21 archivos `.md` sueltos directamente en `raw/` (formato "clippings", con metadata `source: claude.ai/chat/<uuid>`) — capturas parciales hechas con un web clipper de Obsidian, no exportación completa. Se movieron a `raw/clippings/` con un índice ([[Indice-Clippings]]) que mapea 17 de ellas a la conversación completa que ya tenían en `raw/transcripciones/`, y deja 4 como fuente nueva: [[auditoria-uso-hetzner]], [[configurar-obsidian-con-claude]], [[integracion-cerebro-digital-obsidian-github]] y [[exportar-conversaciones-a-obsidian]] (esta última documenta el origen real de `raw/transcripciones/` y confirma que no existe sincronización automática claude.ai → Obsidian, solo volcados puntuales o el web clipper).

Si ese web clipper sigue activo, conviene apuntarlo a `raw/clippings/` directamente para que no vuelva a dejar archivos sueltos en la raíz de `raw/`.

## 2026-09-15 — carpeta copilot/ del plugin Obsidian Copilot

Se instaló el plugin "Copilot" de Obsidian, que crea `copilot/` en la raíz del vault: `copilot/skills/` (configuración del plugin, infraestructura, se deja intacta) y `copilot/copilot-conversations/` (chats reales dentro de la bóveda). Se movieron las conversaciones a `raw/copilot-conversations/` y se procesó la única que llegó a completarse (el resto falló por límite de cuota de la API de Gemini): un listado de fotógrafos/videógrafos de boda de referencia en Cataluña, ahora en [[fotografos-videografos-boda-cataluna]] — primera entrada real de `wiki/analyses/`.

## 2026-09-15 — Copilot guarda ya directamente en raw/

Se cambió `defaultSaveFolder` en `.obsidian/plugins/copilot/data.json` de `copilot/copilot-conversations` a `raw/copilot-conversations` (backup del data.json original guardado como `data.json.bak-cerebro`). A partir de ahora cualquier conversación nueva con Copilot se guarda directamente en `raw/`, sin paso manual — queda cubierta en cualquier repaso futuro de `raw/`. El resto de `copilot/` (`skills/`, `copilot-custom-prompts/`, `projects/`, `memory/`) sigue siendo infraestructura del plugin y no se toca.

Si Obsidian estaba abierto al hacer este cambio, puede hacer falta recargar el plugin Copilot (o reiniciar Obsidian) para que recoja la nueva ruta.

## 2026-09-15 — dos archivos nuevos en raw/

- `raw/vera — CRM para fotógrafos de boda.md`: clipping web del dashboard de app.veracrm.es. Movido a `raw/clippings/`, resumido en [[vera-crm-snapshot-2026-09-15]] y enlazado desde [[vera-crm]].
- `raw/Documento sin título.md`: 0 bytes, sin contenido. Se deja donde está (no se borra sin que lo pidas) — probablemente una nota nueva de Obsidian creada sin querer o sin rellenar todavía.
