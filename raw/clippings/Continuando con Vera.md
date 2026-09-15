---
title: "Continuando con Vera"
source: "https://claude.ai/chat/39c31eea-e23b-48a6-a211-4c1925440fb6"
author:
published: 2026-09-01
created: 2026-09-15
description: "Claude conversation with 9 messages"
tags:
  - "clippings"
---
**Claude**

Voy a ver el resto del documento antes de comentarlo, hay una parte truncada con lo que probablemente sea el contenido más aplicable a Vera (OWASP Top 10, multi-tenant, base de datos).

---

**You**

y que podemos aprender de este audio?

---

**Claude**

Voy a intentar transcribirlo para poder comentarlo contigo — vamos a ver si el entorno lo permite.

---

**You**

que podemos aprender de esto para vera?

---

**Claude**

Este vídeo da en el clavo, y conecta directamente con algo que llevamos viendo toda la sesión sin nombrarlo así: **hoy, la única red de seguridad que tiene Vera es que Code se acuerde de probar manualmente, cada vez, en cada brief.** Ha sido un nivel de disciplina manual excelente —cuentas de prueba desechables, verificación en base de datos, limpieza al final—, pero es exactamente lo que el vídeo describe como insuficiente: funciona mientras alguien se acuerde de probarlo todo, cada vez, para siempre. Y hoy hemos tocado funciones compartidas (`weddingRecipientEmail`, `sendQueuedEmail`, `findRetroactiveMatches`, el generador de nombres del wizard, el selector de variables) en decenas de briefs distintos — cada vez confiando en que el brief de turno se acordara de probar la regresión correcta.

De hecho, tenemos un ejemplo real de hoy mismo de exactamente el fallo que describe el vídeo: el bug del nombre del wizard que no se actualizaba llevaba ahí un tiempo, sin que ningún brief lo detectara, hasta que **tú** lo viste en pantalla. Eso es "se entera tu cliente antes que tú" — solo que esta vez el "cliente" fuiste tú mismo mirando tu propia app.

Traduzco las tres piezas del vídeo a lo que necesitaría Vera:

1. **Playwright para el flujo web** — en vez de que Code abra un navegador y haga clics manuales cada vez (que es literalmente lo que ha hecho hoy, brief tras brief), esos mismos recorridos (login, crear boda, enviar formulario, forzar automatización, firmar contrato) se graban una vez como script y se repiten solos, para siempre, gratis.
2. **Verificar el resultado interno, no solo que "parece que funciona"** — el equivalente en Vera al cálculo de calorías es la aritmética de fechas (`addOffsetYMD`), el guardado atómico contra duplicados, el cálculo de qué bodas cumplen una condición retroactiva. Ahí un fallo silencioso no es solo feo, es un email que no debía salir o que sale dos veces.
3. **Una GitHub Action que bloquee el despliegue si algo falla** — esta es la pieza que más le falta a Vera ahora mismo. Hoy, cualquier `git push` se despliega igual, tanto si las pruebas manuales de ese brief salieron bien como si un cambio rompió silenciosamente algo de otro brief de hace tres semanas que nadie volvió a mirar.

¿Quieres que prepare un brief para montar esto — empezando por un puñado de pruebas automatizadas de las funciones que más veces nos han dado sustos hoy (fechas, dedup, fallback de email), más una Action que bloquee el deploy si fallan?

---

**You**

si

---

**Claude**

Preparo el brief, mismo formato que todos hoy, con una diferencia importante: como es una pieza de infraestructura y no un bug puntual, lo divido en dos fases para no intentarlo todo de golpe.

---

**You**

quiero exportar todas este chat, se puede?

---

**Claude**

Buena pregunta — voy a comprobar cómo funciona esto exactamente en la documentación, en vez de suponerlo.