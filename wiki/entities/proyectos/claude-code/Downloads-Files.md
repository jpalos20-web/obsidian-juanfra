---
title: Downloads-files (Gestor de Proyectos / RAWPress)
tags:
  - claude-code
  - proyecto
cwd: /Users/alba/Downloads/files
aliases:
  - RAWPress
  - Gestor de Proyectos
---

# 📦 Downloads/files

Carpeta local `/Users/alba/Downloads/files`. Contiene al menos dos apps de escritorio distintas: **Gestor de Proyectos** (gestión de bodas/proyectos) y **RAWPress** (compresión de RAWs), además de trabajo puntual sobre Vera CRM.

## Historial de sesiones (Claude Code)

## Move CLAUDE.md and PROGRESO.md to repo root
*(fecha: 2026-06-10 · proyecto: Downloads/files)*

> [!note] Título no coincide con el contenido
> Pese al título de la sesión, la transcripción trata sobre completar el flujo de invite-link de Vera y construir un "Cuestionario previo" nativo, más un bug de PDF. Se deja el título original para poder localizar la sesión.

**Objetivo:** Completar el flujo de invite-link, construir de cero un "Cuestionario previo" nativo en Vera (reglas estrictas de no romper deploy/datos existentes), y corregir un bug de PDF.

**Qué se hizo:**
- Verificados y commiteados los dos flujos de invite-link (registro nuevo y aplicación silenciosa en login).
- Implementada la feature "Cuestionario previo" completa y aditiva: migración SQLite idempotente, backend en `server/routes/cuestionario.js` (rutas públicas con rate-limit + comprobación de propiedad real), frontend con editor, página pública `/q/:token` y descarga de PDF vía html2pdf.js.
- Backup verificado antes de desplegar; verificación post-deploy completa (conteos de filas, webhook con firma buena/mala, login, ruta pública sin exponer campos sensibles). Commit `352b0f8`.
- Bug de PDF: html2canvas fallaba con "unsupported color function oklch" porque leía el CSS computado del `<body>` principal (tokens OKLCH de Vera) aunque el subárbol del PDF ya era hex. Solución final: ejecutar html2pdf.js **dentro** de un iframe aislado. Commit `5b38308`.

**Decisiones clave:**
- Reutilizar verbatim el modelo de datos y plantilla semilla del reference del usuario.
- Aislar completamente el subárbol del PDF (hex inline + iframe) sin tocar los design tokens globales.
- Excluir del commit cambios previos sin relación (mailer.js/portal.js/sign.js).

**Pendiente / próximos pasos:**
- Repo con trabajo previo sin commitear (rewrite de mailer.js/portal.js/sign.js + portal.html, ya desplegado) pendiente de gestión.

---

## App proyectos Mac conversion
*(fecha: 2026-06-28 · proyecto: Downloads/files)*

**Objetivo:** Seguir puliendo la app de escritorio "Gestor de Proyectos" (gestión de ~165-168 proyectos/bodas, migrada desde Notion/CSV), mejorando estética, usabilidad y seguridad de datos.

**Qué se hizo:**
- Rediseño visual "claro y fresco" estilo Notion/Linear (fondo crema, tarjetas blancas, SF Pro, icono propio).
- Seguridad de datos: guardado atómico, copias de seguridad automáticas (últimas 40), exportación e importación de copias — verificado con restauración real de 99 proyectos y vuelta a 165 sin pérdida.
- Tabla transformada en layout de tarjetas tipo Notion; quitado el campo Presupuesto; añadido date picker con calendario (`tkcalendar`).
- Corregido bug importante: referencias huérfanas (`entry_presupuesto`, `self.tree`) tras quitar Presupuesto que crasheaban silenciosamente la selección de tarjetas.
- Añadido botón "✨ Nuevo proyecto" con indicador de modo, y filtros combinables (Año, Proveedor, Tipo, Ubicación).
- Cada cambio verificado con tests headless (simulando eventos reales de Tk).
- Reconstruidos `.app` y `.dmg` en cada iteración.

**Decisiones clave:**
- Tarjetas visuales en vez de tabla clásica, priorizando estética sobre densidad.
- Ante petición de acceso multi-dispositivo: Tkinter es solo de escritorio; se propuso PWA + Supabase, pero el usuario decidió no seguir por ahora.
- No se borraron duplicados/inconsistencias detectadas sin confirmación explícita.

**Pendiente / próximos pasos:**
- Decidir si migrar a PWA + Supabase para acceso multi-dispositivo.
- Confirmar si unificar "Video"/"Vídeo" y limpiar duplicados detectados ("Grabación Circo Raluy", "Torneo Patinaje").

---

## RAW file compression tool
*(fecha: 2026-06-24 · proyecto: Downloads/files)*

**Objetivo:** Reemplazar Rawsie (herramienta de compresión de RAWs de Sony sin soporte) por una herramienta propia, sin pérdida de calidad y con interfaz moderna drag-and-drop.

**Qué se hizo:**
- Construida **RAWPress** (Python + Adobe DNG Converter CLI), ~50% de reducción en modo lossless (verificado con ARW reales, 68→34 MB).
- Iteraciones: Tkinter básico → reescritura en PyQt6 (drag-and-drop real, tarjetas de estado) → rediseño estilo Rawsie (fondo negro, dots animados) + fix de fecha de creación sobrescrita.
- Empaquetada como `.app` nativo arm64 + instalador DMG (~75-76 MB) con icono a medida y branding NexusMediaLab.
- Añadido contador de progreso y ETA.
- Implementado `actualizar_catalogo_lr.py`: actualiza catálogos de Lightroom tras ARW→DNG (preview de cambios, backup con timestamp, bloqueo si Lightroom está abierto).
- Corregido bug de backup del catálogo: `shutil.copy2()` fallaba con `IsADirectoryError` en Lightroom Classic v11+ (`.lrcat-data` es directorio); añadida función `_backup_item()` con `copytree`/`copy2` según tipo. Verificado con catálogo real de 1.432 ARW.
- Trabajo puntual intercalado: restauración de fecha/hora original en vídeos (.MP4/.XML de Sony) para dos bodas (181 y 590 archivos), tras detectar que una plataforma de envío había alterado las fechas.

**Decisiones clave:**
- Compresión lossless matemática (bytes idénticos) en vez de la "visualmente lossless" de Rawsie.
- Descartado `tkinterdnd2` por incompatibilidad; migrado a PyQt6.
- Compilado específicamente para arm64 (Apple Silicon).
- DMG sin firmar con cuenta de Apple Developer (requiere bypass de Gatekeeper la primera vez).

**Pendiente / próximos pasos:**
- Mejoras futuras mencionadas sin implementar: vista previa en miniatura, integración con menú de macOS, procesado automático al conectar tarjeta SD.
- Firma con cuenta de Apple Developer si se quiere distribuir más ampliamente.

## Enlaces

- [[Claude-Code]] — índice de todas las sesiones de Claude Code
- [[Tecnologia-Desarrollo]]
- [[VERA]] — la sesión "Move CLAUDE.md..." es en realidad trabajo de Vera
