---
title: Exportar conversaciones a Obsidian — cómo nació este vault
tags:
  - concepto
  - tema/obsidian
fecha: 2026-09-15
---

# Exportar conversaciones a Obsidian — cómo nació este vault

*(fuente: clipping "Exportar conversaciones a Obsidian", 2026-09-15 — captura parcial)*

Esta conversación documenta el origen de `raw/transcripciones/`: fue un **volcado puntual**, no una sincronización continua. Claude (en claude.ai) leyó 27 conversaciones pasadas, generó notas `.md` con el contenido y Juanfra las descargó en un zip para que Claude Code las metiera en el vault a mano.

También aclara un punto importante que sigue vigente: **no existe hoy ningún puente automático** entre "lo que se habla en claude.ai/app" y "se guarda solo en Obsidian". Ni Claude Code ni ningún conector MCP pueden ir a buscar solos el historial de chats pasados — esa herramienta de búsqueda de conversaciones solo existe dentro de la interfaz de chat de claude.ai. Las opciones reales para mantener esto al día son todas semi-manuales:

1. Repetir el volcado puntual de vez en cuando (pidiéndolo explícitamente en claude.ai).
2. Un recordatorio propio (calendario/tareas) para acordarse de hacerlo.
3. Un web clipper de Obsidian (plugin comunitario + Local REST API) que sí puede capturar una conversación abierta bajo demanda — parece ser lo que generó los archivos de `raw/clippings/` el 2026-09-15.

De paso, esta conversación es también la que descubrió y arregló la colisión de nombre entre el `CLAUDE.md` de la raíz del vault y el symlink `02_Areas/Tecnologia-Desarrollo/CLAUDE.md` (que apunta al `CLAUDE.md` real del repo de Vera) — de ahí que ese symlink se llame hoy [[Vera-CRM-Memoria-Tecnica]].

## 📎 Clipping

- [[Exportar conversaciones a Obsidian]]

## 🔗 Relacionado

- [[configurar-obsidian-con-claude]]
- [[integracion-cerebro-digital-obsidian-github]]
- [[Indice-Transcripciones]]
- [[index]]
