---
title: Recuperar una app eliminada por Gatekeeper/XProtect en macOS
tags:
  - concepto
  - tema/macos
fecha: 2026-07-30
---

# Recuperar una app eliminada por Gatekeeper/XProtect en macOS

*(fuente: chat "App bloqueada por software malicioso", 2026-07-30)*

Una app propia de escritorio ("Juan Fra Songs Download", Electron + yt-dlp, construida con Claude Code) fue eliminada automáticamente por XProtect de macOS. Era un falso positivo: apps sin firmar/notarizar que empaquetan herramientas como `yt-dlp` disparan la protección igual que si fueran malware real.

**Cómo recuperarla:**
1. Recuperar el instalador (`.dmg`) desde donde se descargó/generó originalmente.
2. Quitar el atributo de cuarentena antes de abrirla: `xattr -cr /ruta/a/la/App.app` (o al `.dmg` antes de montarlo).

**Solución permanente:** firmar y notarizar la app con una cuenta de Apple Developer, para que macOS no la vuelva a marcar como sospechosa.

Aplicable a cualquier app propia (BOT, DUPLICITY, herramientas internas) construida sin firma de Apple.

## 📎 Transcripciones completas

- [[2026-07-30-app-bloqueada-por-software-malicioso]]

## 🔗 Relacionado

- [[Tecnologia-Desarrollo]]
- [[index]]
