---
fuente: chat "Configurar Stream Deck+ con DaVinci Resolve"
fecha: 2026-08-30
relevancia: media
tags:
  - research
  - tema/video-edicion
---

# Stream Deck+ con DaVinci Resolve

## 📝 Resumen

Configuración del Stream Deck+ en Mac para controlar parámetros de color de DaVinci Resolve (barras de luminancia máster bajo Lift/Gamma/Gain/Offset) mediante los diales físicos, ya que esos controles no tienen atajo de teclado nativo — solo responden a arrastre de ratón.

## 💡 Insights principales

- BetterTouchTool (~21€) es alternativa gratuita/económica a SideshowFX (44,99$, de pago) para mapear los diales a coordenadas de pantalla.
- Cada "Item" (1-4) de un combo en el plugin MouseMove/Multi Mouse dispara un modificador de teclado fijo distinto (Option, Cmd, Shift, Ctrl); solo el Item asignado a "Left Right" hace snap a coordenada fija.
- El atajo nativo de zoom de Resolve en Mac es Cmd (Item 2), no Option (Item 1) — error de asignación inicial.
- Fallos de atajos desde Stream Deck que sí funcionan por teclado directo suelen ser permisos de Accesibilidad en macOS.
- Para mezclar metraje Rec.709 y S-Log3/S-Gamut3.Cine en un mismo proyecto, usar Resolve Color Management (RCM) en vez de nodos manuales.

## 🛠 Aplicación práctica

- Recalibrar coordenadas del Stream Deck si se mueve/redimensiona la ventana de Resolve (limitación estructural del método por coordenadas fijas).
- Identificar el perfil de color de un clip Sony vía sus metadatos XML antes de mezclar.

## 🔗 Relacionado

- [[dossier-video-bodas]]
