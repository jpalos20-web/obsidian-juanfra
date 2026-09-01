---
title: "Reparar archivo ZIP corrupto"
uuid: 3dc24c73-4ca9-4a4b-a661-835b955cfd42
fecha: 2026-06-19
fuente: conversations.json
tags:
  - transcripcion
---

# Reparar archivo ZIP corrupto

*Conversación completa, 2026-06-19. Exportada de Claude.ai, sin resumir.*

---

### 🧑 Juanfra

me puedes arreglar un archivo .zip que no puedo descomprimir porque me da error? está en el escritorio y lleva el nombre de NOAH

---

### 🤖 Claude

The user is asking me to fix a corrupted ZIP file called NOAH on their desktop, but I don't have access to their local files—they'd need to upload it first. Let me check if there's an uploaded file in the conversation.
```
This block is not supported on your current device yet.
```

The uploads folder is empty, so I can't access the file from their desktop directly. I'll need them to upload it here before I can attempt any repairs.No tengo acceso a tu escritorio directamente, así que para que pueda intentar arreglarlo necesito que **subas el archivo NOAH.zip aquí** (botón de adjuntar). En cuanto lo tenga, intento repararlo.

Mientras tanto, esto es lo que voy a probar cuando lo suba, y algunas cosas que puedes mirar tú:

Lo más habitual con un zip que da error es que esté truncado (descarga incompleta) o tenga la cabecera/índice central dañado. Hay varias técnicas de recuperación según el caso: reparar el índice con `zip -FF`, extraer lo que se pueda ignorando errores, o recuperar streams individuales. No todos los daños tienen arreglo —si faltan bytes reales del contenido, esa parte se pierde— pero muchas veces se rescata casi todo.

Una pregunta rápida para orientarme: ¿de dónde salió el zip y qué error exacto te da?
```
This block is not supported on your current device yet.
```



---

### 🧑 Juanfra

P: ¿De dónde viene el archivo?
R: Me lo pasaron (email/chat)

P: ¿Qué error te da al abrirlo?
R: Archivo dañado/corrupto

---

### 🤖 Claude

The file they received is likely corrupted during transmission through email or chat, which is a common issue. I need them to upload the actual file directly so I can attempt to repair it — I can't work with a file I don't have access to.Vale, ese patrón (te lo pasaron por email/chat + "dañado o corrupto") encaja casi siempre con una de dos cosas: o la descarga quedó incompleta, o el cliente de correo/mensajería lo recodificó al adjuntarlo. Ambas suelen tener arreglo parcial o total.

Para intentarlo necesito el archivo aquí. **Súbelo con el botón de adjuntar** y me pongo. Cuando lo tenga voy a:

Primero comprobar si el zip está entero o truncado (mirando la firma de inicio y el índice final del archivo). Si solo está dañado el índice, lo reconstruyo con `zip -FF`, que suele recuperar todo. Si está truncado de verdad, extraigo todo lo que se pueda salvar antes del punto de corte. Te devuelvo un zip nuevo y sano con lo que se haya podido recuperar, y te digo claramente si se perdió algo.

Un par de cosas que te pueden ahorrar el viaje, por si acaso:

Si quien te lo pasó lo tiene todavía, lo más limpio es que te lo reenvíe comprimido otra vez o por un enlace (Drive, WeTransfer) en vez de adjunto directo —así evitas el problema de raíz. Y si lo descargaste y pesa sospechosamente poco comparado con lo que debería, casi seguro es descarga incompleta y basta con bajarlo de nuevo.

Si aun así quieres que lo intente yo, súbelo y lo reviso.

---

### 🧑 Juanfra

no me deja, pesa mas de 500mb

---

### 🤖 Claude

The file's too large to upload directly, so I'll need to guide them through fixing it locally on their Mac instead. Since they're comfortable with the command line, I can give them terminal commands to repair the file themselves.Claro, con más de 500MB no entra por aquí. Como estás en Mac y te manejas en terminal, lo más rápido es repararlo tú mismo. Abre la Terminal y prueba esto en orden (para si una funciona):

Primero ve al escritorio y mira qué tan roto está:

```bash
cd ~/Desktop
unzip -t NOAH.zip
```

Eso te dice si el problema es el índice o si faltan datos. Luego, el arreglo que funciona la mayoría de las veces —reconstruye el zip ignorando el índice dañado:

```bash
zip -FF NOAH.zip --out NOAH_fixed.zip
```

Te irá preguntando; responde `y` cuando diga `Is this a single-disk archive?`. Al terminar, prueba a abrir `NOAH_fixed.zip`.

Si `zip -FF` no basta, fuerza la extracción de lo que se pueda salvar saltándose los errores:

```bash
mkdir NOAH_recuperado
cd NOAH_recuperado
jar xf ../NOAH.zip 2>/dev/null || unzip -o ../NOAH.zip
```

(`jar` viene con Java; si no lo tienes, `unzip -o` igual saca lo recuperable aunque se queje.)

Dos avisos honestos: si el archivo está **truncado** de verdad (la descarga se cortó), ninguna herramienta inventa los bytes que faltan —recuperarás lo que haya hasta el corte y poco más. Y por el peso, esto huele justamente a descarga/adjunto incompleto. Si quien te lo pasó lo tiene, pídele un enlace de Drive o WeTransfer en vez del adjunto; te ahorras todo el lío.

¿Qué te suelta el `unzip -t`? Con eso te digo si vale la pena seguir o mejor pedir que te lo reenvíen.

---

### 🧑 Juanfra

NOAH-20260618T111230Z-3-001 el nombre del archivo es este

---

### 🤖 Claude

That filename pattern is characteristic of Google Drive's multi-part download system for large folders, where it splits the archive into numbered segments like `FolderName-TIMESTAMP-N-001.zip`, `N-002.zip`, and so on. The `-3-001` designation indicates this is part of a segmented download, which means the file itself likely isn't corrupted—it's just one piece of a larger split archive. Each part is independently openable, so if it's showing as corrupt, the download likely got interrupted—re-downloading is the most straightforward fix. I'm confident about Google Drive's multi-part zip naming convention from established knowledge, so I can explain this directly without needing to verify.Ah, eso cambia el diagnóstico. Ese nombre —`NOAH-20260618T111230Z-3-001`— es exactamente el patrón que pone **Google Drive** cuando descargas una carpeta grande: la parte el timestamp (`20260618T111230Z`) y el sufijo `-001`, `-002`… son los trozos.

Dos cosas importantes:

Cada parte (`-001`, `-002`…) es **un zip completo e independiente**, no son pedazos de un mismo zip que haya que unir. O sea, cada uno debería abrirse solo. Si este te da "dañado", lo más probable con diferencia es que **la descarga se cortó a media** —pasa muchísimo con archivos de +500MB desde Drive.

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

### 🧑 Juanfra

quiero descomprimirlo en el disco LaCie 2022

---

### 🤖 Claude

The user wants to extract the zip file directly to his LaCie external drive to save space on his Mac. I need to give him the command to decompress to the drive's mounted volume, which on macOS would be at `/Volumes/` followed by the drive name.Bien, eso es fácil. En Mac los discos externos se montan en `/Volumes/`. Primero confirma cómo se llama exactamente el LaCie:

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

### 🧑 Juanfra

me sale todo el rato ese mensaje

---

### 🤖 Claude

The unzip process is actually working fine — files are extracting successfully. The real issue is that the LaCie disk itself is full, which is why the write operation is failing partway through. The zip file isn't corrupted at all.

I should tell him to press `n` or Ctrl-C to stop the extraction since continuing won't help, then check the available space on the LaCie drive and either free up some room or extract to a different location instead.Ahí está la clave: **el zip no estaba roto, se descomprime bien**. El problema es otro —mira la última línea:

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

---
