---
title: "Renombrar fotos por hora de captura"
source: "https://claude.ai/chat/45b60986-fa5d-405e-b486-0446023406e3"
author:
published: 2026-06-23
created: 2026-09-15
description: "Claude conversation with 4 messages"
tags:
  - "clippings"
---
**You**

puedes ordenarme por hora de captura y renombrarme todos los archivos de una carpeta de fotos a L&D\_0001 y así sucesivamente?  
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

**Claude**

El error es claro: el programa que usas (un renombrador tipo Finder Rename) intenta leer los metadatos EXIF del `.ARW` para ordenar por fecha, pero **no tiene plugin/lector para el RAW de Sony**, así que falla en el primer archivo y revierte todo.

La solución más robusta es un script propio que lea el EXIF del RAW directamente. Te lo dejo listo.

---

**You**

hay subcarpetas, esto me lo puede hacer automaticamnente cowork?

---

**Claude**

Sí. Esto es justo el tipo de tarea para **Cowork**: le pasas la carpeta y ejecuta el renombrado directamente sobre tu LaCie, sin que tengas que tocar la terminal ni instalar nada a mano. Yo desde este chat no puedo acceder a tu disco, pero Cowork trabaja sobre tus propias carpetas y archivos en el Mac.