---
title: "Reparar archivo ZIP corrupto"
source: "https://claude.ai/chat/3dc24c73-4ca9-4a4b-a661-835b955cfd42"
author:
published: 2026-06-19
created: 2026-09-15
description: "Claude conversation with 5 messages"
tags:
  - "clippings"
---
**Claude**

Ah, eso cambia el diagnóstico. Ese nombre — `NOAH-20260618T111230Z-3-001` — es exactamente el patrón que pone **Google Drive** cuando descargas una carpeta grande: la parte el timestamp (`20260618T111230Z`) y el sufijo `-001`, `-002` … son los trozos.

Dos cosas importantes:

Cada parte (`-001`, `-002` …) es **un zip completo e independiente**, no son pedazos de un mismo zip que haya que unir. O sea, cada uno debería abrirse solo. Si este te da "dañado", lo más probable con diferencia es que **la descarga se cortó a media** —pasa muchísimo con archivos de +500MB desde Drive.

Por eso, antes de pelearte con `zip -FF`, lo que de verdad te va a arreglar esto es **volver a descargarlo**. Si quien te lo pasó te dio enlace de Drive, bájalo otra vez (mejor desde un navegador estable, sin pausar). Si te pasó solo este adjunto, pídele que comparta la carpeta por enlace de Drive directamente en vez de adjuntar el zip —así descargas tú y evitas el corte.

Si aun así quieres rescatar lo que haya en el trozo dañado, los comandos que te pasé siguen valiendo:

```bash
cd ~/Desktop
unzip -t NOAH-20260618T111230Z-3-001.zip
```

Eso te confirma si está truncado. Si lo está, sacas lo recuperable con:

```bash
mkdir NOAH_recuperado && cd NOAH_recuperado
unzip -o ../NOAH-20260618T111230Z-3-001.zip
```

Pero te lo digo claro: si la descarga quedó incompleta, recuperarás solo los archivos que entraron enteros antes del corte. Lo limpio es bajarlo de nuevo.

Una duda: ¿solo tienes el `-001` o hay más partes (`-002`, etc.)? Y si está el `.zip` al final del nombre, asegúrate de incluirlo en los comandos.

---

**You**

quiero descomprimirlo en el disco LaCie 2022

---

**Claude**

Bien, eso es fácil. En Mac los discos externos se montan en `/Volumes/`. Primero confirma cómo se llama exactamente el LaCie:

```bash
ls /Volumes/
```

Te saldrá el nombre tal cual (por ejemplo `LaCie`, `LaCie 2022`, etc.). Con ese nombre, descomprime directamente ahí:

```bash
unzip ~/Desktop/NOAH-20260618T111230Z-3-001.zip -d "/Volumes/LaCie 2022/NOAH"
```

Eso crea una carpeta `NOAH` dentro del disco y mete todo dentro. Las comillas son importantes si el nombre lleva espacios.

Si el zip está dañado y `unzip` normal se queda a medias, usa `-o` para que siga pese a los errores y saque lo que pueda:

```bash
unzip -o ~/Desktop/NOAH-20260618T111230Z-3-001.zip -d "/Volumes/LaCie 2022/NOAH"
```

Dos avisos rápidos: comprueba que el LaCie esté formateado en algo que admita archivos grandes y nombres largos —si es **exFAT** o **APFS/Mac OS Plus**, perfecto; si fuera **FAT32** te petaría con cualquier archivo de más de 4GB. Y asegúrate de tener espacio libre suficiente, que descomprimido ocupará más que el zip.

¿Confirmas el nombre exacto que te sale en `ls /Volumes/` y te dejo el comando ya listo para copiar y pegar?

---

**You**

me sale todo el rato ese mensaje

---

**Claude**

Ahí está la clave: **el zip no estaba roto, se descomprime bien**. El problema es otro —mira la última línea:

`write error (disk full?). Continue? (y/n/^C)`

El LaCie se está quedando **sin espacio** mientras escribe. Por eso te sale una y otra vez: cada archivo que intenta escribir falla.

Pulsa `n` (o `Ctrl-C`) para cortar, no tiene sentido seguir si el disco está lleno. Luego comprueba cuánto espacio te queda:

```bash
df -h "/Volumes/LaCie 2022"
```

Mira la columna `Avail`. Si está a cero o casi, esa es la causa. Opciones:

Liberar espacio en el LaCie y volver a lanzar el `unzip`. O descomprimir en otro sitio con hueco (por ejemplo el propio Mac, si tienes espacio, o el disco interno temporalmente).

Un detalle que vi de paso: te está creando `NOAH/NOAH/` (carpeta dentro de carpeta) porque el zip ya traía una carpeta `NOAH` dentro y tú lo mandaste a otra `NOAH`. No es grave, pero si quieres evitarlo descomprime a secas en `/Volumes/LaCie 2022` y ya se crea la carpeta interna sola.

¿Qué te dice el `df -h`? Con el espacio disponible te digo si cabe o hay que buscar otro destino.