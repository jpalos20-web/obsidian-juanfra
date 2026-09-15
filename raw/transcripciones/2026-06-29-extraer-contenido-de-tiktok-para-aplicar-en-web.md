---
title: "Extraer contenido de TikTok para aplicar en web"
uuid: 941bcae4-b5c1-4ba2-a368-df9cb3d86ec4
fecha: 2026-06-29
fuente: conversations.json
tags:
  - transcripcion
---

# Extraer contenido de TikTok para aplicar en web

*Conversación completa, 2026-06-29. Exportada de Claude.ai, sin resumir.*

---

### 🧑 Juanfra

puedes extraer el contenido de un video de tik tok para hacer un prompt para claude para que lo aplique a una web que me hizo?

---

### 🤖 Claude

El usuario me pregunta si puedo extraer contenido de un video de TikTok para hacer un prompt para Claude que lo aplique a una web que le hizo. 

Esto me plantea dos preguntas:
1. ¿Puedo acceder/extraer contenido de TikTok?
2. ¿Qué tipo de ayuda busca exactamente?

Respecto a lo primero: No puedo acceder directamente a TikTok ni descargar videos. Sin embargo, el usuario podría:
- Compartirme un video (subirlo como archivo)
- Describirme el contenido
- Pasarme un link del que no podría extraer contenido automáticamente, pero podría ver una transcripción si la proporciona

Respecto a lo segundo: Parece que quiere que:
1. Entienda el contenido de un video de TikTok
2. Genere un prompt para Claude
3. Que ese prompt se pueda aplicar a una web (probablemente Vera CRM o otra de sus webs)

Debería ser honesto sobre mis limitaciones pero ofrecerle alternativas prácticas. Conociendo el contexto de Juanfra (trabaja en Vera CRM, Nexus Media Lab con TikTok, etc.), probablemente necesita esto para algo de sus canales o productos.No puedo acceder directamente a TikTok ni descargar videos, pero puedo ayudarte de otras formas:

**Opciones que sí funcionan:**

1. **Subes el video aquí** → Lo ves en chat, lo analizo y genero el prompt + la aplicación web que necesites

2. **Me describes el contenido** → No es tan preciso, pero si me das detalles (qué se ve, textos, estilo, flujo) puedo hacer un prompt bastante sólido

3. **Pasas un screenshot o frame del video** → Puedo verlo y trabajar desde ahí

4. **Me compartes la transcripción o el texto del TikTok** → Si ya tienes el copy, eso es suficiente

**¿Qué tipo de aplicación necesitas?**

- ¿Es para Vera CRM? (como una integración de contenido TikTok → propuesta de boda)
- ¿Un parser/extractor para Nexus Media Lab?
- ¿Una web standalone que muestre contenido estilo TikTok?
- ¿Un generador de prompts automático?

Dame más contexto y te lo resuelvo. Si es con urgencia, sube el video directo y vamos de una. 👍

---

### 🤖 Claude

El usuario ha subido un archivo mp4. Necesito ver qué contiene. Puedo usar la herramienta de lectura de archivos para entender qué tipo de archivo es y luego decidir cómo proceder.

Primero debería verificar la habilidad de lectura de archivos para saber cómo procesar un mp4.
```
This block is not supported on your current device yet.
```

Tengo el archivo mp4. Para trabajar con video, necesito extraer información. Puedo usar bash para:
1. Obtener metadatos del video (duración, resolución)
2. Extraer frames/screenshots
3. Si tiene audio, intentar transcribir

Voy a usar ffmpeg para extraer un frame del video y también para ver los detalles técnicos.
```
This block is not supported on your current device yet.
```

El ffmpeg está leyendo el archivo. Necesito ver los detalles completos del stream para entender si tiene audio y video. Voy a extraer frames y también intentar obtener más información.
```
This block is not supported on your current device yet.
```

Perfecto. El video:
- Duración: 1 minuto y 3 segundos
- Tiene audio AAC
- Tiene video H264 a 576x1024 (formato TikTok vertical 9:16)
- 30 fps

Ahora necesito:
1. Extraer un frame (screenshot) para ver el contenido
2. Si es posible, transcribir el audio para obtener el texto

Voy a extraer un frame en el medio del video y luego intentar extraer el audio.
```
This block is not supported on your current device yet.
```

Hay un error al extraer el frame. Probablemente sea un tema de codec o permisos. Voy a intentar extraer el audio directamente para transcribirlo, que es lo más importante de todos modos.
```
This block is not supported on your current device yet.
```

¡Bien! El audio se extrajo exitosamente. Ahora tengo un MP3 con el contenido de audio. Para transcribir necesitaría usar una API de speech-to-text. Pero primero, déjame intentar de nuevo extraer un frame del video de una forma diferente - maybe con PNG en lugar de JPG.
```
This block is not supported on your current device yet.
```

El frame se extrajo correctamente. Voy a guardarlo como una imagen que pueda ver.
```
This block is not supported on your current device yet.
```

Perfecto, el frame se extrajo. Ahora puedo verlo. Voy a visualizar la imagen.
```
This block is not supported on your current device yet.
```

¡Perfecto! Puedo ver el video. Es un TikTok de @notfound404.es que muestra código HTML en un editor (parece VS Code) con el tema oscuro. El tema del video es "ESTRUCTURA" (HTML structure). 

Veo código HTML típico:
- DOCTYPE
- html lang="es"
- head con meta charset, viewport, title, meta description
- Estructura básica de divs con clases
- Mentions de "etiquetas semánticas", "divs sin sentido semántico"
- Referencias a "motor de búsqueda" y "fragments más precisos en resultados"
- Mentions de "footer", "Checklist"

Parece ser un video educativo sobre buenas prácticas de HTML y la importancia de usar etiquetas semánticas en lugar de divs genéricos.

Ahora necesito transcribir el audio para obtener el contenido completo. Voy a usar la API de Anthropic para transcribir el audio con el modelo de audio.Perfecto, veo el video. Es un TikTok de **@notfound404.es** sobre **estructura HTML y etiquetas semánticas**. Veo código en VS Code mostrando HTML.

Ahora voy a extraer el audio completo y transcribirlo para generar un prompt preciso:
```
This block is not supported on your current device yet.
```

El audio tiene 1.5M. Voy a usar la API de Anthropic para transcribir este audio. Necesito leer el archivo como base64 y enviarlo a la API de Anthropic.Voy a transcribir el audio usando la API de Claude para obtener el contenido exacto:
```
This block is not supported on your current device yet.
```

Ahora voy a crear un artifact que use la API de Anthropic para transcribir el audio. Voy a usar el file con el audio en base64.
```
This block is not supported on your current device yet.
```



---

### 🧑 Juanfra

Hice una web con Claude y ahora no encuentro los chats

---
