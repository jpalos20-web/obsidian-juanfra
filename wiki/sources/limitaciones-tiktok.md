---
title: Limitaciones al procesar contenido de TikTok
tags:
  - resources
  - tema/claude
  - sin-resolucion
---

# Limitaciones al procesar contenido de TikTok

Dos intentos de usar Claude para trabajar con vídeos de TikTok, ninguno resuelto del todo. Útil como referencia rápida de qué NO funciona sin pasos previos.

## Transcribir un vídeo de TikTok por enlace
*(fuente: chat "Transcripción de video de TikTok", 2026-07-31)*

Pidió transcribir un vídeo de TikTok (@martinjom2.0) pasando solo el enlace. Claude no puede acceder a audio/vídeo de TikTok directamente a partir de una URL — sin resolución en el intercambio.

## Extraer contenido de un TikTok para aplicar a una web
*(fuente: chat "Extraer contenido de TikTok para aplicar en web", 2026-06-29)*

Quería extraer el contenido de un TikTok (@notfound404.es, sobre HTML semántico) para generar un prompt aplicable a una web ya hecha. Subiendo el MP4 directamente sí se pudieron extraer metadatos/frame/audio con `ffmpeg`, pero la transcripción del audio quedó incompleta.

**Lección:** para trabajar con un TikTok concreto, subir el archivo de vídeo/audio directamente (no el enlace) y esperar tener que ayudar a `ffmpeg`/transcripción manualmente.

## 📎 Transcripciones completas

- [[2026-07-31-transcripci-n-de-video-de-tiktok]]
- [[2026-06-29-extraer-contenido-de-tiktok-para-aplicar-en-web]]

## 🔗 Relacionado

- [[index]]
