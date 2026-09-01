---
estado: activo
fecha_inicio: 2026-06-24
fecha_objetivo:
tags:
  - proyecto
  - estado/activo
aliases:
  - RAWPress
---

# RAWPress

## 📝 Descripción

Herramienta propia de compresión lossless de RAWs de Sony (sustituta de Rawsie, sin soporte), con motor Adobe DNG Converter. Incluye un módulo complementario para actualizar catálogos de Lightroom Classic tras la conversión ARW→DNG.

## 📌 Decisiones clave

**2026-06-24 — Actualizador de catálogos de Lightroom** *(fuente: chat "Actualizar catálogos de Lightroom con archivos DNG")*
- El `.lrcat` es una base SQLite; los ajustes de revelado están ligados al `id_local` en `Adobe_images`, no al archivo físico — basta actualizar `extension`, `idx_filename` y `originalFilename` en `AgLibraryFile`.
- Precondiciones críticas: Lightroom cerrado (sin `.lrcat-wal`/`.lrcat-shm`), backup previo obligatorio, normalización Unicode NFC/NFD de nombres en macOS.
- Bug corregido: el backup fallaba con `IsADirectoryError` porque en Lightroom Classic v11+ `.lrcat-data` es una carpeta (máscaras IA), no un archivo — fix con `shutil.copytree()`/`copy2()` según tipo.
- Flujo obligatorio: dry-run + confirmación explícita antes de tocar el catálogo real.

## ✅ Próximos pasos

- [ ] Validar el actualizador de catálogo contra más catálogos reales

## 🔗 Relacionado

- [[Downloads-Files]] — historial técnico de Claude Code (compresión RAW, empaquetado de la app)
- [[organizador-fotos-duplicity]]
