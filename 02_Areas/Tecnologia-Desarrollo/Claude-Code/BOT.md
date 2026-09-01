---
title: BOT (Chollos Verificados / juanfrapalos.com)
tags:
  - claude-code
  - proyecto
cwd: /Users/alba/BOT
aliases:
  - Chollos Verificados
---

# 🤖 BOT

Carpeta local `/Users/alba/BOT`. Dos frentes distintos comparten este directorio:

- **Chollos Verificados** — bot de Telegram en Python que rastrea canales de ofertas de Amazon, las verifica y publica en @ChollosVerificados.
- **juanfrapalos.com** — auditoría SEO del sitio web de fotografía de bodas.

## Historial de sesiones (Claude Code)

## SEO plugin setup
*(fecha: 2026-08-13 · proyecto: BOT)*

Sesión sin contenido recuperable en el transcript (0 eventos con mensajes pese a figurar como 2/2). Sin datos sobre qué se hizo.

## SEO audit for juanfrapalos.com
*(fecha: 2026-08-14 · proyecto: BOT)*

**Objetivo:** El usuario pidió una auditoría SEO completa del sitio juanfrapalos.com (fotógrafo/videógrafo de bodas en Sabadell/Barcelona, alojado en Wix), y posteriormente solicitó que todos los entregables se le presentaran en español.

**Qué se hizo:**
- Se ejecutó una auditoría completa mediante 10 agentes especialistas en paralelo: SEO técnico, calidad de contenido, schema/datos estructurados, sitemap, rendimiento (Core Web Vitals), visual, GEO (preparación para IA), SEO local, backlinks y SXO (experiencia de búsqueda).
- Varios agentes se quedaron a medio proceso sin escribir su archivo de hallazgos y tuvieron que ser reanudados manualmente.
- Se sintetizaron los 92 hallazgos individuales en un informe global con **puntuación de salud de 45/100**, desglosada por categoría: SEO Técnico 62, Contenido 42, On-Page 37, Schema 22, Rendimiento 48, GEO/IA 50, Imágenes 55.
- Se generaron tres entregables: `FULL-AUDIT-REPORT.md`, `ACTION-PLAN.md` y `audit-data.json`, guardados en `/Users/alba/BOT/juanfrapalos.com-audit/`.
- Se intentó generar un PDF del informe, pero falló por falta de la dependencia `weasyprint` (requiere Pango/Cairo); se entregaron los archivos markdown/JSON en su lugar.
- Tras petición del usuario, se tradujeron al español los tres entregables mediante subagentes de traducción, verificando integridad y reenviando los archivos finales.

**Decisiones clave:**
- Sin credenciales de Google Search Console, PageSpeed/CrUX, DataForSEO ni Moz, el rendimiento se midió con Lighthouse local (datos de laboratorio) y los backlinks solo con Common Crawl, dejándolo explícito en el informe en vez de inventar datos.
- No se reportó puntuación de backlinks por falta de fuentes suficientes.
- Se priorizó entregar los archivos markdown/JSON sin bloquear por el fallo del PDF.

**Pendiente / próximos pasos:**
- Hallazgos críticos aún sin corregir: LCP de 7,4–12,8 s por vídeos de fondo con autoplay; ausencia total de schema de negocio (LocalBusiness/Person); página de tarifas huérfana con 55 `<h1>` duplicadas rotulada "2023"; contenido duplicado/contradictorio indexado (`/error-404` indexable, borradores huérfanos, posts de ejemplo de Wix sin editar); ausencia de teléfono visible y de reseñas/testimonios.
- Instalar `weasyprint` si se quiere el informe en PDF.

---

## Telegram bot optimization
*(fecha: 2026-07-15 · proyecto: BOT)*

**Objetivo:** Mejorar de forma iterativa "Chollos Verificados" (`chollos_bot.py`, servicio systemd `chollosbot`), corrigiendo bugs de producción y ampliando su alcance.

**Qué se hizo:**
- Detección de enlaces cortos de Amazon (`amzn.to`, `a.co`) y, después, de cualquier enlace externo del post que redirija a Amazon (capturando acortadores de terceros como `chollo.to`, `ganga.ad`).
- Eliminada la fuente RSS de Chollometro (JS-renderizado); descartado explícitamente usar Selenium/Playwright.
- Cambiado el modelo de confianza de precios: se usa el precio indicado en el propio post de Telegram (`claimed_price`) en vez de exigir confirmación por Amazon (precios distintos para peticiones anónimas), etiquetando "Precio (visto por la comunidad)".
- Generalizado el extractor de precios/descuentos para múltiples formatos de texto.
- Rotación de logs (5MB x 3 backups) y aviso al admin si pasan 6h sin publicar en horario activo (08:30–23:00).
- Corregido el texto "AHORRO: -XX%" cortado en la imagen promocional (ajuste dinámico de fuente).
- Reordenado el caption (nombre del producto primero) y añadidos emojis por categoría de producto.
- Diagnosticada y resuelta una caída total del servicio: fallo DNS de `t.me` (dominio `.me` suspendido, aparentemente OFAC); solucionado cambiando las URLs a `telegram.me`.
- Sustituido el botón "COMPARTIR" nativo por enlace directo a WhatsApp (`wa.me`) con texto precargado (última func., despliegue sin confirmar al cortar la transcripción).
- Ampliado el radar de canales de Telegram rastreados (13 → 22), verificando cada uno.
- Corregido bug de duplicación de archivo en el servidor (789 líneas en vez de ~395); logging detallado de "Descartado ..." en cada filtro.

**Decisiones clave:**
- Filtros anti-inflado: descuento mínimo 15%, precio mínimo 10€, descuentos >60% en precios <50€ tratados como sospechosos, precio "antes" limitado a 4x el actual, valoración mínima 3.8/5.
- Se priorizó volumen de publicaciones aceptando precios algo menos verificados.
- Rechazada explícitamente una sugerencia de "growth hacking" con comentarios falsos en canales competidores, por manipulación.
- `telegram.me` adoptado como solución permanente, no parche.

**Pendiente / próximos pasos:**
- Confirmar el despliegue de la función de compartir por WhatsApp.
- Decidir si añadir `@ChollosInformatica` (solo 32 suscriptores).
- No hay alerta genérica para futuras caídas tipo DNS más allá del aviso de "6h sin publicar".

## Enlaces

- [[Claude-Code]] — índice de todas las sesiones de Claude Code
- [[Tecnologia-Desarrollo]]
