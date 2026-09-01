---
estado: activo
fecha_inicio: 2026-05-13
fecha_objetivo:
tags:
  - proyecto
  - estado/activo
aliases:
  - Alba Salud
---

# Alba Salud

## 📝 Descripción

App de salud y nutrición hecha a medida para Alba (mujer de Juanfra): single-file HTML/CSS/JS (~200KB, sin backend, datos en `localStorage`), instalada como PWA en iPhone vía Safari. Integra el plan semanal de un "Gem" de Gemini (dieta + ejercicio) con seguimiento diario de comidas, ejercicio y marcadores de salud, con el objetivo de bajar de peso y mejorar marcadores hepáticos/metabólicos (GGT 237, ALT 89 al inicio). Diseño generalizado para cualquier usuario, no hardcodeado — perfil configurable en onboarding.

## 🎯 Objetivos

1. Registro diario de comidas y ejercicio sin fricción, con base de datos nutricional offline fiable.
2. Coach IA (Gemini) contextualizado con el perfil real del usuario.
3. Gamificación suave de la adherencia (rachas, Liver Score) sin ser invasiva.

## 📌 Decisiones clave

**2026-05-13 — Construcción inicial** *(fuente: chat "App personalizada de control de peso y salud")*
- Arquitectura single-file, PWA con manifest.json + service worker, safe-area para Dynamic Island.
- Rediseño estilo iOS 18/HIG: tab bar de 5 pestañas (Hoy, Progreso, Registrar, Coach IA, Más), blur, SF Pro, dark/light automático.
- Base nutricional offline ampliada a 187-265 alimentos (`NUTRICION_RAW`/`FULL_DB`) con marcas españolas (Hacendado, Milbona, Carrefour); `kcalPorcion` siempre calculado automáticamente (nunca a mano) para eliminar errores recurrentes.
- Funciones de salud: "Lista Negra" de alimentos prohibidos, "Liver Score" gamificado, medidas antropométricas con histórico, fotos de progreso comprimidas a canvas, lista de la compra generada desde el plan activo.
- Integración Gemini: API key propia del usuario (nunca hardcodeada), detección automática de modelo disponible, generación de plan semanal en JSON, análisis de foto de nevera/etiquetas.
- Báscula inteligente descartada (Web Bluetooth no viable en Safari iOS); peso manual.
- Bug recurrente: variables declaradas con `let`/`const` después de usarse en el bloque INIT — fix constante: mover declaraciones antes del INIT.
- Generado `PROYECTO-ALBA-ESTADO.md` para trasladar contexto a un Proyecto de Claude dedicado.

**2026-05-18 — Actualizar estética y funciones** *(fuente: chat "Actualizar estética y funciones de la app")*
- Rediseño Lifesum: paleta crema (`#F0EBE1`) + verde oscuro (`#1A4A2E`); dial circular SVG de calorías con arco lima→naranja→rojo.
- Liver Score rediseñado como gauge circular; tarjeta de rachas (`calcStreakRecord()`).
- Fix `showPicker()` roto en iframe/iOS Safari → selector propio de fecha (últimos 30 días).
- Fix `searchFood` (nunca estaba implementada) → búsqueda fuzzy multi-término.
- Onboarding de 3 pasos (nombre, peso/objetivo/edad/estatura, restricciones) guardado en `localStorage`; estatura añadida como campo obligatorio para IMC dinámico.
- `buildCoachContext()` generalizado para usar el perfil guardado en vez de datos hardcodeados de "Alba" — hace la app portable a cualquier usuario.

## ✅ Próximos pasos

- [ ] Revisar ajustes de diseño en móvil
- [ ] Cards de comida con foto/emoji grande y pills de macros (propuesto, no confirmado)

## 📎 Transcripciones completas

- [[2026-05-13-app-personalizada-de-control-de-peso-y-salud|Construcción inicial — 13 may]]
- [[2026-05-18-actualizar-est-tica-y-funciones-de-la-app|Actualizar estética y funciones — 18 may]]

## 🔗 Relacionado

- [[perfil-juanfra]]
