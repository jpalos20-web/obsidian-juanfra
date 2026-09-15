---
title: "Configurar Stream Deck+ con DaVinci Resolve"
source: "https://claude.ai/chat/c17c2926-fc1b-475a-b869-2f231451f7c3"
author:
published: 2026-09-01
created: 2026-09-15
description: "Claude conversation with 8 messages"
tags:
  - "clippings"
---
**You**

va de derecha a izquierda, no hace zoom

---

**Claude**

Ahí está la causa — y tiene sentido con lo que vimos en los logs antes: el modificador de teclado (Option, Cmd, Shift, Ctrl) no lo eliges tú en un campo, lo asigna el plugin automáticamente según **qué pestaña de Item uses** (Item 1 = Option, Item 2 = Cmd, Item 3 = Shift, Item 4 = Ctrl). Y **Option+scroll en Resolve mueve el timeline horizontalmente (izquierda/derecha)**, no hace zoom — el verdadero atajo de zoom en Resolve en Mac es **Cmd+scroll**.

Es decir: configuraste el **Item 1** (que siempre será Option → pan izq/derecha), en vez del **Item 2** (que siempre será Cmd → zoom real).

Arréglalo así:

1. En ese mismo dial nuevo, cambia a la pestaña **"Item 2"** en vez de Item 1.
2. Pon ahí el título "Zoom" y marca "Reverse the direction of the wheel" si lo quieres igual que antes.
3. Deja el **Item 1** vacío/desactivado (así el dial solo tendrá función en Item 2, y como no vas a pulsar para ciclar, siempre usará esa).
4. Prueba a girar el dial sobre el timeline — ahora debería hacer zoom de verdad.

Si quieres además el dial de "Left Right" (pan) por separado en otro hueco, ese sí lo montas usando **Item 1**, que es el que ya tenías funcionando bien.

---

**You**

no lo entiendo

---

**Claude**

Perdona, me he liado con la explicación. Vamos más despacio, paso a paso, sin dar nada por hecho.

**Lo que hemos descubierto:** ese plugin tiene 4 "cajones" (Item 1, Item 2, Item 3, Item 4). Cada cajón hace una cosa distinta en Resolve, y no depende de lo que tú escribas, sino de **cuál de los 4 cajones uses**:

- Item 1 → mueve la imagen izquierda/derecha
- Item 2 → hace zoom
- Item 3 → otra cosa (tamaño de pista)
- Item 4 → otra cosa (subir/bajar)

Tú metiste el Zoom en el cajón **Item 1**, por eso se mueve izquierda/derecha en vez de hacer zoom. Solo hay que cambiarlo de cajón.

---

**You**

en que carpeta está todo lo que se guarda de claude, la necesito para configurar obsidian

---

**Claude**

Necesito saber a qué te refieres exactamente para no liarme, porque "lo que se guarda de Claude" puede ser varias cosas distintas:

---

**You**

P: ¿Qué producto de Claude estás usando y quieres localizar en el sistema de archivos?  
R: Claude Desktop (la app de chat)

---

**Claude**

Este es un dato clave que confirman varias fuentes: **Claude Desktop no guarda tus conversaciones en el disco de tu Mac**. La app de escritorio (y la web/móvil) es solo una ventana hacia tu cuenta en la nube — el historial de chats vive en los servidores de Anthropic, no en ninguna carpeta local que puedas apuntar desde Obsidian.

Lo único que hay realmente en tu Mac relacionado con Claude Desktop es un **archivo de configuración**, no tus conversaciones:

```
~/Library/Application Support/Claude/claude_desktop_config.json
```

Ese archivo solo contiene la configuración de conectores MCP (integraciones), no el contenido de tus chats.

**Para lo que probablemente quieres hacer** (tener tus conversaciones de Claude en Obsidian), las opciones reales son:

1. **Exportar manualmente**: dentro de claude.ai, en Ajustes → cuenta, hay una opción de exportar todos tus datos, que te llega por email como un ZIP con tus conversaciones — puedes volcar eso a una carpeta que indexe Obsidian.
2. **Copiar/pegar** conversación por conversación a notas de Obsidian, si son pocas.
3. Si lo que buscas es más bien **automatizar** ese volcado (por ejemplo con un plugin de Obsidian tipo "Claude sync"), eso normalmente usa la API de Anthropic para tirar del historial, no un archivo local — pero no tengo constancia de un plugin oficial de Anthropic para esto.

¿Es esto lo que buscabas (sacar tus conversaciones hacia Obsidian), o te referías a otra cosa como configurar Claude Desktop como cliente MCP para que Obsidian le pase datos a Claude?