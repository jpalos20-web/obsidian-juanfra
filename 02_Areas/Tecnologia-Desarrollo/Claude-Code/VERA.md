---
title: VERA CRM
tags:
  - claude-code
  - proyecto
cwd: /Users/alba/VERA
aliases:
  - Vera
---

# 💍 VERA CRM

Carpeta local `/Users/alba/VERA`. CRM para fotógrafos y videógrafos de bodas en España (`veracrm.es` / `app.veracrm.es`, VPS en Hetzner, Docker + Caddy).

## Historial de sesiones (Claude Code)

## Vera CRM lead form optional fields + Instagram
*(fecha: 2026-08-12 · proyecto: VERA)*

**Objetivo:** El usuario fue entregando briefs sucesivos con bugs y mejoras puntuales sobre automatizaciones y la ficha de boda/lead, implementados y desplegados uno a uno.

**Qué se hizo:**
- **Vista previa de plantilla en el wizard**: sustituidos los campos editables "Asunto"/"Cuerpo" por una vista previa de solo lectura + enlace de edición, eliminando el PATCH implícito sobre `email_templates`. Commit `abbbefe`.
- **4º disparador "Lead sin respuesta"**: implementado en backend (`server/automation.js`, `server/routes/automation.js`) y frontend; verificado con leads de prueba (disparo correcto, dedup 409, envío real). Se comprobó que las "18 reglas legacy" del brief no existían en producción. Commit `e756b7c`.
- **Nombres de plantilla en notificaciones**: "Actividad reciente" y "Automatizaciones disponibles" muestran el nombre real en vez del UUID; nueva `notifyLeadFollowupSent()`. Commit `d1381d8`.
- **Fix crash en lead sin fecha**: `WeddingDetail` crasheaba por llamada sin guardia a `daysBetween` en `src/app.jsx:4968`; corregido y probado con regresión. Commit `767a453`.
- **Fix nombre "congelado" en wizard**: refactor a función pura `computeAutoName` + flag `nombreTouched`. Probado con 4 escenarios. Commit `affc009`.
- En todos los casos: pruebas con datos reales/desechables en el VPS, limpieza verificada, hashes VPS↔git comprobados tras cada despliegue.

**Decisiones clave:**
- Reutilizar patrones ya existentes (vista previa de solo lectura, criterio "sin respuesta") en vez de crear conceptos nuevos.
- Discrepancias con el brief documentadas con transparencia sin bloquear la implementación.

**Pendiente / próximos pasos:**
- Ninguno explícito en los tramos revisados; nota: el título menciona "lead form optional fields" e "Instagram", temas no cubiertos en la parte de la transcripción revisada (podrían corresponder a un tramo anterior no consultado).

---

## OAuth/Resend mailer and timeline bugs
*(fecha: 2026-06-11 · proyecto: VERA)*

> [!note] Aviso de transparencia
> El resumen de esta sesión se generó con un subagente cuya llamada de lectura activó un aviso automático de seguridad ("blocked by classifier"). El contenido revisado son nombres de variables de entorno y nombres de commits, no valores secretos, pero queda anotado aquí por si se quiere auditar.

**Objetivo:** Diagnosticar y arreglar dos bugs de producción — email de prueba fallando con `invalid_grant` (OAuth de Google) en vez de usar Resend, y botón "Ver todo →" del Cronograma sin respuesta — sin tocar deploy/.env.

**Qué se hizo:**
- Diagnosticado: un rewrite sin commitear de `server/mailer.js` introdujo un eslabón Gmail OAuth2 sin try/catch; el `gmail_refresh_token` estaba caducado, reventando cualquier envío antes de llegar a Resend.
- Arreglado `server/mailer.js`: bloque Gmail envuelto en try/catch con degradación a SMTP→Resend; auto-limpieza del token muerto en BD si el fallo es `invalid_grant`.
- Diagnosticado (vía `git blame`): el botón "Ver todo →" nunca tuvo `onClick`, huérfano desde el commit inicial.
- Arreglado `src/app.jsx`: callback `onSeeTimeline` cableado a la pestaña Timeline.
- Dos commits separados (`b55639a` mailer, `126b236` botón), desplegados y verificados en vivo (500→200 OK, caída a Resend confirmada).
- Investigado y arreglado que el backup nocturno no se ejecutaba: el bit `+x` de `backup.sh` se perdía en cada `rsync`, y `age` no estaba en el PATH mínimo de cron. Arreglado PATH explícito + `bash backup.sh` en crontab. Commit `8b4fc31`.
- Creado `MEMORY.md` y nota de traspaso (`memory/handoff-2026-06-11.md`) con el estado de producción.

**Decisiones clave:**
- Mantenida la integración Gmail "enviar como" para otros betatesters, con caída limpia a Resend en vez de forzar solo Resend a nivel de código.
- PATH explícito en `backup.sh` en vez de rutas absolutas hardcodeadas.

**Pendiente / próximos pasos:**
- Confirmar que el backup nocturno se ejecuta solo a las 03:00 sin intervención manual.
- Validar en navegador real (clic) que "Ver todo →" abre Timeline.

---

## VERA CRM database migration setup
*(fecha: 2026-06-01 · proyecto: VERA)*

**Objetivo:** Endurecer la infraestructura del VPS (backups, variables de entorno, autenticación) y construir varias features de producto (portal de novios, sincronización fiscal y de calendario, precios/cobros).

**Qué se hizo:**
- Auditoría del repo volcada en `CLAUDE.md`; backup diario de `vera.sqlite` a Backblaze B2 vía `rclone`.
- Fixes de infraestructura: `trust proxy`, `EMAIL_FROM` con dominio verificado de Resend, secretos como variables de entorno reales.
- Sincronización fiscal: `POST /api/invoices` crea automáticamente `income_entries` (IVA/IRPF); migración de IDs a `crypto.randomUUID()`.
- Google Calendar: sincronización nativa unidireccional Vera→Google (crea calendario, inserta/actualiza/borra eventos según stage).
- Pipeline: columna "Rechazadas" con modal de archivo y estadísticas por motivo.
- Módulo financiero reestructurado en 3 pestañas: Contabilidad, Hucha Fiscal, Analíticas.
- **Portal de Novios**: endpoint público con token UUID, diseño premium mobile-first, firma digital de contrato integrada (canvas táctil).
- Facturas: nueva plantilla "Editorial"; migrado a PDF server-side con Puppeteer/Chromium.
- Tabla de precios y nueva pantalla de registro/login estilo split-screen editorial.
- Iniciada migración de cobros a Lemon Squeezy (tras descartar Stripe); interrumpida a medio implementar por error de API.

**Decisiones clave:**
- Descartada sync bidireccional de Google Calendar por riesgo de conflictos; unidireccional Vera→Google.
- Descartado jsPDF y el flujo HTML+impresión manual para facturas; asentado en Puppeteer server-side.
- Lemon Squeezy elegido como Merchant of Record frente a Stripe.

**Pendiente / próximos pasos:**
- Terminar integración de Lemon Squeezy (migración DB, webhook, botones de checkout).
- Login social real con Google.
- Botón explícito "Eliminar de Google Calendar" en la ficha de boda.
- Verifactu Fase 2 (envío real a AEAT), obligatorio julio 2027.

---

## Project continuation across devices
*(fecha: 2026-05-30 · proyecto: VERA)*

**Objetivo:** Completar el sistema de facturación, implementar portal de firma digital de contratos a distancia, poner en marcha beta testers, y migrar la infraestructura a dominio propio con VPS.

**Qué se hizo:**
- Corregido cálculo de IVA en facturas (importe con IVA incluido → base imponible hacia atrás); detectado que `index.html` estaba "horneado" en la imagen Docker (requiere rebuild completo).
- Rediseñado el PDF de factura completo (QR Verifactu incluido, bug de `qrcode` → `qrcode-generator`).
- Rate limiting en login/registro/forgot-password; recuperación de contraseña por email.
- Portal de firma digital de contratos: enlace único con token, contrato con variables sustituidas, pad de firma con curvas Bezier, certificado SHA-256/IP/timestamp, subida de contrato propio en PDF.
- Sistema de beta testers: registro por invitación (`REQUIRE_INVITE`), códigos `VERA-ABCD-1234`, widget de feedback, tab "Beta" en Ajustes.
- Dominio `veracrm.es` registrado, DNS migrado a Cloudflare, VPS en Hetzner (CX23, Ubuntu 24.04) con Docker y Caddy.
- Arquitectura separada: `veracrm.es` (landing pública) y `app.veracrm.es` (app).
- Landing page rediseñada (de "dark hero" a fondo crema/serif/dorado, consistente con la app); copy del headline iterado hasta fijar mensaje "hecho por fotógrafos, para fotógrafos".
- Confirmado al final: `veracrm.es` y `app.veracrm.es` en vivo con HTTPS.

**Decisiones clave:**
- No mencionar Verifactu en la landing hasta implementación 100% legal (límite real: julio 2027).
- Vera se presenta como marca independiente, sin "build in public".
- VPS + dominio propio priorizado sobre NAS con Cloudflare Tunnel.

**Pendiente / próximos pasos:**
- Migrar datos de prueba del NAS al VPS.
- Configurar `hola@veracrm.es` vía Cloudflare Email Routing.
- Activar `REQUIRE_INVITE=true` y generar primeros códigos de invitación.
- Facturas rectificativas y numeración multi-serie.
- Portal cliente: falta envío automático por email del enlace de firma.

## Enlaces

- [[Claude-Code]] — índice de todas las sesiones de Claude Code
- [[Tecnologia-Desarrollo]]
