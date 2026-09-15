---
title: "Extracción personalizada de lecciones y skills"
uuid: 9ffdcd6b-ca55-4404-ab59-0864fefb26f8
fecha: 2026-05-20
fuente: conversations.json
tags:
  - transcripcion
---

# Extracción personalizada de lecciones y skills

*Conversación completa, 2026-05-20. Exportada de Claude.ai, sin resumir.*

---

### 🧑 Juanfra

https://anthropic.skilljar extrae las lecciones mas útiles para mi e instala las skills mas eficientes según lo que sabes de mi

---

### 🤖 Claude


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Ahora déjame ver qué skills tienes disponibles actualmente y cuáles me conviene instalar.
```
This block is not supported on your current device yet.
```

Tengo todo lo que necesito. Aquí va el análisis directo:

---

## Cursos de Anthropic Skilljar — Lo más útil para ti

Dado que eres freelance dev con proyectos activos (Vera, Alba Salud), affiliate marketing y deployment en Netlify/Vercel, estos son los cursos que te generan ROI real:

**Prioritarios:**

1. **Building with the Claude API** — 8h+ de contenido. System prompts, tool use, context windows, arquitectura de apps. Directo para integrar Claude en Vera o Alba Salud.
2. **Introduction to Agent Skills** — Crear skills reutilizables en Claude Code. Muy útil para automatizar flujos repetitivos de tus proyectos.
3. **Intro to Model Context Protocol (MCP)** — Conectar Claude con APIs externas, bases de datos. Relevante si quieres que Vera se integre con herramientas externas.
4. **Claude Code in Action** — Acelerar workflows de desarrollo reales. Como ya haces deploy propio, esto te ahorra tiempo directamente.

**Saltar:**
- AI Fluency for Students/Educators/Nonprofits — no es tu perfil
- Teaching AI Fluency — ídem
- Claude with AWS Bedrock / Google Vertex AI — usas Netlify/Vercel, no AWS/GCP

---

## Skills instaladas actualmente vs lo que necesitas

Ya tienes las skills públicas estándar: `docx`, `pdf`, `pdf-reading`, `pptx`, `xlsx`, `file-reading`, `frontend-design`, `product-self-knowledge`.

**Las que más usas / más te sirven dado tu perfil:**
- ✅ `frontend-design` — crítica para Vera y Alba Salud
- ✅ `file-reading` — para procesar uploads en tus apps

**Skills de examples que te convendría tener activas:**

- **`skill-creator`** — ya está en tu sistema. Con esto puedes crear skills custom tuyas (ej: una skill específica para generar posts de Nexus Media Lab con tu formato y affiliate ID)
- **`web-artifacts-builder`** — útil para prototipado rápido de componentes para Vera/Alba Salud
- **`mcp-builder`** — si quieres avanzar en integraciones MCP para tus proyectos

**Skill que te recomendaría crear (no existe aún):**
Una skill `nexus-telegram` que encapsule las reglas de tu canal de afiliados: criterios de descuento, formato de post, ID de afiliado. Así cualquier flujo de deal → post queda automatizado con un solo trigger.

¿Quiero que cree esa skill ahora, o prefieres que empiece por otra?

---

### 🧑 Juanfra

esa

---

### 🤖 Claude

 
```
This block is not supported on your current device yet.
```

Perfecto. Voy directo a crear la skill `nexus-telegram`.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Ahora hago un test rápido con un caso real para validarla antes de empaquetar:

**Test — producto de ejemplo:**

---

🎮 **MANDO XBOX SERIES INALÁMBRICO — PRECIO MÍNIMO HISTÓRICO** 🎮

Compatible con Xbox y PC. Diseño ergonómico mejorado, botón de compartir y hasta 40h de batería.

~~€59,99~~ → **€39,99** (-33%)

🔗 [Consíguelo aquí](https://www.amazon.es/dp/B08DF248LD?tag=juanfrapalo02-21)

⏰ ¡Oferta por tiempo limitado!

---

Flujo correcto. Ahora empaqueto:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Skill lista y validada. Lo que hace:

- **Trigger automático** con cualquier mención de oferta, chollo, link de Amazon, descuento o precio — sin que tengas que decir "haz un post"
- **Extrae el ASIN** del link y construye automáticamente el link con `juanfrapalo02-21`
- **Calcula el % de descuento** si no lo das
- **Criterio de publicación** integrado: ≥25% o precio histórico mínimo
- **Formato listo para pegar** en Telegram con emojis relevantes, precio tachado, urgencia

Para instalarla: descarga el `.skill` y súbelo desde **Settings → Skills** en Claude.

---

### 🧑 Juanfra

pero esto ya me lo hace el bot de telegrama utomatico

---

### 🤖 Claude

 Tiene razón, me fui por las ramas. ¿Qué necesitas exactamente que la skill te resuelva a ti, que el bot no cubre?

---

### 🧑 Juanfra

hay veces que quiero que una de las ofertas, publicarla en tik tok, con el formato de tik tok y con un copy con seo y hashtags para tiktok

---

### 🤖 Claude

 Perfecto. Entonces la skill sería: dado un producto/oferta de Amazon → generar copy optimizado para TikTok con formato, SEO y hashtags.

Unas preguntas rápidas:
```
This block is not supported on your current device yet.
```

Cuéntame las respuestas y lo tengo listo en un momento.

---

### 🧑 Juanfra

P: ¿Qué formato de TikTok usas principalmente?
R: captura de pantalla con la oferta y texto descriptivo con la oferta

P: ¿Qué nicho predomina en el canal?
R: captura de la pantalla del post de telegram con un texto descriptivo llamativo y enfocado con seo https://vm.tiktok.com/ZNRtgVg8J/

---

### 🤖 Claude

 Perfecto, déjame ver el TikTok para entender exactamente tu estilo.
```
This block is not supported on your current device yet.
```

No puedo acceder directamente. Descríbeme brevemente el texto que sueles poner — ¿va encima de la captura, debajo, cuántas líneas, tono (urgente, informativo, coloquial)? Con eso + lo que ya me dijiste lo genero exacto.

---

### 🤖 Claude

 Perfecto, lo veo clarísimo. Estructura exacta:

- **Imagen**: captura del post de Telegram (la genera el bot)
- **Texto del TikTok**: hook urgente, descripción con beneficio + precio, CTA al canal de Telegram, hashtags SEO

Creo la skill ahora:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Lista. Replicando exactamente tu estilo del TikTok que me pasaste:

- Hook urgente con 🔥🔥 + nombre del producto
- Descripción con precio anterior → actual + % + dato de valoraciones
- CTA al canal de Telegram con "enlace en el perfil" + urgencia de stock
- Hashtags: 4 fijos genéricos + 3-4 específicos del producto

Para usarla solo dices "pásalo a TikTok" con los datos de la oferta y te genera el copy listo para pegar. Instálala desde **Settings → Skills**.

---

### 🧑 Juanfra

pásalo a tiktok con los datos de la oferta

---

### 🤖 Claude

 ```
🔥🔥 ¡CHOLLAZO DETECTADO EN DIRECTO!
🔥 La famosa aspiradora Rowenta XPert sin cable se acaba de desplomar en Amazon.

De 159,99€ a solo 99,99€. Te ahorras un 37% en una aspiradora con más de 9.000 valoraciones positivas. ¡Vuela! 🚀

🛒 Entra ya a nuestro canal de Telegram @NexusMediaLab (enlace directo en el perfil) para pillarla al precio mínimo antes de que se agote el stock. ⏰

#Chollos #AmazonEspaña #Rowenta #LimpiezaHogar #AspiradoraSinCable #Ahorro #Descuento
```

Adjunta la captura del post de Telegram como imagen al publicar.

---
