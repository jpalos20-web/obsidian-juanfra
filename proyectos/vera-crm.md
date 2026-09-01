---
estado: activo
fecha_inicio: 2026-04-28
fecha_objetivo:
tags:
  - proyecto
  - estado/activo
aliases:
  - Vera
  - VeraCRM
---

# Vera CRM

## 📝 Descripción

SaaS propio de Juan Fra: un CRM para fotógrafos y videógrafos de bodas en España — "el primer CRM hecho por fotógrafos, para fotógrafos". Pipeline de leads a boda entregada, contratos con firma digital, facturación con Verifactu, cuestionario pre-boda, portal de novios, automatizaciones de email. Stack: React 18 + Node/Express + SQLite + Docker, desplegado en un VPS de Hetzner detrás de Cloudflare y Caddy (rsync deploy, backups nocturnos a R2/B2). Dominio `veracrm.es` (landing) + `app.veracrm.es` (aplicación). Compite indirectamente con BodaLab y Studio Ninja, posicionándose como más simple y hecho específicamente para el sector nupcial español.

## 🎯 Objetivos

1. Sustituir herramientas externas (Wix Ascend, PDFs manuales, WhatsApp suelto) por un flujo nativo end-to-end: lead → cuestionario → contrato firmado → factura → entrega.
2. Motor de automatizaciones fiable y sin sorpresas ("nada activo por defecto", el fotógrafo decide qué se automatiza).
3. Producto vendible a otros fotógrafos/videógrafos de boda (beta con invitación, precios Free/Pro).

## 📌 Decisiones clave y registro

**2026-07-27 — Reconstrucción completa del motor de automatizaciones** *(fuente: chat "Continuando con Vera")*
- Auditoría reveló dos motores duplicados corriendo en paralelo (`STAGE_TRIGGERS`/`scheduleWeddingEmails()` legacy vs. `automation_rules` nuevo), con race condition real en el dedup.
- Fase 1: eliminado el motor legacy, dedup atómico con transacción (`stampFired()` antes del INSERT en `email_queue`), tabla `automation_log` para auditoría.
- Fase 2: `computeSendAt()` generalizado para templates custom; dron y música migrados de envío directo a la cola con el mismo patrón atómico; decisión de no sembrar nada activo por defecto.
- Fase 3: nuevo modelo de 3 disparadores (`cambio_de_estado` / `antes_de_la_boda` / `despues_de_la_boda`), migración de 82 reglas sin pérdida, wizard de 4 pasos como único punto de creación.
- Fase 4: eliminados los 3 sembradores automáticos de reglas — a petición explícita: "no quiero nada predefinido, decido yo qué se automatiza".
- Añadido 4º disparador "lead sin respuesta en X días", con aviso de disparo retroactivo, filtro por servicio contratado, y "Enviar ahora" realmente instantáneo.

**2026-07-27 — Incidente de producción: datos de prueba en clientas reales** *(fuente: chat)*
- Contenido de prueba llegó al cuestionario real de 3 parejas por snapshot de plantilla no congelado; contención inmediata (enlaces bloqueados, plantillas vaciadas).
- Bug crítico: todo el motor (formularios, emails, firma) leía solo `wedding.email` sin fallback a `email_2`, dejando 2 bodas reales sin recibir nada silenciosamente durante semanas; corregido centralizando `weddingRecipientEmail()`.

**2026-07-27 — Constructor de formularios y notificaciones** *(fuente: chat)*
- Ancho de pregunta, secciones condicionales, checkbox obligatorio, duplicar sección, selector de variables clicable (`{{pareja}}`).
- Notificación al estudio al completar un formulario (email + PDF), con verificación multi-tenant real (404 no 403 entre estudios).
- Notificaciones en tiempo real vía Server-Sent Events sustituyendo el refresco manual.

**2026-07-27 — Bugs de fecha/zona horaria y honestidad de datos** *(fuente: chat)*
- Contrato de clienta en Florida mostraba la fecha un día antes (parseo sin anclar a UTC); corregido para fecha fija.
- Curva del dashboard (spline) inventaba subidas/bajadas falsas y el eje mostraba un día de más; corregido con interpolación monótona y marcadores reales.

**2026-07-27 — Otros fixes y decisiones de producto** *(fuente: chat)*
- 16 modales corregidos para no perder datos al clicar fuera; duplicar paquete; fuente de lead "Google Calendar" corregida tras importación.
- Rechazado adoptar la interfaz de BodaLab tal cual (evitar "parecer copiado"); reforzar identidad visual propia.
- Descartado un informe de seguridad genérico (asumía Supabase/RLS que Vera no usa); se aceptaron puntos válidos (IDOR, SQL injection, hashing) para un futuro audit real.
- Planificada Fase 1 de tests automatizados + GitHub Actions, dejando Playwright/E2E para una Fase 2.

---

**2026-07-14 — Diseño de formulario de boda** *(fuente: design chat)*
- Recreación del formulario web de juanfrapalos.com integrado en veracrm.es: plantilla editable + vista pública por pasos, ES/EN.
- Iteración 2 con identidad "Juan Fra Palos Fotografía" (foto del fotógrafo, galería de 3 fotos personalizable) y un tercer modo "Respuesta" con descarga de PDF.
- Archivo de diseño: `Formulario Boda VeraCRM.dc.html`.

**2026-06-29 — Rediseño del gráfico del dashboard (design chat)**
- Fila completa del dashboard rediseñada: tarjetas de métricas + gráfico de área interactivo + donut, con estilo editorial refinado (crema/terracota/verde, Newsreader + Hanken Grotesk).
- Gráfico de área con curvas Bézier suaves y degradados sutiles (sustituye las líneas planas originales); tooltip interactivo con línea guía y valores exactos por fecha al pasar el ratón.
- Donut "Origen de leads" interactivo: al pasar por un segmento o la leyenda se resalta y el centro muestra su porcentaje.
- Datos de ejemplo coherentes con el CRM real (26 leads, 6 bodas) para que la curva cuente una historia de crecimiento en vez de verse vacía.

**2026-06-29 — Cerrar lead con tono cercano y agradecimiento** *(fuente: chat)*
- Email de cierre para lead real (Alisha y Alex, boda 22 may 2027, Masia Casa del Mar, Sitges): felicitación, disponibilidad, dossier, propuesta de café/videollamada sin presión.
- Estilo de Juan Fra fijado como referencia: frases cortas, muletillas naturales, sin enlaces a trabajos previos salvo que se pida, nada que "suene a IA".

**2026-06-22 — Contenido de Instagram (design chat)**
- Sistema visual de marca: serif editorial Bodoni Moda, charcoal/marfil, acentos dorados, sin fotos.
- 12 piezas (6 posts + 6 historias): lanzamiento, pipeline visual, firma digital, portal de novios, "hecho en España", beta/lista de espera.
- 3 mockups de producto (MacBook/iPhone/monitor) + 8 mockups "lifestyle" estilo Pinterest, exportados a PNG/JPG a resolución real de Instagram.

**2026-06-11 — Contratos: variables, bug de "enviado" falso y render** *(fuente: chat "Vera CRM: features desplegadas y pendientes de verificar")*
- Plantilla Word real convertida al sistema de variables de Vera (`{{persona_1}}`, `{{dni_1}}`, `{{deposito}}`...); apellidos y DNI separados por persona.
- Bug crítico: estado "Enviado, pendiente firma" se marcaba al generar el enlace, no al enviar el email; fix con columna `email_sent_at` como única fuente de verdad. Auditoría encontró 4 contratos falsamente marcados (ninguno crítico).
- Firma pública y PDF renderizaban markdown crudo; arreglado. Cache de Cloudflare servía `app.js` viejo hasta 4h; resuelto con cache-buster `?v={timestamp}`.

**2026-06-11 — Motor de formularios y unificación de Emails/Automatizaciones** *(misma fuente)*
- Generalización del motor del Cuestionario (`showIf`, `bloque_rep`, etc.), migración del formulario de música, biblioteca de formularios reutilizable.
- Hallazgo grave: para 6 de 8 estudios, los 6 emails integrados nunca se habían persistido en BD — nunca se enviaron automáticamente hasta sembrarlos.
- Eliminado un `autoSend` vestigial que generaba toasts falsos de envío sin backend real.

**2026-06-11 — Pipeline configurable, ficha de lead y seguimiento** *(misma fuente)*
- Etapas del pipeline migradas de código a tabla `pipeline_stages` por estudio; "Perdido" resultaron ser dos etapas reales (`ghost`/`rejected`).
- Formulario de lead simplificado a un solo campo obligatorio; seguimiento manual con atajos +3/+7/+14 días.

**2026-06-11 — Permiso de dron, Google Calendar y onboarding** *(misma fuente)*
- Bug `invalid_grant` de Google Calendar (app OAuth en modo "Testing" revoca tokens a los 7 días); fix definitivo: publicar la app a producción.
- Checklist de onboarding automático para cuentas nuevas; backup nocturno a R2 verificado en vivo.

**2026-06-10 — Plan Ascend de Wix**
- Motivación de origen del cuestionario nativo: sustituir el plan Ascend de Wix (contratado solo para enviar formularios pre-boda) sin depender de Tally/Jotform externos.
- Definido: plantilla de cuestionario JSON preseedada por estudio, token público `/q/:token` sin login, snapshot de plantilla al enviar, PDF en cliente con html2pdf.js.

**2026-06-04 — Tres posts de Instagram y prompts de diseño** *(fuente: chat)*
- Post "Manifiesto — El CRM Invisible" (carrusel tipográfico), post "Portal Público de Contratos" (reel de firma táctil), post "Dashboard de Rentabilidad Neta".
- Auditoría comparativa de la experiencia móvil de Vera frente a BodaLab (menú hamburguesa invisible, tarjetas KPI apretadas, leyenda del donut ilegible) → instrucciones concretas de estilo mobile.

**2026-06-04 — Diseño del portal de novios (design chat)**
- Metáfora visual: tablón de corcho/moodboard de boda, estilo scrapbook (polaroids, post-its, washi tape, chinchetas).
- 8 secciones como objetos físicos: héroe con cuenta atrás, bienvenida manuscrita, calendario, contrato para firmar, paquete contratado, checklist, momentos, contacto.

**2026-06-01 — Continuidad del proyecto sin perder contexto**
- Sesión llegó al 188% del límite de contexto durante una migración de BD + integración de pago con Lemon Squeezy.
- Establecido el patrón de traspaso: `CLAUDE.md` (memoria persistente) + `PROGRESO.md` (handoff de sprint) en la raíz del repo, reconciliado contra `git diff`. Recomendación: usar `/compact` proactivamente, no como rescate de última hora.

**2026-06-01 — Diseño de facturas (design chat)**
- Dos plantillas A4 implementables: "Editorial" (papel crema, serif Cormorant) y "Moderna" (banda navy, Space Grotesk).
- QR real de Verifactu generado en cliente desde la URL de validación de la AEAT; todos los campos legales obligatorios mantenidos.

**2026-05-31 — Contenido de posts (ver conv_19 más arriba, mismo hilo de trabajo de identidad visual)**

**2026-05-14 — Prototipo completo "vera" (design chat, archivo "Studio Juan Fra")**
- Prototipo navegable completo inspirado en Studio Ninja pero simplificado: wordmark `vera`, tagline "Less clicks, more weddings."
- 6 pantallas: Inicio, Pipeline Kanban, Calendario, Mensajes (bandeja unificada), Boda en detalle (7 tabs), Configuración con importación desde Studio Ninja/HoneyBook/Excel.

## ✅ Próximos pasos

- [ ] Terminar integración de Lemon Squeezy (migración DB, webhook, botones de checkout)
- [ ] Login social real con Google
- [ ] Auditoría de seguridad real (IDOR, SQL injection, hashing de contraseñas)
- [ ] Fase 1 de tests automatizados + GitHub Actions
- [ ] Decidir si desinstalar algún skill de diseño solapado (Impeccable / Emil Kowalski / Taste Skill)
- [ ] Verifactu Fase 2 (envío real a AEAT), obligatorio julio 2027

## 🔗 Relacionado

- [[VERA]] — historial técnico detallado de sesiones de Claude Code
- [[skills-claude-code-instalacion]]
- [[Tecnologia-Desarrollo]]
