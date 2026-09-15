---
title: "Actualizar catálogos de Lightroom con archivos DNG"
source: "https://claude.ai/chat/eef6715f-7a9f-4074-852b-bd86b23243f3"
author:
published: 2026-06-24
created: 2026-09-15
description: "Claude conversation with 5 messages"
tags:
  - "clippings"
---
**You**

tengo la herramienta creada para convertir los raws de sony a dng, pero con esos raws tengo catalogos de lightroom, es posible actualizar esos catalogos con los nuevos dng, se que la herramienta que usaba antes, Rawsie, tenía esa opción

---

**Claude**

Sí, es totalmente posible, y es exactamente lo que hace Rawsie por debajo: no es magia, es editar la base de datos SQLite del catálogo.

La clave está en entender cómo identifica Lightroom las fotos. Los ajustes de revelado, keywords, colecciones, ratings... todo cuelga de un ID interno (`Adobe_images.id_local`), no del archivo físico. Ese registro apunta a una fila en la tabla `AgLibraryFile` mediante `rootFile`. O sea: si solo cambias la **extensión** en `AgLibraryFile` (de `arw` a `dng`) sin tocar el `id_local`, conservas absolutamente todos los edits y metadatos; Lightroom simplemente empieza a leer el `.dng` en lugar del `.arw`.

Los campos que tienes que tocar en `AgLibraryFile` son:

- `extension` → de `arw` a `dng` (ojo al formato exacto, normalmente minúsculas; míralo con un SELECT antes)
- `idx_filename` → el nombre indexado en minúsculas con extensión (`img_1234.arw` → `img_1234.dng`)
- `originalFilename` → `IMG_1234.ARW` → `IMG_1234.DNG`

El `baseName` se queda igual porque no cambia.

El procedimiento seguro:

1. **Cierra Lightroom del todo** (que desaparezcan los `.lrcat-wal` y `.lrcat-shm`; si no, pierdes cambios o corrompes).
2. **Backup** del `.lrcat` y `.lrcat-data`.
3. Los DNG tienen que estar en **la misma carpeta y con el mismo nombre base** que los ARW. Si no, LR los marcará como "missing/offline".
4. Haz el UPDATE en SQLite.
5. Abre LR. Las previews se regeneran solas (smart previews también), eso es normal.

Dos avisos que para tu caso son críticos:

- **Unicode NFC/NFD en macOS** — el mismo problema que tuviste con exiftool. Si algún nombre lleva acentos o ñ, el `idx_filename` del catálogo y el nombre real del DNG en disco pueden no coincidir byte a byte y LR lo dará por perdido. Normaliza a NFC en ambos lados.
- Los develop settings se aplican igual porque el DNG contiene el mismo mosaico RAW, pero el perfil de cámara base puede mostrar diferencias mínimas en algún caso. En la práctica con Sony se ve idéntico.

Dado que ya tienes tu conversor ARW→DNG en Python, lo lógico es que el mismo flujo, tras convertir, repunte el catálogo. ¿Quiero que te escriba el script que: hace backup automático, detecta los ARW del catálogo que tienen un DNG hermano en disco, hace un dry-run mostrando qué va a cambiar, y luego aplica el UPDATE con normalización NFC? Lo dejo con el patrón de handoff que usas para Claude Code.

Una alternativa sin tocar SQL: la conversión nativa de Lightroom (`Library > Convert Photo to DNG`) hace todo esto sola y sin riesgo, pero pierdes el control de tu propio conversor (y la compresión lossy tipo Rawsie, si es lo que buscas para ahorrar espacio).

---

**You**

creame las instrucciones para claude code para que implemente esta nueva función en la herramienta que ya tenemos creada

---

**Claude**

No encuentro en nuestro historial el detalle exacto del conversor ARW→DNG (nombre del script, si es CLI o GUI PySide6, qué usa para convertir), así que he escrito el SPEC de forma que lo primero que hace Claude Code es leer tu herramienta actual e integrarse en ella. El núcleo técnico —que es lo que aporta valor— sí va cerrado y verificado.

---

**Claude**

El error es de la implementación, no del catálogo: tu `.lrcat-data` es una **carpeta**, no un archivo. En Lightroom Classic moderno (v11+) `.lrcat-data` es un directorio (guarda las máscaras de IA, ediciones generativas, etc.), y el código está intentando copiarlo con `shutil.copy2()` / `copyfile()`, que sobre un directorio lanza justo ese `[Errno 21] Is a directory`.

Mi SPEC lo describió como archivo y ahí estuvo el fallo. Se arregla detectando el tipo antes de copiar. Pásale esto a Claude Code:

```
BUG en el backup del módulo actualizar_catalogo_lr: al respaldar el catálogo
falla con "[Errno 21] Is a directory" sobre el .lrcat-data.

CAUSA: en Lightroom Classic v11+ el ".lrcat-data" NO es un archivo, es un
DIRECTORIO (contiene máscaras IA y ediciones generativas). El backup usa
shutil.copy2()/copyfile(), que sobre una carpeta lanza IsADirectoryError (Errno 21).

ARREGLO:
1. En la función de backup, detectar el tipo de cada elemento antes de copiar y
   usar la función adecuada. Algo así:

   import os, shutil
   def _backup_item(src, dst):
       if os.path.isdir(src):
           shutil.copytree(src, dst)   # .lrcat-data es carpeta
       else:
           shutil.copy2(src, dst)      # .lrcat es archivo

2. Aplicarlo tanto al ".lrcat" (archivo) como al ".lrcat-data" (carpeta) y, si
   existe, a cualquier ".lrcat-data" hermano. Si .lrcat-data no existe, saltarlo
   sin error.
3. El destino del backup sigue el patrón con timestamp:
   nombre.lrcat.bak-YYYYMMDD-HHMMSS  y  nombre.lrcat-data.bak-YYYYMMDD-HHMMSS
   (copytree crea la carpeta destino; asegúrate de que no exista ya).
4. NO toques la lógica de UPDATE ni la verificación de WAL: solo el backup.
5. Verifica con el catálogo "Barberà vs. Terrassa.lrcat" en /Volumes/LaCieBackup:
   que el dry-run llegue a mostrar conteos sin reventar en el backup.
```

Un apunte aparte: estás trabajando sobre el catálogo en `/Volumes/LaCieBackup/...`. Asegúrate de que ahí están también los `.dng` ya convertidos, en la misma carpeta y con el mismo nombre base que los `.ARW`, o el dry-run te dirá que no encuentra los DNG hermanos y no actualizará nada (que es el comportamiento correcto y seguro, pero no es lo que buscas).