---
title: "Integración de cerebro digital con Obsidian y GitHub"
source: "https://claude.ai/chat/4dd46a8c-d524-4161-9d9d-a08359c53486"
author:
published: 2026-09-01
created: 2026-09-15
description: "Claude conversation with 4 messages"
tags:
  - "clippings"
---
**You**

vamosa hacer que tengas un cerebro conectado con obsidian y github y tengas absolutamente todo conectado para que tengas contexto de absolutamente todo

---

**Claude**

Vamos a ser realistas sobre lo que hay disponible, sin venderte humo:

**No existe un conector MCP de "Obsidian" ni de "GitHub" en el directorio** que pueda añadirte con un botón. Así que "todo conectado" no es un toggle, es un setup.

Lo que sí es real y ya funciona:

1. **GitHub** — En este chat tengo acceso directo a `github.com` y `api.github.com` desde el sandbox (bash). Puedo clonar y leer cualquier repo público tal cual. Si es privado (como el de Vera CRM, imagino), necesitaría un token tuyo para esa sesión — no se guarda entre conversaciones.
2. **Obsidian** — Obsidian no tiene API en la nube, son archivos `.md` en local (en tu caso probablemente en el Mac de Alba junto a `/Users/alba/VERA` o en otro vault tuyo). Yo desde aquí no tengo acceso a ese sistema de archivos. Dos caminos reales:
	- Subes los `.md` que quieras que lea en cada conversación (funciona, pero manual).
		- Si el vault ya está sincronizado como repo de GitHub (mucha gente lo hace para backup/versión), lo leo exactamente igual que cualquier otro repo — esto sí sería "automático".
3. **Memoria** — Ya tengo memoria persistente entre conversaciones (lo que ves reflejado arriba sobre Vera, Nexus, etc.). Eso ya te da contexto sin que hagas nada, pero es distinto de "leer en vivo" tus archivos.
4. **Lo más parecido a lo que describes de verdad** (acceso continuo al sistema de archivos de tu Mac, no solo por sesión de chat) es **Claude Code** o **Claude Desktop**, que sí trabajan directamente sobre tus carpetas locales — ahí sí podrías tener el vault de Obsidian y el repo de Vera abiertos permanentemente como contexto de trabajo. Esta interfaz de chat no llega a eso.

Pregunta clave para no perder tiempo: ¿tu vault de Obsidian ya vive en un repo de GitHub, o está solo en local?

---

**You**

esto es claude desktop

---

**Claude**

Vale, con Claude Desktop esto sí es real y bastante potente — acceso directo a tu sistema de archivos y repos, no solo por sesión de chat. Te dejo el setup completo.