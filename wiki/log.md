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

## 2026-09-15 — raw/gemini/ (historial general de Gemini)

Apareció `raw/consultas genrales gemini.md`, un volcado de 1.6 MB / ~15.200 líneas de un historial de Gemini sin separar en chats — mucho más grande y heterogéneo que cualquier fuente anterior. Se movió a `raw/gemini/consultas-generales-gemini.md`. Por su tamaño no se resumió tema por tema; se dejó una nota puente ([[consultas-generales-gemini-pendiente]]) señalando 3 bloques que sí parecen valer la pena procesar (comercialización de Vera CRM, comparativa de precios de álbumes, dominio/hosting de juanfrapalos.com) y quedando el resto pendiente de una pasada dedicada.

## 2026-09-15 — raw/gemini/ separado por temas

Se dividió `raw/gemini/consultas-generales-gemini.md` (1.6 MB, ~15.200 líneas) en 9 archivos por tema dentro de `raw/gemini/por-tema/`, mediante un proceso automático: detección heurística de ~1.970 posibles arranques de pregunta/respuesta + clasificación por palabras clave contra 8 categorías (`vera-crm`, `fotografia-boda`, `nexus-media-lab`, `photo-tooling`, `finanzas-personal`, `web-hosting-dominio`, `tech-general`, `personal-varios`) más un catch-all `sin-clasificar` para no perder nada que el clasificador no reconociera con confianza. El archivo original se conserva intacto en `raw/` — esto es una vista derivada adicional, no un reemplazo.

Primera pasada dejó `vera-crm.md` con solo 3 fragmentos — la discusión real sobre comercializar Vera como producto (líneas ~1412-1614) se había repartido en otras categorías por usar frases genéricas ("mi CRM") en vez de "Vera CRM" literal. Se corrigió con una segunda pasada de palabras clave más específicas.

Nota puente creada: [[gemini-consultas-por-tema]] (sustituye a [[consultas-generales-gemini-pendiente]], que queda como redirección). Enlazado desde [[vera-crm]]. Pendiente: revisión manual de `sin-clasificar.md` (1.240 fragmentos, el más grande) por si contiene algo de valor mal etiquetado.

## 2026-09-15 — repaso: 3 archivos nuevos en raw/

- `Sin título.md` (raíz de la bóveda, nota vacía de Obsidian que se rellenó con contenido real): tres ideas de vídeo de boda. Movida a `raw/clippings/Tres ideas para videos de boda.md` y resumida en [[ideas-videos-boda]], enlazada desde [[dossier-video-bodas]].
- `raw/gemini/consultas vera.md`: conversación con Gemini sobre cómo implementar tracking de apertura de emails/lectura de PDFs en Vera sin riesgo legal (RGPD/LSSI-CE). Renombrada a `raw/gemini/consultas-vera-tracking-legal.md` y resumida en [[vera-tracking-emails-pdf-legal]], enlazada desde [[vera-crm]].
- `raw/copilot-conversations/Fotógrafos_de_boda_en_Cataluña@20260915_175124.md`: nueva conversación de Copilot, esta vez completada sin fallos de cuota — mismo resultado (10 fotógrafos + 10 videógrafos) que ya estaba en [[fotografos-videografos-boda-cataluna]], así que solo se añadió una nota confirmando que el listado se repite igual en una segunda pasada.

También se detectó que una conversación de Copilot abierta antes del cambio de `defaultSaveFolder` siguió escribiendo en la ruta antigua (`copilot/copilot-conversations/`) con una pregunta adicional sin respuesta ("consejos de música para un vídeo de drift"); se fusionó con su copia ya movida en `raw/copilot-conversations/` y se eliminó la carpeta antigua, ahora vacía. Conclusión práctica: el cambio de carpeta de guardado solo afecta a conversaciones *nuevas* — una que ya estaba abierta puede seguir escribiendo en la ruta vieja hasta que se cierre/reinicie.
