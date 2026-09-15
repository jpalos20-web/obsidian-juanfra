---
title: DUPLICITY
tags:
  - claude-code
  - proyecto
cwd: /Users/alba/DUPLICITY
aliases:
  - Organizador de Fotos y Vídeos
---

# 🗂️ DUPLICITY

Carpeta local `/Users/alba/DUPLICITY`. App de escritorio "Organizador de Fotos y Vídeos" (organización/deduplicación de archivos e importación desde iPhone).

## Historial de sesiones (Claude Code)

## Review request
*(fecha: 2026-06-16 · proyecto: DUPLICITY)*

**Objetivo:** Continuar el desarrollo con una larga serie de correcciones de bugs, nuevas funcionalidades y un rediseño visual siguiendo handoffs de diseño.

**Qué se hizo:**
- Corregido crash grave (SIGSEGV) en detección del iPhone: `ImageCaptureCore` debía ejecutarse en el hilo principal vía `QTimer`, no en `QThread`; documentado en `CLAUDE.md`.
- Validado end-to-end con iPhone real: detección de 2458 archivos y descarga de 2455, con progreso en vivo y log de errores por archivo.
- Empaquetada como `.app` con icono propio, firma ad-hoc y script `reconstruir_app.command`; creados `DESARROLLO.md` y `CHANGELOG.md`.
- Añadido borrado manual de archivos ya importados en el iPhone (excepción deliberada a la regla de "solo lectura" del proyecto).
- Cambiada la regla de clasificación por fecha: EXIF primero, mtime como fallback marcado "incierto" (antes todo iba a `Sin_Fecha`).
- Añadidos botones "Detener" (cancelación cooperativa) para analizar/aplicar y para detectar/descargar/ordenar del iPhone.
- Corregido que la `.app` empaquetada no detectaba el iPhone (Qt no bombeaba el run loop de ImageCaptureCore) y que siempre aparecían "107 archivos nuevos" (emparejamiento por fecha demasiado estricto).
- Añadidas miniaturas y panel de vista previa de archivos del iPhone.
- Implementado rediseño visual de "Organizar y deduplicar" (hero, banda de características, tarjetas de modo, tabla).
- Integrado `duplicados_perceptual.py` (pHash) en la GUI, validado con fotos reales (124 grupos en 532 fotos).
- Implementado `organizar_completo.py` (`FullOrganizer`): unifica duplicados exactos y casi-duplicados en una sola acción "Analizar".
- Arreglado que el fondo verde del diseño salía gris en la app real (degradado no se propagaba por el widget central transparente).
- Sesión terminada justo al empezar a corregir "picos" en las esquinas redondeadas (límite de sesión alcanzado).

**Decisiones clave:**
- Borrado en el iPhone: solo manual, restringido a archivos ya verificados como importados — excepción consciente a la regla de "solo lectura", documentada.
- Filosofía general: mover, nunca borrar (salvo esa excepción puntual y controlada).
- Cambio deliberado de la regla de fechas (EXIF primero, mtime fallback) manteniendo transparencia con la marca "incierta".

**Pendiente / próximos pasos:**
- Terminar de corregir los "picos" en las esquinas redondeadas (QSS) — a medias.
- Validar el borrado real de archivos contra el iPhone (nunca probado con dispositivo).
- Validar detección de casi-duplicados en vídeos reales (código escrito, sin validar).
- Rediseño pendiente de la pantalla "Importar desde iPhone".

## Enlaces

- [[Claude-Code]] — índice de todas las sesiones de Claude Code
- [[Tecnologia-Desarrollo]]
