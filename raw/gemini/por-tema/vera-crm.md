---
title: "Vera CRM — extracto de Gemini"
tags:
  - clippings
  - gemini
---

# Vera CRM

*Extracto agrupado automáticamente (por palabras clave) de `raw/gemini/consultas-generales-gemini.md`. Orden cronológico original conservado; cada bloque indica su rango de líneas en el archivo fuente para poder verificarlo.*

<!-- líneas 10344-10380 del original -->

¡Perfecto! Este es el momento ideal para darle a Claude Code unas instrucciones claras y maestras. He preparado un brief completo dividido en fases estratégicas.
El objetivo de este prompt es que Claude entienda exactamente en qué punto está el proyecto, proteja tus datos actuales como prioridad absoluta y comience la migración técnica paso a paso sin que el diseño de Vera sufra ningún cambio.
Solo tienes que copiar el texto que está entre las líneas y pegarlo directamente en Claude Code:
CONTEXTO DEL PROYECTO: VERA CRM
Actúa como un Desarrollador Full-Stack experto en React, Vite y arquitecturas de software modernas.
Estamos construyendo "Vera", un CRM de primer nivel diseñado exclusivamente para fotógrafos de boda. Actualmente, el proyecto está en una fase MVP avanzada: la interfaz visual está muy pulida (usando un sistema de diseño propio basado en CSS puro con variables oklch), la lógica funciona y ya estoy gestionando clientes reales en la aplicación.
Actualmente el proyecto está estructurado de forma monolítica (un archivo o estructura básica con scripts cargados por CDN). El objetivo ahora es migrar a una arquitectura profesional, escalable y modular para poder implementar funciones avanzadas en el futuro (como un creador de formularios integrado y una pantalla de configuración centralizada), pero sin perder absolutamente nada de información.
Quiero que ejecutes este plan de acción paso a paso, pidiéndome confirmación antes de avanzar a la siguiente fase:
FASE 1: Seguridad y Backup de Datos (CRÍTICO)
Antes de tocar la arquitectura, necesitamos asegurar los datos de mis clientes reales.
	•	Haz una auditoría inmediata del código actual e identifícame cómo y dónde se están guardando los datos actualmente (¿localStorage, IndexedDB, archivos locales, base de datos externa?).
Escribe un script o dame las instrucciones exactas para hacer un backup/exportación completa de todos estos datos a un archivo seguro (ej. un JSON local) para tener un respaldo antes de migrar.
	•	-> Detente aquí y espera mi confirmación de que el backup está hecho antes de seguir.
FASE 2: Inicialización del Entorno Profesional
Una vez asegurados los datos, vamos a modernizar el motor de la app:
	•	Inicializa un nuevo entorno utilizando Vite + React.
	•	Elimina las dependencias externas por CDN (como React, ReactDOM, jsPDF, qrcode-generator) e instálalas nativamente vía npm o yarn.
	•	Configura la estructura de carpetas estándar (/src/components, /src/styles, /src/pages, /src/utils).
FASE 3: Refactorización del Sistema de Diseño (CSS)
El diseño actual de Vera es intocable, es nuestra mayor fortaleza.
	•	Extrae todo el bloque de <style> que contiene nuestro sistema de diseño (variables :root, colores oklch, utilidades y clases semánticas).
	•	Llévalo a un archivo global (ej. index.css o global.css) y asegúrate de que las fuentes de Google (Instrument Sans, Instrument Serif, JetBrains Mono, Dancing Script) se carguen de manera óptima en la nueva arquitectura.
FASE 4: Componentización
Divide el archivo monolítico actual en componentes lógicos y reutilizables de React, manteniendo la estructura de clases intacta para que no se rompa el diseño. Necesitaremos al menos:
	•	Layout principal (Sidebar, Topbar).
	•	Dashboard (KPIs, widgets de tarjetas).
	•	Pipeline / Kanban (Tarjetas drag & drop).
	•	Calendario y Tareas.
	•	Inbox (Mensajería).
	•	Módulo de Facturación y Finanzas.
	•	Contratos y Firmas (integrando jsPDF).
REGLAS DURANTE LA EJECUCIÓN
	•	No modifiques los nombres de las clases CSS ni la paleta de colores. El diseño debe verse 100% idéntico al actual tras la migración.
	•	Mantén la lógica de guardado actual conectada en los nuevos componentes para que, al arrancar el nuevo entorno Vite, la app siga leyendo los datos de mis clientes reales (o del backup que hemos creado).
	•	Ve paso a paso. No me lances cientos de archivos de golpe. Guíame en el proceso de migración archivo por archivo o fase por fase.
Con esto, Claude Code tendrá un mapa de ruta perfecto y sabrá que no debe borrar nada antes de asegurarse.
Una vez que le pases este brief y finalicéis la migración del código base, ¿te gustaría que preparemos el prompt exacto para empezar a construir el "Creador de Formularios" integrado?

---

<!-- líneas 13650-13655 del original -->

pasta cocida en la never desde hace 4 días se puede comer?
Sí, en principio puedes comerla sin problema. El tiempo máximo recomendado para conservar la pasta cocida en la nevera es de 3 a 5 días, por lo que estás dentro del límite seguro.
Antes de calentarla, hazle una prueba rápida:
	•	Textura: Si notas que está babosa o excesivamente pegajosa, tírala.
	•	Olor: Si tiene un olor ácido o extraño, no te la juegues.
Si se ve y huele como siempre, y ha estado guardada en un recipiente bien cerrado, asegúrate de calentarla a fondo (mejor si es a más de 70ºC) para eliminar cualquier posible bacteria y lista para comer.

---

<!-- líneas 14489-14501 del original -->

dentro de ese nodo se habla mucho de vera que está en otros nodos
Ese es exactamente el "problema". En programas como Obsidian, escribir una palabra de forma normal (en texto plano) no crea ninguna conexión en el gráfico, por muchas veces que la repitas a lo largo del texto.
El programa es ciego al texto normal para evitar que el gráfico se convierta en un caos de líneas inútiles conectando preposiciones o palabras comunes. Para que el sistema reconozca la relación y dibuje la línea que conecte a CLAUDE con el resto, tienes que decirle explícitamente que "Vera" es un concepto clave.
Tienes dos formas de solucionarlo:
Opción 1: Hacerlo a mano (La más rápida)
Solo tienes que entrar en la nota de CLAUDE, buscar una de las veces donde pone "Vera" y ponerle los dobles corchetes alrededor para convertirlo en un enlace. Es decir, cambiarlo a [[Vera]]. Con que lo hagas una sola vez en todo el texto, el nodo de CLAUDE se conectará inmediatamente al nodo de Vera.
Opción 2: Usar la herramienta del programa (Ideal si tienes muchos)
Obsidian tiene una función inteligente para detectar esto que te está pasando:
	•	Abre la nota de CLAUDE.
	•	Abre el panel lateral derecho y ve a la pestaña de Menciones (el icono de unos enlaces o flechas).
	•	Busca la sección que dice "Menciones no enlazadas" (Unlinked mentions).
	•	El programa te mostrará una lista con todas las veces que has escrito la palabra "Vera" en el texto sin ponerle corchetes. Al lado de cada una, verás un botón que dice "Enlazar". Si lo pulsas, el programa le pone los corchetes por ti automáticamente.
En cuanto conviertas uno de esos textos planos en un enlace [[Vera]], verás que el punto gris de CLAUDE dejará de flotar solo y se enganchará a la red principal de tu gráfico.

---

