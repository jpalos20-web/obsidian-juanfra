---
title: "Bot autónomo de Amazon Afiliados en Python"
source: "https://claude.ai/chat/ff66c3d5-199a-4f9e-9efa-cf85ae2ca272"
author:
published: 2026-07-17
created: 2026-09-15
description: "Claude conversation with 7 messages"
tags:
  - "clippings"
---
**Claude**

Ahora lo entiendo todo. El `chollosbot` es un bot muy interesante que construimos juntos — lee **20+ canales de Telegram de chollos** (Chollometro, @una\_ganga, @ofertascadahora, etc.) y republica los mejores verificando el precio en Amazon.

El problema de las zapatillas fue que leyó el precio de otro canal que tenía el precio mal, y cuando intentó verificar en Amazon (`B0C5JKGXQT`) fue bloqueado y se saltó la verificación.

Tenemos dos bots buenos pero con problemas distintos:

- **sniperbot**: scraping directo, bloqueado por Amazon en páginas de producto
- **chollosbot**: lee otros canales, verificación en Amazon también bloqueada a veces

La solución es **combinar los dos**: que el `chollosbot` sea el principal (lee otros canales sin bloqueos) y que cuando Amazon bloquee la verificación, use los datos del canal fuente en lugar de publicar con precio incorrecto.

¿Quieres que arreglemos el `chollosbot` para que cuando no pueda verificar el precio en Amazon, descarte el producto en lugar de publicarlo con el precio del canal fuente?

```bash
grep -n "bloqueo\|omite\|verificar\|precio" /root/chollos_bot/chollos_bot.py | head -20
```

---

**You**

de que canal era ese chollo?

---

**Claude**

Del log se ve claramente:

```
Canal @ofertascadahora: 20 posts leídos, 2 nuevos, 2 con link de Amazon
```

Y justo después:

```
No se pudo leer la ficha de B0C5JKGXQT (posible bloqueo puntual). Se omite.
```

Ese ASIN `B0C5JKGXQT` es el de las zapatillas Adidas. Lo leyó de **@ofertascadahora**, intentó verificar el precio en Amazon, fue bloqueado, y en lugar de descartar el producto lo publicó con el precio que venía en el post original del canal fuente (19.99€) que era incorrecto.

El fix es simple: cuando Amazon bloquee la verificación, descartar el producto en lugar de publicarlo. ¿Lo arreglamos?

---

**You**

ese canal lo tenemos en nuestra lista?

---

**Claude**

Sí, `@ofertascadahora` está en la lista de canales que monitoriza el `chollosbot`. Para ver la lista completa:

```bash
grep -n "ofertascadahora\|CANALES\|canales" /root/chollos_bot/chollos_bot.py | head -20
```

Y para ver todos los canales de la lista:

```bash
grep "telegram.me/s/" /root/chollos_bot/chollos_bot.py
```

Dime qué muestra y vemos si conviene quitarlo o mantenerlo.

---

**Claude**

Los canales están en una variable de entorno `TELEGRAM_CHANNELS`, no hardcodeados en el código. Para verlos:

```bash
cat /root/chollos_bot/.env 2>/dev/null || grep -r "TELEGRAM_CHANNELS\|ofertascadahora" /root/chollos_bot/ | grep -v ".py:"
```

O directamente:

```bash
systemctl cat chollosbot | grep -A5 "Environment\|ENV"
```

Así vemos exactamente qué canales está monitorizando y si `@ofertascadahora` está en la lista para decidir si lo quitamos.

---

**Claude**

Los canales están en `/root/chollos_bot/.env`. Veámoslos:

```bash
cat /root/chollos_bot/.env
```