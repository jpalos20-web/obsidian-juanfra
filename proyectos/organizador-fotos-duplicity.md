---
estado: activo
fecha_inicio: 2026-04-28
fecha_objetivo:
tags:
  - proyecto
  - estado/activo
aliases:
  - DUPLICITY
  - Organizador de Fotos y Vídeos
---

# Organizador de Fotos y Vídeos (DUPLICITY)

## 📝 Descripción

App de escritorio en Python/PySide6 (proyecto "DUPLICITY", `/Users/juanfra/Desktop/DUPLICITY`) para organizar y deduplicar las fotos y vídeos de los iPhones de Juanfra y su mujer Alba: detección de duplicados exactos por hash y de casi-duplicados (fotos recomprimidas por WhatsApp, etc.), importación directa desde iPhone, y organización por fecha real de captura (EXIF/QuickTime).

## 🎯 Objetivos

1. Nunca borrar nada automáticamente — mover a `_DUPLICADOS`, siempre reversible.
2. Importar directamente desde iPhone sin depender de Finder/Fotos.
3. Detectar tanto duplicados exactos (hash) como casi-duplicados (pHash).

## 📌 Decisiones clave

**2026-06-15 — Construcción inicial** *(fuente: chat "Organizador de fotos y vídeos sin duplicados")*
- `organizador_fotos.py` (GUI, dry-run/preview, copia segura), `importar_iphone.py` (ImageCaptureCore vía PyObjC), `duplicados_perceptual.py` (pHash + BK-tree + ffmpeg para vídeo), `organizar_completo.py` (orquestador de ambos pases).
- Copiar (no mover) por defecto; sin fecha EXIF/QuickTime fiable → `Sin_Fecha/` (no usar mtime).
- Selección automática del "mejor" archivo en casi-duplicados: más píxeles > formato original (HEIC/TIFF > PNG > JPEG) > tamaño > fecha real.
- Documentos de handoff para Claude Code: `CLAUDE.md`, `README.md`, `SPEC_IMPORTAR_IPHONE.md`, `SPEC_FLUJO_COMPLETO.md`.

**2026-06-15 — Diseño de la pantalla "Importar desde iPhone" (design chat)**
- Hero degradado verde bosque→teal con hojas translúcidas flotantes, tarjetas flotantes translúcidas con profundidad.
- Iterado a banda de características integrada + selector de modo como dos tarjetas-cuadrado con insignia circular flotante.
- Handoff completo a Claude Code: README con tokens de diseño, spec de ambas pantallas, prototipo `.dc.html`, capturas.

**2026-06-23 — Renombrar fotos por hora de captura** *(fuente: chat)*
- Script Python (`renombrar_fotos.py`, librería `exifread`) para renombrar RAWs de Sony (.ARW) por hora de captura real cuando el software habitual no soporta EXIF de RAW (boda "LIDIA Y DANI").
- Fallback a fecha de modificación si no hay EXIF; modo preview + confirmación antes de aplicar.

**2026-04-28 — Origen: automatización de discos duros** *(fuente: chat "Automatización y organización de discos duros")*
- Precursor del proyecto: `buscar_duplicados.py` (hash MD5, conserva el más antiguo como original, mueve el resto a `_DUPLICADOS`).
- Ejecutado en modo `--simulacion` sobre el disco "LaCie 2022" (carpeta IPHONE, 23.427 archivos); regla de oro: simular siempre antes de mover/borrar.

## ✅ Próximos pasos

- [ ] Corregir bug de fechas por posible desajuste de normalización Unicode (NFD/NFC) al emparejar rutas con exiftool
- [ ] Resolver empaquetado `.app` con PyInstaller (falló por arquitectura)
- [ ] Corregir artefactos visuales en esquinas redondeadas (Qt stylesheet)
- [ ] Validar `importar_iphone.py` contra un iPhone real
- [ ] Terminar de aplicar el rediseño de "Importar desde iPhone" en el código real

## 📎 Transcripciones completas

- [[2026-06-15-organizador-de-fotos-y-videos-sin-duplicados|Construcción inicial — 15 jun]]
- [[2026-06-15-design-adaptar-dise-o-de-importar-fotos|Diseño de "Importar desde iPhone" — 15 jun]]
- [[2026-06-23-renombrar-fotos-por-hora-de-captura|Renombrar fotos por hora — 23 jun]]
- [[2026-04-28-automatizaci-n-y-organizaci-n-de-discos-duros|Automatización de discos duros — 28 abr]]

## 🔗 Relacionado

- [[DUPLICITY]] — historial técnico detallado de sesiones de Claude Code
- [[Tecnologia-Desarrollo]]
