---
title: "Actualizar catálogos de Lightroom con archivos DNG"
uuid: eef6715f-7a9f-4074-852b-bd86b23243f3
fecha: 2026-06-24
fuente: conversations.json
tags:
  - transcripcion
---

# Actualizar catálogos de Lightroom con archivos DNG

*Conversación completa, 2026-06-24. Exportada de Claude.ai, sin resumir.*

---

### 🧑 Juanfra

tengo la herramienta creada para convertir los raws de sony a dng, pero con esos raws tengo catalogos de lightroom, es posible actualizar esos catalogos con los nuevos dng, se que la herramienta que usaba antes, Rawsie, tenía esa opción

---

### 🤖 Claude

El usuario está preguntando sobre cómo funcionan los catálogos de Lightroom, específicamente si es posible convertir archivos RAW de Sony a DNG y luego actualizar los catálogos existentes con esos nuevos archivos, mencionando que Rawsie ofrecía esa funcionalidad. Estoy considerando si necesito verificar información en línea o si puedo responder basándome en mi conocimiento actual sobre cómo Lightroom gestiona los catálogos y las referencias de archivos.

Ahora estoy pensando en la estructura técnica: el catálogo de Lightroom Classic es una base de datos SQLite que almacena referencias a los archivos por ruta y nombre. Cuando conviertes archivos ARW a DNG, los nuevos archivos tienen una extensión diferente pero generalmente el mismo nombre base. La pregunta central es si se puede actualizar el catálogo para que apunte a los nuevos DNG mientras se preservan todos los ajustes de revelado. Lightroom tiene una función nativa de conversión a DNG que maneja esto automáticamente.

Sin embargo, si conviertes los archivos fuera de Lightroom usando una herramienta como Rawsie, los nuevos DNG no están vinculados al catálogo. El desafío es que Lightroom identifica las fotos por la ruta completa más el nombre de archivo con extensión, así que un ARW y un DNG con el mismo nombre base son archivos diferentes para el catálogo. Lo que hace Rawsie es editar directamente la base de datos SQLite del catálogo, modificando los campos de extensión y nombre de archivo en las tablas relevantes para que las entradas que apuntaban a .arw ahora apunten a .dng, preservando el ID de la foto y por tanto todos los ajustes de revelado.

El proceso sería cerrar Lightroom, hacer un backup del catálogo, abrir el archivo .lrcat con SQLite, actualizar la extensión en la tabla AgLibraryFile de ARW a DNG, reemplazar físicamente los archivos en disco, y luego abrir Lightroom nuevamente para que reconozca los DNG con los ajustes intactos. Aunque hay algunas sutilezas a considerar, como que Lightroom almacena los metadatos de revelado en el catálogo.

Ahora bien, los ajustes de revelado están vinculados al ID interno de la imagen en la base de datos, no al archivo físico, así que mientras el registro siga apuntando al nuevo archivo DNG, los ajustes se mantienen. Hay que tener en cuenta que las previews podrían regenerarse y que los ajustes creados para un ARW pueden no trasladarse perfectamente a DNG debido a diferencias en el perfil de cámara o proceso, aunque ambos contengan los mismos datos RAW.

Mirando la estructura de la base de datos de Lightroom Classic, el cambio principal ocurre en la tabla `AgLibraryFile`, donde necesito actualizar la extensión de ARW a DNG y el nombre del archivo, mientras que las referencias en `Adobe_images` y los develop settings en `Adobe_imageDevelopSettings` permanecen vinculados al mismo ID de imagen. Necesito verificar la estructura exacta del esquema SQLite del catálogo de Lightroom para asegurarme de que el SQL sea correcto y no corrompa nada. Voy a buscar esa información.
```
This block is not supported on your current device yet.
```

Tengo clara la respuesta: es posible convertir fotos a DNG de dos formas, siendo la más directa usar la herramienta nativa de Lightroom en Library > Convert Photo to DNG, aunque el usuario ya tiene su propio método implementado.

Si prefiere mantener su flujo externo, necesita editar la base de datos SQLite del catálogo, actualizando los campos de extensión, nombre de archivo y nombre original en la tabla AgLibraryFile. Lo importante es que el id_local del archivo permanece igual, así que todos los ajustes, palabras clave y colecciones se preservan automáticamente.

El proceso es directo: cerrar Lightroom completamente, hacer backup del catálogo, colocar los DNG en la misma carpeta que los originales con el mismo nombre base, luego actualizar la base de datos SQLite para cambiar la extensión de ARW a DNG y actualizar los campos relacionados del nombre de archivo.

Hay algunos detalles técnicos a tener en cuenta: el campo idx_filename suele ser el nombre en minúsculas con la extensión, la extensión se almacena sin punto y en minúsculas, y hay que confirmar estos valores con una consulta antes de hacer cambios. También existe la tabla AgHarvestedDNGMetadata que Lightroom maneja cuando convierte a DNG.

Los riesgos principales son que si los nombres o rutas no coinciden exactamente, Lightroom marcará las fotos como offline, y en macOS hay que tener cuidado con las diferencias de normalización Unicode (NFC/NFD) en nombres con acentos, algo que ya causó problemas con exiftool. Las previews y smart previews también pueden necesitar regeneración.

Podría ofrecerle un script Python que haga el UPDATE de forma segura con backup y verificación, lo cual encaja bien con su perfil de trabajo. Pero primero necesito confirmar si realmente requiere conversión externa o si le basta la nativa de Lightroom — si solo busca el resultado final, la opción nativa es trivial y sin riesgo, aunque su herramienta probablemente ofrece ventajas como compresión con pérdida controlada para ahorrar espacio.

Voy a darle la confirmación de que sí es posible (exactamente lo que hace Rawsie), explicar que Lightroom identifica archivos por id_local interno y los edits se vinculan a ese identificador, así que solo hay que actualizar el registro en AgLibraryFile con la extensión, nombre de archivo e información de ruta correctos. También le menciono los puntos críticos: considerar diferencias de normalización Unicode (NFC/NFD), asegurar que el archivo esté en la misma carpeta con el mismo nombre base, hacer backup antes, cerrar Lightroom durante la operación, y estar preparado para que se regeneren los previews. Le ofrezco escribir el script directamente.Sí, es totalmente posible, y es exactamente lo que hace Rawsie por debajo: no es magia, es editar la base de datos SQLite del catálogo.

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

### 🧑 Juanfra

creame las instrucciones para claude code para que implemente esta nueva función en la herramienta que ya tenemos creada

---

### 🤖 Claude

El usuario necesita instrucciones para que Claude Code integre la funcionalidad de actualizar catálogos de Lightroom con los nuevos archivos DNG en su herramienta existente de conversión ARW→DNG en Python. No tengo acceso al código actual de su conversor, así que necesitaré que me proporcione los detalles de cómo está estructurado.
```
This block is not supported on your current device yet.
```

Parece que el usuario menciona tener una herramienta para convertir archivos RAW de Sony a DNG, pero no la veo explícitamente en las conversaciones anteriores. Podría ser una herramienta más reciente que no tengo registrada, o tal vez esté integrada dentro de su conjunto de scripts de organización de fotos.
```
This block is not supported on your current device yet.
```

I can't find the specific ARW to DNG conversion tool in my search results—it's likely something more recent that isn't in my indexed memory, or something he's using that he didn't go into detail about. What I do know is his typical setup: single-file Python scripts running on Mac from his home directory, executed locally through Claude Code, and he relies on exiftool for the heavy lifting.

He also uses PySide6 for building GUIs, understands the NFC/NFD filename normalization issue well, generates handoff documentation like CLAUDE.md and README.md, works on his LaCie drive, and has a very specific style for Claude Code instructions—numbered steps, explicit verification at the end, "don't revert anything," and confirmation prompts.

The exact details of the DNG converter matter though—I don't know the filename, whether it's a GUI or CLI tool, or what library it uses to actually convert the files. That shapes how I'd write instructions for Claude Code. I'm weighing two approaches: asking him directly about the tool's specifics, or writing self-contained instructions that tell Claude Code to inspect the existing tool first and then add the catalog update module on top of it. The second option fits better with his workflow since Claude Code can read his local code directly.

What would be most useful and aligned with how he works is a detailed spec document I can hand to Claude Code—something self-contained with the objective, context about what the current tool does, the exact technical logic for updating the catalog (tables, fields, SQL), critical caveats like closing Lightroom, backing up, handling NFC/NFD normalization, and the structure of the new module, plus the flow with a mandatory dry-run, confirmation, and verification criteria.

The real question is whether the tool is CLI or GUI-based, since that changes how the catalog update module integrates—either as a button in the interface or as a command-line flag. I could make the instructions generic and ask Claude Code to discover the file structure, but knowing this one detail upfront would make the design much cleaner. I'll keep the catalog update as a separate opt-in step that takes the catalog path as input—safer since Lightroom needs to be closed and backed up first. I'm creating a markdown SPEC file as a standalone artifact to hand off to Claude Code, following the documentation pattern. Ahora estoy definiendo los detalles técnicos del módulo: necesito actualizar los catálogos .lrcat para que las fotos editadas apunten a los nuevos archivos DNG en lugar de los ARW originales, manteniendo intactos todos los metadatos como ediciones, palabras clave, colecciones y calificaciones. La clave es que Lightroom vincula las ediciones por el id_local de Adobe_images, así que no puedo tocar ese identificador; solo necesito cambiar la referencia al archivo físico (nombre y extensión) en la tabla AgLibraryFile, dejando el baseName igual pero actualizando la extensión.

Antes de hacer cualquier cambio, debo verificar el formato exacto de los campos extension e idx_filename en la base de datos (mayúsculas, minúsculas, presencia de punto), y asegurarme de que Lightroom esté completamente cerrado revisando que no existan archivos de bloqueo como .lrcat-wal o .lrcat-shm.

Necesito hacer un backup automático del catálogo antes de modificarlo, y como Lightroom usa Write-Ahead Logging, debo trabajar con cuidado para que el checkpoint se complete correctamente al cerrar la conexión. Los archivos DNG generados deben estar en la misma carpeta y con el mismo nombre base que los ARW originales, de lo contrario Lightroom los marcará como offline.

También tengo que considerar la normalización Unicode en macOS, donde los nombres de archivo pueden estar en diferentes formas (NFC vs NFD), así que necesitaré normalizar al comparar los nombres del catálogo con los archivos en el disco.

El flujo del módulo será: abrir una copia del catálogo, hacer un SELECT de todos los archivos ARW, verificar que existe el DNG hermano en disco construyendo la ruta absoluta desde las carpetas del catálogo, mostrar un resumen de cambios en modo dry-run, pedir confirmación explícita, y finalmente ejecutar el UPDATE en una transacción.

Para la verificación, necesito asegurarme de que el dry-run no modifica nada, que existe un backup, que después de aplicar los cambios Lightroom muestra los DNGs correctamente sin marcar las fotos como faltantes, y que los ARW sin DNG hermano se dejan intactos. También debo evitar borrar archivos ARW del disco, no tocar identificadores locales, y respetar las lecciones aprendidas sobre sintaxis de shell.

La integración debe leer primero la herramienta existente e incorporarse como módulo separado u opcional que recibe la ruta del catálogo, sin ejecutarse automáticamente después de la conversión ya que requiere que Lightroom esté cerrado y haya backup disponible. Mencionaré también los Smart Previews y la regeneración de previews, aunque AgHarvestedDNGMetadata es secundario.

Voy a escribir el SPEC de forma concisa pero completa en español, adaptable para que Claude Code inspeccione la herramienta, y al final le pediré que me pase el path exacto del conversor para afinar los detalles.

Procedo a crear el archivo directamente sin pedir confirmación, ya que pidió las instrucciones listas para usar.No encuentro en nuestro historial el detalle exacto del conversor ARW→DNG (nombre del script, si es CLI o GUI PySide6, qué usa para convertir), así que he escrito el SPEC de forma que lo primero que hace Claude Code es leer tu herramienta actual e integrarse en ella. El núcleo técnico —que es lo que aporta valor— sí va cerrado y verificado.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Listo. El SPEC le dice a Claude Code que primero lea tu conversor actual e integre el módulo según sea CLI o GUI, y lleva cerrado el núcleo crítico: el UPDATE sobre `AgLibraryFile` sin tocar `id_local`, la verificación de que Lightroom esté cerrado (WAL ausente), el backup obligatorio, la normalización NFC/NFD, el dry-run con confirmación y los criterios de aceptación.

Dos cosas que conviene que decidas tú antes de pasárselo:

El módulo va como **paso separado** (recibe la ruta del `.lrcat`), no automático tras convertir, porque exige Lightroom cerrado + backup. Si prefieres que la conversión y la actualización vayan en un solo flujo guiado, dímelo y lo ajusto.

Y si me pasas el nombre/ruta del script de conversión (y si es CLI o GUI PySide6), afino el SPEC para que el enganche sea exacto en vez de dejárselo a criterio de Claude Code.

---

### 🤖 Claude

El usuario está viendo un error en la GUI de PySide6 cuando intenta hacer backup: el código está intentando copiar un archivo `.lrcat-data` pero en realidad es un directorio, no un archivo. El error `Errno 21 Is a directory` indica que la función de copia está tratando de copiar un directorio como si fuera un archivo individual.

El problema es que en versiones recientes de Lightroom Classic, `.lrcat-data` puede ser una carpeta que contiene datos de máscaras AI y otros elementos, no solo un archivo. La solución es detectar si es un archivo o directorio y usar `shutil.copytree()` para directorios o `shutil.copy2()` para archivos, en lugar de asumir que siempre es un archivo.El error es de la implementación, no del catálogo: tu `.lrcat-data` es una **carpeta**, no un archivo. En Lightroom Classic moderno (v11+) `.lrcat-data` es un directorio (guarda las máscaras de IA, ediciones generativas, etc.), y el código está intentando copiarlo con `shutil.copy2()` / `copyfile()`, que sobre un directorio lanza justo ese `[Errno 21] Is a directory`.

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

---
