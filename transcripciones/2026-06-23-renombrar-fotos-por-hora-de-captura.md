---
title: "Renombrar fotos por hora de captura"
uuid: 45b60986-fa5d-405e-b486-0446023406e3
fecha: 2026-06-23
fuente: conversations.json
tags:
  - transcripcion
---

# Renombrar fotos por hora de captura

*Conversación completa, 2026-06-23. Exportada de Claude.ai, sin resumir.*

---

### 🧑 Juanfra

puedes ordenarme por hora de captura y renombrarme  todos los archivos de una carpeta de fotos a L&D_0001 y así sucesivamente?
Con el programa que lo hago me da error:
An error occurred while renaming photo "A7408883.ARW".
The operation will be cancelled, and the original filenames will be restored.
Unable to get item information for '/Volumes/LaCie/JUAN FRA PALOS FOTOGRAFÍA 2026/LIDIA Y DANI/FOTOS/A7408883.ARW'
No plugin available to handle '/Volumes/LaCie/JUAN FRA PALOS FOTOGRAFÍA 2026/LIDIA Y DANI/FOTOS/A7408883.ARW'
No plugin available to handle '/Volumes/LaCie/JUAN FRA PALOS FOTOGRAFÍA 2026/LIDIA Y DANI/FOTOS/A7408883.ARW'
No plugin available to handle '/Volumes/LaCie/JUAN FRA PALOS FOTOGRAFÍA 2026/LIDIA Y DANI/FOTOS/A7408883.ARW'
Unable to get item information for '/Volumes/LaCie/JUAN FRA PALOS FOTOGRAFÍA 2026/LIDIA Y DANI/FOTOS/A7408883.ARW'
No plugin available to handle '/Volumes/LaCie/JUAN FRA PALOS FOTOGRAFÍA 2026/LIDIA Y DANI/FOTOS/A7408883.ARW'
No plugin available to handle '/Volumes/LaCie/JUAN FRA PALOS FOTOGRAFÍA 2026/LIDIA Y DANI/FOTOS/A7408883.ARW'

---

### 🤖 Claude

El usuario necesita ordenar fotos RAW de Sony por fecha de captura y renombrarlas secuencialmente, pero su programa actual no soporta el formato .ARW. Aunque no puedo acceder directamente a su disco LaCie, puedo proporcionarle un script que automatice esta tarea.

Voy a crear un script que lea la fecha EXIF de cada archivo .ARW usando la librería `exifread`, ordene los archivos cronológicamente, y luego los renombre a L&D_0001, L&D_0002, etc. Necesito considerar que el renombrado debe hacerse de forma segura para evitar colisiones de nombres durante el proceso. I'm weighing whether to use `exifread` via pip or leverage macOS's native `mdls` command for reading .ARW metadata. `exifread` is more portable and robust, while `mdls` requires no installation but has fragile output parsing. I'll go with `exifread` to keep the script straightforward and reliable.

The script needs a preview mode by default to show what would happen, ask for confirmation, handle files without EXIF data by falling back to file modification time, and use a two-phase rename strategy to avoid collisions. I'll parametrize the prefix as "L&D" for Lidia and Dani, and since this is a utility script over 20 lines, I'll create it as a file rather than paste it inline. I'm responding in Spanish since the user is writing in Spanish.

Writing the Python script... I'm setting up a function to extract the capture date from image EXIF data, falling back to the file's modification timestamp if that's not available, and then defining a sorting key function that's being cut off mid-definition.

I see the issue now—mixing EXIF date strings with file modification timestamps as floats in the same tuple breaks the sorting since they're different types. The EXIF format "YYYY:MM:DD HH:MM:SS" sorts lexicographically in the same order as chronologically, which is convenient, but combining it with a float timestamp won't work properly. I need to normalize everything to a consistent format.

Converting both to datetime objects...

Devuelvo una tupla con el datetime y un booleano indicando si proviene de EXIF, para poder reportar cuáles usaron fallback.

Para el renombrado, uso un enfoque en dos fases: primero renombro todo a nombres temporales únicos con un prefijo, luego los renombro a sus nombres finales. Esto previene colisiones entre archivos que aún se están procesando. Aunque en este caso los nombres origen y destino no deberían colisionar, hacerlo así lo hace más robusto y reutilizable.

Preservo la extensión original tal como viene (Sony usa .ARW en mayúsculas), sin normalizarla para no sorprender al usuario. El script tendrá un modo preview que muestra las primeras N operaciones y pide confirmación antes de proceder, y lo haré ejecutable directamente en su Mac.

El error original viene de que el programa de renombrado (probablemente "A Better Finder Rename" o similar) no tiene plugin para leer EXIF de archivos RAW, por eso el mensaje "No plugin available to handle". Le explico la causa y le doy la solución con Python. Voy a crear el script completo, lo pondré en outputs y le presento todo en español. También le paso el comando para instalar exifread con pip3, que debería estar disponible en su Mac.El error es claro: el programa que usas (un renombrador tipo Finder Rename) intenta leer los metadatos EXIF del `.ARW` para ordenar por fecha, pero **no tiene plugin/lector para el RAW de Sony**, así que falla en el primer archivo y revierte todo.

La solución más robusta es un script propio que lea el EXIF del RAW directamente. Te lo dejo listo.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Cómo usarlo en el Mac:

```bash
pip3 install exifread
python3 ~/Downloads/renombrar_fotos.py
```

Qué hace y por qué no falla con los `.ARW`:

`exifread` lee el bloque EXIF del RAW de Sony directamente (no necesita "revelar" el archivo ni plugins externos), saca el `DateTimeOriginal`, ordena todo cronológicamente y renombra a `L&D_0001.ARW`, `L&D_0002.ARW`, etc. Antes de tocar nada te muestra una vista previa y pide confirmación escribiendo `si`.

Tres detalles pensados a propósito:

El renombrado va en **dos fases** (primero a nombres temporales, luego a los finales) para que nunca un `L&D_0005` pise un archivo aún sin procesar. Si alguna foto no tuviera EXIF legible, en vez de cancelar todo como tu programa, usa la fecha de modificación del archivo como respaldo y te avisa de cuántas fueron. Y el prefijo, el relleno de ceros y la carpeta están arriba del todo en `CONFIGURACION`, así lo reutilizas para la próxima boda cambiando solo dos líneas.

Una nota: el `&` en `L&D_` es válido en nombres de archivo de macOS, pero si luego mueves esas fotos por terminal recuerda que el `&` hay que escaparlo o entrecomillar la ruta. En Finder y en la mayoría de programas no te dará problema.

¿La carpeta tiene los `.ARW` directamente dentro o hay subcarpetas? El script mira solo el primer nivel; si necesitas que entre en subcarpetas lo ajusto.

---

### 🧑 Juanfra

hay subcarpetas, esto me lo puede hacer automaticamnente cowork?

---

### 🤖 Claude

El usuario está preguntando dos cosas: si hay subcarpetas involucradas y si Cowork puede automatizar este proceso de renombrado. Cowork es la aplicación de escritorio para trabajo de conocimiento agéntico que puede acceder a herramientas del Mac, navegador y carpetas del usuario, así que teóricamente podría trabajar con el disco LaCie, aunque necesito verificar exactamente cómo maneja el acceso a unidades externas.

Lo más importante es que si hay subcarpetas, necesito aclarar con el usuario cómo quiere que se numeren: ¿una secuencia continua global ordenada por fecha a través de todas las carpetas, o renumeración independiente dentro de cada subcarpeta? Para una boda, lo más probable es que prefiera una secuencia única y continua.

Voy a responder directamente ajustando el script para que sea recursivo, preguntarle sobre esa decisión de numeración que es clave, y recomendarle Cowork como la herramienta ideal para ejecutar esto automáticamente en su Mac sobre sus archivos locales. Hay un riesgo real de colisión si tengo subcarpetas con fotos: necesito decidir si renumero todo globalmente pero dejo los archivos en sus subcarpetas originales, si los muevo todos a la carpeta raíz con numeración continua, o si renumero independientemente dentro de cada subcarpeta. Para una boda, lo más útil sería tener todas las fotos en un flujo cronológico único, así que probablemente la opción B (todo junto, secuencia continua) o A sean las más razonables. Esto justifica preguntar al usuario porque hay varias opciones válidas y el resultado es destructivo.

Además, debería recomendar Cowork directamente ya que es exactamente lo que necesita para automatizar esto en su Mac. Estoy considerando si puedo llamar a ambas funciones en el mismo turno — recommend_claude_apps para mostrar Cowork y ask_user_input para la pregunta sobre las subcarpetas. Creo que pueden coexistir en la respuesta, así que voy a estructurar el mensaje con texto breve, la recomendación de la app, y luego los botones de la pregunta. Pero ahora me pregunto si realmente necesito preguntar al usuario o si hay otras formas de manejar las opciones de organización.

Pensándolo mejor, la pregunta clave es cómo quiere el resultado final: si todo junto en una secuencia continua, si mantener cada foto en su subcarpeta original, o si numerar cada subcarpeta por separado. Son tres opciones claras y mutuamente excluyentes, perfectas para ask_user_input.Sí. Esto es justo el tipo de tarea para **Cowork**: le pasas la carpeta y ejecuta el renombrado directamente sobre tu LaCie, sin que tengas que tocar la terminal ni instalar nada a mano. Yo desde este chat no puedo acceder a tu disco, pero Cowork trabaja sobre tus propias carpetas y archivos en el Mac.
```
This block is not supported on your current device yet.
```

Antes de lanzarlo (con Cowork o con el script), hay una decisión que cambia el resultado y que conviene fijar, porque al haber subcarpetas el renombrado masivo es difícil de deshacer:
```
This block is not supported on your current device yet.
```



---
