---
estado: activo
fecha_inicio: 2026-04-28
fecha_objetivo:
tags:
  - proyecto
  - estado/activo
aliases:
  - Nexus Media Lab
  - Chollos Verificados
---

# Nexus Media Lab

## 📝 Descripción

Dos frentes bajo la marca "Nexus Media Lab": (1) un canal/bot de Telegram de ofertas de Amazon España en afiliación (@ChollosVerificados, ID de afiliado `jpalos20-21`), con repurposing a TikTok; y (2) la web corporativa **nexusmedialab.es**, agencia de fotografía y vídeo corporativo de Juanfra en Barcelona (alojada en Piensa Solutions, migrada a GitHub privado).

## 📌 Decisiones clave

**2026-04-30 — Construcción del "Sniper Bot" de chollos Amazon** *(fuente: chat "Bot autónomo de Amazon Afiliados en Python")*
- Bot Python autónomo: rastrea bestsellers/goldbox/movers-and-shakers de Amazon España, genera imágenes con Pillow, publica en Telegram evitando duplicados.
- Ampliado el radar de 6 a 18 fuentes; filtros anti-inflado tras detectar "chollos falsos" (descuento mínimo 20%, valoración mínima 4★).
- Desplegado en VPS de Arsys como servicio systemd `sniperbot`; ScraperAPI/Crawlbase probados y abandonados (créditos/bloqueos) a favor de scraping directo con user-agents rotatorios.
- Amazon rechazó la cuenta de afiliado inicial (`juanfrapalo02-21`) por uso indebido de marca (color/mención "Amazon"); corregido: rediseño de imagen (fondo oscuro, verde/rojo), canal renombrado a `@ChollosVerificados`, nuevo ID `jpalos20-21`, aviso "canal independiente, no somos Amazon".
- PA-API oficial descartada (requiere 10 ventas cualificadas en 30 días). Horario automático vía cron (8:00-23:00).
- Descubierto un segundo bot en paralelo (`chollos_bot.py`/`chollosbot`) que lee ~20 canales de Telegram de chollos y republica verificando precio — ver también [[BOT]] para su evolución posterior en Claude Code.

**2026-05-20 — Skill `nexus-tiktok`** *(fuente: chat "Extracción personalizada de lecciones y skills")*
- Skill que genera copy de TikTok a partir de una oferta ya publicada en Telegram: hook urgente, precio antes/después, CTA a @NexusMediaLab, hashtags SEO en español.
- Descartada una skill `nexus-telegram` redundante (ese flujo ya lo cubre el bot automático).

**2026-06-29 — Historial perdido de nexusmedialab.es y migración a GitHub** *(fuente: chat "Historial perdido de web creada con Claude")*
- El sitio se había construido con Visual Studio Code (no Claude Code), por eso no aparecía en el historial de Claude Code.
- Auditoría SEO técnica: faltaban `<header>`/`<main>` semánticos, jerarquía de encabezados inconsistente.
- Migrado a repositorio GitHub privado (`jpalos20-web/nexusmedialab`) para versionado y backup.
- Instalada la "Taste Skill" (design-taste-frontend) tras compartir un análisis competitivo (We Are Sama, Muse Photo Studio, Keig Studio); primeros intentos de rediseño considerados "muy simplones" — ver evolución en [[BOT]].

**2026-07-01 — Rediseño vanguardista de la web (design chat)**
- Pivote de estilo negro+dorado a paleta editorial papel/tinta con rojo-tinta de acento; tipografía descomunal y grid roto.
- Hero cinético con entrada en cascada, marquesina de acento, parallax, preview de imagen flotante al pasar el cursor por servicios.
- Todo el contenido real conservado (copy, SEO, galerías, logos de clientes, formulario Formspree).

## ✅ Próximos pasos

- [ ] Decidir dirección visual definitiva de nexusmedialab.es (afinar la actual o explorar una segunda)
- [ ] Revisar solapamiento de skills de diseño instaladas (Taste Skill vs. Impeccable/Emil)

## 🔗 Relacionado

- [[BOT]] — historial técnico de Claude Code (bot Chollos Verificados, iteraciones posteriores)
- [[dossier-video-bodas]]
