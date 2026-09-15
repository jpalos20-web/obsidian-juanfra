---
title: NexusMediaLab
tags:
  - claude-code
  - proyecto
cwd: /Users/alba/Projects/nexusmedialab
---

# 🎬 NexusMediaLab

Carpeta local `/Users/alba/Projects/nexusmedialab`. Sitio web de agencia (fotografía/vídeo corporativo).

## Historial de sesiones (Claude Code)

## Index.html redesign with Taste Skill
*(fecha: 2026-07-01 · proyecto: nexusmedialab)*

**Objetivo:** Rediseñar por completo `index.html` aplicando la skill local "design-taste-frontend" (Taste Skill, anti-AI-slop) con paleta y restricciones concretas, iterando después varias veces (tema claro, brief `rediseño.md`, versión "épica" final).

**Qué se hizo:**
- Versión 1 (oscura, Taste Skill): tipografía Cabinet Grotesk + DM Sans, paleta oro `#C9A84C` / naranja `#FF6B35`, hero asimétrico, grid de servicios tipo bento, portfolio masonry, galería carrusel con scroll-snap.
- Bug corregido: el menú móvil nunca funcionaba (faltaba la regla CSS de `.open`); reconstruido con backdrop y panel deslizante.
- Versión 2 (tema claro): fondo claro respetando "un solo tema por página"; nueva variable `--gold-ink` (`#8A6B1E`) porque el dorado original no pasaba WCAG AA en texto sobre claro; hero rehecho como split real texto/foto.
- Aplicado brief adicional del usuario (`rediseño.md`): hero con degradado radial oro→negro, servicios con grid roto, sección de Estadísticas con contadores animados, fondos alternados por sección.
- Bug real corregido: llamadas `io.observe(...)` antes de declarar `IntersectionObserver`, causando `ReferenceError` que rompía animaciones, contadores, menú móvil y formulario.
- Petición final: `index.html` "ÉPICO y AUDAZ" abandonando la Taste Skill, inspirado en We Are Sama / Muse Photo Studio / Keig Studio — hero a pantalla completa, H1 dorado ~104px, bento roto, portfolio masonry con overlay blur, botón flotante de WhatsApp pulsante.

**Decisiones clave:**
- Tema oscuro mantenido salvo petición explícita de versión clara.
- Dorado puro no usado como texto sobre fondo claro por contraste AA; variante `--gold-ink` creada solo para ese caso.
- Lightbox de galería siempre oscuro, independientemente del tema.
- Imágenes reales de `/img/` no presentes en el checkout local; se asume que se suben aparte en el despliegue (según `DEPLOY.md`).

**Pendiente / próximos pasos:**
- Sin confirmar qué versión final se mantiene (oscura Taste Skill, clara, o "épica" sin Taste Skill).
- Imágenes reales no verificadas visualmente por no estar en `/img/` local.
- `.claude/launch.json` de servidor estático añadido como conveniencia (opcional mantener o borrar).

## Enlaces

- [[Claude-Code]] — índice de todas las sesiones de Claude Code
- [[Tecnologia-Desarrollo]]
