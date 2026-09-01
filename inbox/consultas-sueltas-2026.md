---
tags:
  - inbox
---

# Consultas sueltas sin procesar

Conversaciones cortas de bajo valor de reutilización, importadas del historial de Claude. Pendiente de decidir si archivar o descartar.

## Transcripción de vídeo de TikTok
*(fecha: 2026-07-31)*

Pidió transcribir un vídeo de TikTok (@martinjom2.0) por enlace. Claude no puede acceder a audio/vídeo de TikTok directamente; sin resolución en el intercambio.

## App bloqueada por software malicioso
*(fecha: 2026-07-30)*

Una app "Juan Fra Songs Download" (Electron + yt-dlp, construida en un proyecto de Claude Code) fue eliminada por XProtect de macOS — falso positivo por app sin firmar. Recuperada desde el `.dmg` con `xattr -cr`. Solución permanente sugerida: firma/notarización con cuenta de Apple Developer.

## Reconciliación de gastos e ingresos en Notion
*(fecha: 2026-07-03)*

Cuadre de Notion contra movimientos de ING (PDF bancario + CSV, 65 entradas de ingresos). 395 transacciones extraídas del PDF, balance validado sin errores. Detectados ingresos en ING ausentes en Notion (reembolsos de seguros, un reembolso grande de Amazon, posibles duplicados). Reconciliación de gastos quedó pendiente.

## Extraer contenido de TikTok para aplicar en web
*(fecha: 2026-06-29)*

Preguntó si se podía extraer contenido de un TikTok para generar un prompt aplicable a una web ya hecha. Tras subir un MP4 (@notfound404.es sobre HTML semántico), se extrajeron metadatos/frame/audio con ffmpeg; transcripción quedó incompleta.

## Reparar archivo ZIP corrupto
*(fecha: 2026-06-19)*

Archivo `NOAH...zip` (>500MB, descarga multi-parte de Google Drive) marcado como dañado. El problema real resultó ser falta de espacio en el disco externo LaCie 2022, no corrupción del ZIP.

## Consumo rápido en apartado Proyectos de Claude.ai
*(fecha: 2026-05-18)*

Preguntó por qué la sección Proyectos de Claude.ai consume el límite de uso más rápido. Explicación: contexto adicional cargado en cada mensaje (instrucciones, archivos RAG, herramientas/conectores activos). Consejos: acortar instrucciones, limpiar archivos, desactivar pensamiento extendido y herramientas no usadas.

## Onboarding: primer chat
*(fecha: 2026-04-28)*

Primer chat de Juanfra con Claude: mapeo de su flujo de trabajo completo como fotógrafo de bodas (Captación → Contratación → Pre-boda → Día del evento → Post-producción), diagrama SVG interactivo, y preguntas sobre estrategias de marketing y sobre Claude Design.
