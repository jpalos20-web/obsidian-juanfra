---
title: "App bloqueada por software malicioso"
source: "https://claude.ai/chat/9e737b7a-ecb2-4905-97b0-74e9471588ca"
author:
published: 2026-07-30
created: 2026-09-15
description: "Claude conversation with 4 messages"
tags:
  - "clippings"
---
**Claude**

Vale, vamos a verificarlo con datos, no de memoria.

---

**Claude**

Vale, esto lo cambia todo — es tu app real, construida en un proyecto tuyo de Claude Code ("Build stacher-like app"), un descargador estilo Stacher con Electron + yt-dlp + ffmpeg. Perdona la desconfianza inicial, pero con un mensaje de "malware eliminado" y un nombre que no reconocía en tu historial, tocaba verificar antes de ayudar a saltárselo.

Ahora el problema real: **es un falso positivo**, y es bastante común en apps así. La razón:

- Tu app no está firmada con un certificado de Apple Developer (`codesign` + notarización), así que macOS no puede verificar quién la hizo.
- Lleva **yt-dlp** empaquetado — una herramienta que un porcentaje enorme de malware real también empaqueta disfrazado de "descargador de YouTube gratis". XProtect (el antivirus de Apple) usa firmas heurísticas, y a veces esas firmas coinciden con patrones de apps Electron + yt-dlp sin firmar, aunque el código sea legítimo.

**Qué hacer:**

1. **Confirma qué detectó XProtect** (opcional pero útil): abre la app *Consola* (Console.app) → busca "XProtect" en el buscador → filtra por hora en la que abriste la app. Te dirá el nombre de la firma que coincidió.
2. **Arreglo rápido (uso personal, sin firma de Apple):**
	- Vuelve a copiar el `.app` desde el `.dmg` a Aplicaciones (si XProtect ya lo borró, necesitas el `.dmg` original de nuevo).
		- Antes de abrirlo, quita el atributo de cuarentena desde Terminal:

```
xattr -cr "/Applications/Juan Fra Songs Download.app"
```

- Esto evita que Gatekeeper/XProtect vuelva a interceptarla en el arranque.
3. **Arreglo real y permanente:** si vas a repartir esta app a más gente (o quieres dejar de pelearte con esto cada build), necesitas:
	- Una cuenta de **Apple Developer** (99$/año)
		- Firmar el `.app` con `codesign --deep --sign "Developer ID Application: Tu Nombre"`
		- Notarizarla con `xcrun notarytool submit`
	Esto elimina el problema de raíz porque Apple verifica el binario y dejas de depender de heurísticas.

¿Quieres que te prepare el brief para pasarle a Claude Code el flujo de firma + notarización (paso 3), o de momento te vale con el `xattr -cr` para uso personal?

---

**You**

no entiendo los pasos para el uso personal ( el apso de la consola, xprotect, no me aparece por ningún sitio)

---

**Claude**

Sin problema, olvida el paso de la Consola — no es necesario, era solo diagnóstico opcional. Vamos directo a la solución:

**1\. Recupera la app**

Como XProtect ya la borró, necesitas volver a copiarla desde el `.dmg` original:

- Busca el archivo `.dmg` que descargaste/exportaste (probablemente en Descargas, o donde lo tengas guardado)
- Haz doble clic para montarlo
- Arrastra de nuevo el icono a Aplicaciones (sobrescribe si te pregunta)

Si no tienes ya el `.dmg` a mano, dime y vemos cómo generarlo otra vez desde el proyecto de Claude Code.

**2\. Quítale la cuarentena antes de abrirla**

Abre la app **Terminal** (Cmd+Espacio, escribe "Terminal", Enter) y pega esto:

```
xattr -cr "/Applications/Juan Fra Songs Download.app"
```

Pulsa Enter. No debería devolver nada (o silencio = bien).

**3\. Ábrela**

Doble clic en la app desde Aplicaciones. Ya no debería saltar el aviso de malware.

---

Si al pegar el comando en Terminal te da un error tipo "Operation not permitted", dímelo y lo resolvemos (a veces Terminal necesita permiso de "Acceso completo al disco" en Ajustes → Privacidad y Seguridad).