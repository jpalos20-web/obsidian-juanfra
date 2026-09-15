---
title: "Vera: tracking de emails/PDFs — plan de cumplimiento legal"
tags:
  - concepto
  - tema/vera-crm
  - tema/legal
fecha: 2026-09-15
---

# Vera: tracking de emails/PDFs — plan de cumplimiento legal

*(fuente: `raw/gemini/consultas-vera-tracking-legal.md`, conversación con Gemini, 2026-09-15)*

Consulta sobre cómo implementar en Vera un seguimiento de apertura de emails y lectura de PDFs (al estilo Mailtrack/Mailsuite y DocSend) sin riesgo legal bajo RGPD/LSSI-CE, partiendo de que Vera es un proyecto que empieza y no podría absorber una sanción de la AEPD (que para una startup pequeña ronda entre 3.000-15.000 €, no los 100.000 € de referencia de Mailtrack).

**Plan de "Riesgo Cero" propuesto para el lanzamiento:**

1. **Sin píxeles de tracking en emails.** El valor analítico de saber si se abrió un correo es bajo frente al riesgo legal de un rastreo invisible; además muchos clientes de correo ya bloquean la descarga de imágenes, así que ni siquiera funcionaría de forma fiable.
2. **PDFs sin seguimiento intrusivo, en dos fases:**
   - *Fase 1 (súper-lean):* compartir los PDFs como enlaces estáticos de solo lectura (Dropbox/Google Drive corporativo) con DPA firmado — riesgo legal prácticamente nulo, pero sin saber qué páginas se leen.
   - *Fase 2 (si hace falta analítica):* portal de consentimiento simple al abrir el enlace — dos opciones del mismo tamaño ("Aceptar y abrir" vs. "Abrir sin seguimiento"), cumpliendo el principio de no condicionalidad del consentimiento del RGPD.
3. **Analítica agregada, no individual.** Medir "el PDF de propuesta tuvo 15 visitas hoy" en vez de "Juan Pérez lo abrió a las 10:15", con IP anonimizada/truncada de inmediato — la AEPD exime de consentimiento la analítica agregada que no identifica a una persona física.
4. **Convertir la privacidad en argumento de venta B2B:** mensaje explícito tipo "en Vera no usamos píxeles espía ni rastreo invisible" en el pie de los correos/propuestas, como diferenciador frente a herramientas más intrusivas.

## 🔗 Relacionado

- [[vera-crm]]
- [[index]]
