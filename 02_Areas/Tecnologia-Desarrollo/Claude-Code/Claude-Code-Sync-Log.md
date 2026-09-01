---
title: Claude Code — registro de sincronización
tags:
  - claude-code
  - sync-state
---

# 🔄 Registro de sincronización

Nota de estado interna, usada por la tarea programada para saber qué sesiones ya están volcadas al vault y no repetir trabajo. No editar el bloque de abajo a mano salvo para forzar un re-proceso (borrar la línea de la sesión correspondiente).

**Última sincronización completa:** 2026-09-01

## Sesiones procesadas

| session_id | proyecto | nota destino | última actividad procesada |
|---|---|---|---|
| local_d8554fac-e341-46b4-b275-e91eaade33ec | BOT | [[BOT]] | 2026-08-14T10:05:01.680Z |
| local_ce7f4d0f-6b27-4d75-ad6b-2cb5b3c902e5 | BOT | [[BOT]] | 2026-08-13T14:51:25.964Z |
| local_72cf609f-6792-4c02-8cd7-a5dcb00a0ff4 | VERA | [[VERA]] | 2026-08-12T15:21:59.810Z |
| local_109f8f76-6011-45ab-8264-c7dd5b93b7ff | BOT | [[BOT]] | 2026-07-15T09:16:50.166Z |
| local_108f1d56-2239-413b-9466-fd955a4b9b6c | nexusmedialab | [[Nexusmedialab]] | 2026-07-01T18:04:35.244Z |
| local_2d355dd1-d6fc-418d-b6ef-ce957e9c48f1 | Downloads/files | [[Downloads-Files]] | 2026-06-28T20:24:38.360Z |
| local_42011ec9-ca55-4282-9e4d-9bbaca5e23e1 | Downloads/files | [[Downloads-Files]] | 2026-06-24T17:58:45.126Z |
| local_bed3df96-7f66-4b0d-9b16-fd599f2b1b6b | DUPLICITY | [[DUPLICITY]] | 2026-06-16T11:09:55.818Z |
| local_0ba6320b-665d-4958-b9f6-3920e6e02aa6 | VERA | [[VERA]] | 2026-06-11T16:08:27.971Z |
| local_4ba88563-6f78-4cc1-9565-d6af81455530 | Downloads/files | [[Downloads-Files]] | 2026-06-10T15:40:42.685Z |
| local_ffe41e66-7577-42c1-8f80-c0ec4e7ef119 | VERA | [[VERA]] | 2026-06-01T18:06:58.055Z |
| local_7c9d4bb5-b3b5-4a76-95e5-1011256bdcbc | VERA | [[VERA]] | 2026-05-30T08:47:57.898Z |

## Cómo funciona la sincronización periódica

1. Llamar a `mcp__ccd_session_mgmt__list_sessions` (incluyendo archivadas).
2. Comparar `lastActivityAt` de cada sesión contra la tabla de arriba.
3. Para cada sesión nueva o con `lastActivityAt` más reciente que la registrada: leer su transcript con `mcp__ccd_session_mgmt__list_events` y generar/actualizar su resumen en la nota de proyecto correspondiente (crear la nota si el `cwd` es nuevo).
4. Añadir o actualizar la fila en la tabla de arriba y la fecha de "Última sincronización completa".
5. Si aparece un `cwd` nuevo sin nota de proyecto, crear una nota siguiendo el mismo formato que [[BOT]] / [[VERA]] y enlazarla desde [[Claude-Code]].
