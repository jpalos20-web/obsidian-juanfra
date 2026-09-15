---
title: "Configurar Obsidian con Claude"
source: "https://claude.ai/chat/d24b8bed-fed2-40de-a1f5-cfd68713a333"
author:
published: 2026-09-01
created: 2026-09-15
description: "Claude conversation with 2 messages"
tags:
  - "clippings"
---
**You**

acabo de instalar obsidian me puedes dar un promt para que quede todo instalado perfectamente con claude?

---

**Claude**

Aquí tienes un prompt que puedes pegar en Claude Code (o Claude Desktop con acceso a archivos) para que configure tu vault de Obsidian de una:

---

**Prompt:**

```
Tengo un vault de Obsidian recién creado en [RUTA_DEL_VAULT]. Quiero que lo dejes configurado así:

1. ESTRUCTURA DE CARPETAS: crea una estructura tipo PARA (Proyectos, Áreas, Recursos, Archivo) 
   más una carpeta "00-Inbox" para notas sueltas y "Templates" para plantillas.

2. CONFIGURACIÓN CORE (.obsidian/app.json y core-plugins.json):
   - Activa daily notes, templates, backlinks, graph view, y outgoing links
   - Configura daily notes para que se guarden en una carpeta "Daily" con formato YYYY-MM-DD
   - Activa "Show line numbers" y "Strict line breaks" en editor.json

3. PLANTILLAS: crea 2-3 plantillas básicas en Templates/ (nota diaria, nota de proyecto, 
   nota de reunión) con frontmatter YAML (tags, fecha, estado)

4. COMMUNITY PLUGINS recomendados (déjame el community-plugins.json listo, aunque tenga 
   que instalarlos yo desde la UI porque requieren descarga):
   - Dataview
   - Templater
   - Calendar
   - Excalidraw (si hago diagramas)

5. Un archivo README.md en la raíz explicando la estructura y cómo uso cada carpeta.

Ve carpeta por carpeta explicándome qué hiciste al final.
```

---

**Nota importante:** los community plugins (Dataview, Templater, etc.) Claude puede dejarte el JSON de configuración listo, pero tienes que instalarlos tú desde dentro de Obsidian (Settings → Community plugins → Browse), porque se descargan directamente desde la app y no desde el sistema de archivos.

Si me dices para qué lo vas a usar principalmente (gestión de los proyectos de Vera/Nexus/Alba Salud, notas de bodas, o algo más personal) te afino la estructura de carpetas al caso concreto.