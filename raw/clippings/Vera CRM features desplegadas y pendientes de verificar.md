---
title: "Vera CRM: features desplegadas y pendientes de verificar"
source: "https://claude.ai/chat/8c58d2bf-f471-4932-90ec-67e8922af1d4"
author:
published: 2026-07-28
created: 2026-09-15
description: "Claude conversation with 9 messages"
tags:
  - "clippings"
---
**Claude**

Sí, y de hecho es exactamente la funcionalidad que construimos en la Fase 1 del motor de formularios — solo que aplicada a un caso nuevo. Lo que muestra esa captura es lógica condicional más interpolación de respuestas previas, y el motor de Vera ya sabe hacer las dos cosas. Te lo separo:

**"Arrastrar los nombres a preguntas siguientes"** (que la etiqueta de una pregunta diga "Nombres de los padres de **Elena** " usando lo que la pareja escribió antes) — esto es interpolar una respuesta anterior dentro del texto de otra pregunta. El motor tiene el mecanismo de variables; habría que confirmar que soporta usar una **respuesta del propio formulario** como variable dentro de otra etiqueta, no solo variables de la boda como `{{pareja}}`. Eso es lo único que tendría que verificar Claude Code.

**Mostrar/ocultar preguntas según una respuesta** — esto sí lo tienes seguro, es el `showIf` que construimos y probamos en la Fase 1. Ya funciona.

Así que la respuesta corta es: **sí, es justo para lo que se diseñó ese motor.** Y hay un matiz que te da una ventaja sobre lo que sugiere esa captura: fíjate que el texto habla de "herramientas digitales avanzadas" y termina preguntándote qué plataforma externa vas a usar (Typeform, Google Forms, un PDF...). Tú ya no necesitas ninguna de esas — el motor que tienes dentro de Vera hace esto de forma nativa, con tu estética, con el enlace tokenizado por boda, y con las respuestas guardadas en la ficha. No tienes que salir a Typeform ni a Google Forms para nada.

Lo único que no puedo confirmarte al 100% sin mirar el código es el primer punto (usar una respuesta previa como variable en la etiqueta de otra pregunta). ¿Quieres que te prepare un mini-brief para que Claude Code verifique si eso ya funciona tal cual, o si le falta esa pieza concreta — y si le falta, que la añada? Es pequeño, y de paso te dejaría el motor listo para montar exactamente el formulario de esa captura sin herramientas externas.

---

**You**

yo lo que quiero hacer es al crear el formulario, para no tener que poner novio, novia (me puede llegar una pareja LGTBI) pues poder preguntar y que coja los nombres

---

**Claude**

Entendido perfectamente, y es una razón de peso — no es solo elegancia técnica, es no dar por sentado que toda pareja es "novio y novia", que en tu sector importa de verdad. Lo que quieres es que el formulario pregunte los dos nombres al principio y luego los reutilice tal cual la pareja los haya escrito, sin que tú tengas que asumir géneros ni roles.

Esto es exactamente el primer punto que te comentaba: usar una **respuesta previa del propio formulario** como variable dentro de una pregunta posterior. Y aquí hay un matiz importante que conviene que sepas antes de mandar nada: el formulario de música que ya tienes hace algo parecido, pero **al revés** — coge los nombres desde los datos de la boda (`{{pareja}}`) porque tú ya los sabes. Lo que pides ahora es distinto: que los nombres los ponga **la propia pareja al rellenar**, y que a partir de ahí el formulario los use en las siguientes preguntas. Eso puede que el motor no lo haga todavía, porque nunca lo hemos necesitado — hasta ahora las variables salían de datos que Vera ya conocía, no de respuestas que el cliente acaba de escribir en ese mismo formulario.

Por eso el brief empieza por verificar si esa pieza existe, y solo la construye si falta:

---

**You**

no se están gguardando las nuevas automatizaciones

---

**Claude**

Vamos a diagnosticarlo con el mismo método de siempre, porque "no se guardan" puede ser varias cosas distintas y conviene acotar antes de mandar nada.

Primero, precisa qué estás creando exactamente, porque ahora mismo hay varios "+ Nueva..." en la pantalla de Automatizaciones:

---

**You**

cuano cre un formulario nuevo no se guarda

---

**Claude**

Esto es justo el mismo tipo de bug que ya cazamos una vez en la Fase 3 (formularios que no guardaban nombre ni preguntas) — y sospecho que ha vuelto por la refactorización grande de ayer, cuando se fusionaron Emails, Formularios y Automatizaciones en una sola pantalla. Ese cambio tocó justo el flujo de "crear formulario nuevo" y cómo se abre su editor (ahora el botón Editar abre `CustomFormEditor` dentro de la pantalla unificada, con un "← Volver a Automatizaciones"), así que es un candidato muy probable a haber roto algo en el camino de guardado sin que nadie lo notara, porque el foco de esa verificación fue el motor de reglas, no la creación de formularios en sí.

Antes de mandar el brief, una comprobación rápida que te ahorra vueltas si puedes hacerla: cuando pulses "Guardar" en el formulario nuevo, abre la consola del navegador (F12 → Network) y mira si sale una petición y qué código de estado devuelve. Si no puedes mirarlo ahora, no pasa nada — se lo pido directamente a Claude Code con la pista fuerte de por dónde mirar.

---

**You**

si iniciamos chat nuevo, tienes memoria de lo que hemos habladdo en este?

---

**Claude**

Sí, hasta cierto punto, pero conviene que sepas exactamente cómo funciona para que no te lleves una sorpresa.

Tengo un sistema de memoria que, entre conversación y conversación, va guardando un resumen de lo que hemos hecho — en tu caso, todo este proyecto de Vera: el pipeline configurable, el motor de formularios, las automatizaciones, los bugs que hemos ido cazando, etc. Cuando abras un chat nuevo, ese resumen estará disponible y podré aplicarlo de forma natural, sin que tengas que volver a explicarme quién eres ni en qué estamos.

Pero hay dos matices importantes:

**No es la conversación completa palabra por palabra** — es un resumen derivado, así que puede que se pierdan detalles muy finos (un número exacto, una frase concreta de un reporte). Si necesito algo muy específico de esta conversación, tengo una herramienta para buscar en el historial de chats pasados, así que puedo ir a buscarlo si hace falta en vez de depender solo de lo que recuerde de memoria.

**Se actualiza con cierto retraso** — si abres el chat nuevo justo después de este, es posible que lo más reciente (como este mismo mensaje sobre el bug de los formularios que no se guardan) todavía no esté reflejado en la memoria. Si eso pasa, simplemente recuérdamelo tú al empezar y seguimos sin perder nada.

Así que en la práctica: puedes abrir un chat nuevo con tranquilidad, decir algo como "seguimos con Vera" y lo más probable es que ya tenga el contexto — pero si notas que algo muy reciente no lo tengo, dímelo y lo recupero o lo retomamos sin problema.