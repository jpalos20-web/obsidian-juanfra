---
title: "Portal Novios"
uuid: 1686c594-1f2e-4927-9d8f-815de9189e67
fecha: 2026-06-04
fuente: design_chats (Claude Design)
tags:
  - transcripcion
  - design-chat
---

# Portal Novios

*Conversación de Claude Design completa, 2026-06-04. Sin resumir; las llamadas a herramientas de escritura de código se anotan por nombre, no se incluye el código generado completo.*

---

### 🤖 Claude

<system-info comment="Only acknowledge these if relevant">
Project title is now "Portal Novios"
Project is currently empty (no files)
Current date is now June 4, 2026
</system-info>

<pasted_text name="Pasted text (53 lines)">
PRIORIDAD ABSOLUTA: mobile-first. El portal debe verse y funcionar perfecto en móvil ANTES que en escritorio. Si algo no se ve impecable a 360–390px de ancho, no vale.

Crea un "Portal de Novios" para Vera, un CRM para fotógrafos y videógrafos de boda: la página privada que el fotógrafo comparte con la pareja. Metáfora visual: un TABLÓN DE CORCHO tipo moodboard de boda, RICO Y TÁCTIL, dentro de una ESCENA de habitación cálida. Cada sección es un objeto distinto pinchado en el corcho.

== CONCEPTO VISUAL / ESCENA ==
- Pared en verde salvia suave (#C9D4CC) con luz de tarde. Tablón de corcho grande con marco de madera clara (biseles y veta) y una GUIRNALDA DE LUCES cálidas bordeando el marco (brillo suave, lento).
- ENTORNO: en la franja inferior, el canto de una mesa de madera con un libro abierto, una libreta cerrada, un par de fotos sueltas y una manta de punto desenfocada al fondo — estilo foto lifestyle, con profundidad y ambiente.
- Corcho muy "scrapbook": objetos variados y ligeramente SOLAPADOS — polaroids, post-its pastel, calendario de espiral metálica, tickets/entradas, sellos, un par de ramitas de eucalipto/flores secas, clips, washi tape de colores. Textura de corcho granulada, papel con fibra, madera con veta.
- Cada objeto rotado (±5°), con SOMBRA de relieve real y sujeto con CHINCHETA de colores vivos (rojo, azul, amarillo, verde, turquesa) — círculo con brillo + sombra clavado arriba.
- Cálido y abundante, pero elegante: la tipografía editorial lo mantiene refinado.

== MARCA VERA ==
- Titulares/nombres en "Instrument Serif"; cuerpo en "Instrument Sans". Notas manuscritas (post-its) en "Caveat".
- Paleta base: tinta cálida #1C1813, papel marfil #F4EEE2, acento terracota #B0573C; las chinchetas/washi aportan el color.
- Filigrana "vera." grabada en una esquina del marco. Rótulo superior en serif: "Portal de Novios".

== SECCIONES (cada una = un objeto físico) ==
1. POLAROID GRANDE (héroe, central): foto de la pareja; bajo la imagen, a mano, nombres + fecha. Debajo, en serif, CUENTA ATRÁS en vivo ("Faltan 245 días"). Chincheta roja.
2. POST-IT DE BIENVENIDA: mensaje manuscrito del fotógrafo. Sujeto con washi tape.
3. CALENDARIO DE PARED (espiral arriba): mes de la boda con el día rodeado a mano en rojo + 2-3 próximos hitos.
4. TICKET "CONTRATO PARA FIRMAR": CTA principal → abre la firma; su chincheta LATE suavemente. Si está firmado, sello "FIRMADO".
5. TARJETA "VUESTRO PAQUETE": qué incluye + importe + barra de estado de pago.
6. POST-IT CHECKLIST: tareas pendientes con casillas.
7. TIRA DE POLAROIDS "MOMENTOS": 3-4 miniaturas solapadas + enlace a la galería.
8. TARJETA "HABLEMOS": contacto con el fotógrafo (WhatsApp / email).
(Esenciales: 1, 4, 5. El resto, deseables.)

== INTERACCIONES ==
- Hover (solo escritorio): el objeto se levanta, la sombra crece y se endereza un poco.
- Cuenta atrás en vivo. Chincheta del contrato con pulse. Luces de la guirnalda con brillo leve y lento. Ligero parallax del entorno al hacer scroll (sutil).

== MÓVIL PRIMERO (regla que manda sobre todo lo demás) ==
- Diseña y resuelve la vista móvil ANTES que la de escritorio. El escritorio es la mejora, no al revés.
- En móvil NO hay tablón disperso. El corcho, su marco y las luces siguen de fondo, pero los objetos se apilan en UNA SOLA COLUMNA vertical scrollable, a todo el ancho con márgenes cómodos. Cero posiciones absolutas que se solapen o se salgan de pantalla.
- Cada objeto conserva su identidad táctil: polaroid/post-it/ticket, su chincheta o washi arriba, y rotación reducida (máx ±2°; el héroe a 0°).
- Orden en móvil (arriba → abajo): 1 Héroe → 4 Contrato → 5 Paquete → 3 Calendario → 6 Checklist → 7 Momentos → 2 Bienvenida → 8 Hablemos.
- Táctil: botones de mínimo 44px de alto, cuerpo de texto ≥16px, titulares serif bien legibles. Nada diminuto ni objetivos de toque pequeños.
- Sin hover en móvil: todo es tap, con estados :active claros.
- El marco de madera adelgaza en móvil para no robar ancho; el corcho llena el fondo sin recortar objetos.
- Breakpoints: columna apilada por defecto; el tablón disperso solo a partir de ~900px. Comprueba 360px, 390px y 768px.
- Nunca scroll horizontal. En pantallas pequeñas reduce o desactiva las luces animadas y el parallax para que el scroll sea fluido.
- Compatible con PWA / pantalla completa en iOS: viewport con viewport-fit=cover y respeta los safe-area-inset.

== TÉCNICO ==
- Un único HTML autocontenido, sin build, JS vanilla, desplegable en Netlify.
- Fuentes vía Google Fonts (Instrument Serif, Instrument Sans, Caveat).
- TODOS los datos salen de un objeto al inicio del <script>:
  const PORTAL = { novios:"Sara & Miguel", fecha:"14 jun 2026", lugar:"Sevilla", paquete:"Premium", importe:"3.200 €", diasRestantes:245, firmado:false };
  Úsalo por defecto; lo conectaré luego a la API de Vera.
- Texturas (corcho, madera, papel, luces) con CSS/SVG/gradientes, sin imágenes externas pesadas. Placeholders para las fotos.

== EVITA ==
Que parezca infantil o de manualidades baratas, sombras duras, degradados morados, plantilla genérica. Busca cálido, hecho a mano y a la vez de boda de autor.
</pasted_text>

<!-- The user explicitly selected the following skills for this project, as attachments to their message. These are not optional context — they define how you work. Use them. -->
<attached-skill name="Hi-fi design">
Create a high-fidelity, polished design.

Follow this general design process (use the todo list to remember):
(1) ask questions, (2) find existing UI kits and collect design context — copy ALL relevant components and read ALL relevant examples; ask the user if you can't find them, (3) start your file with assumptions + context + design reasoning (as if you are a junior designer and the user is your manager), with placeholders for the designs, and show it to the user early, (4) build out the designs and show the user again ASAP; append some next steps, (5) use your tools to check, verify and iterate on the design.

Good hi-fi designs do not start from scratch — they are rooted in existing design context. Ask the user to Import their codebase, or find a suitable UI kit / design resources, or ask for screenshots of existing UI. You MUST spend time trying to acquire design context, including components. If you cannot find them, ask the user for them. In the Import menu, they can link a local codebase, provide screenshots or Figma links; they can also link another project. Mocking a full product from scratch is a LAST RESORT and will lead to poor design. If stuck, try listing design assets and ls'ing design system files — be proactive! Some designs may need multiple design systems — get them all. Use the starter components (device frames and the like) to get high-quality scaffolding for free.

When presenting several options or explorations side-by-side, lay them out clearly: give the page a neutral gray background, put each option in its own labeled frame (a small heading + a white rounded card sized to its content), and group related options into sections.

When designing, asking many good questions is ESSENTIAL.

Give options: try to give 3+ variations across several dimensions. Mix by-the-book designs that match existing patterns with new and novel interactions, including interesting layouts, metaphors, and visual styles. Have some options that use color or advanced CSS; some with iconography and some without. Start your variations basic and get more advanced and creative as you go! Try remixing the brand assets and visual DNA in interesting ways — play with scale, fills, texture, visual rhythm, layering, novel layouts, type treatments. The goal is not the perfect option; it's exploring atomic variations the user can mix and match.

CSS, HTML, JS and SVG are amazing. Users often don't know what they can do. Surprise the user.

If you do not have an icon, asset or component, draw a placeholder: in hi-fi design, a placeholder is better than a bad attempt at the real thing.
</attached-skill>

<attached-skill name="Interactive prototype">
Create a fully interactive prototype with realistic state management and transitions. Use React useState/useEffect for dynamic behavior. Include hover states, click interactions, form validation, animated transitions, and multi-step navigation flows. It should feel like a real working app, not a static mockup.
</attached-skill>

<attached-skill name="Design System (design system)">
[Design System] This project uses the **Design System** design system. This is a binding choice for visual style — every visual must follow it. Don't invent colors, type, spacing, or components not grounded here.

Scope: the design system is a visual style reference only. Its guide may describe example products, brands, or people that are unrelated to the user and unrelated to the subject of this conversation. Never treat anything in the design system as a fact about the user, their work, or the topic they asked about.

    Explore it to find what you need:
    - Always copy out the fonts and colors you need
    - For prototypes and designs, always copy out any relevant components
    - If the design system contains existing mocks of products, and you were asked to design or prototype something similar, copy and fork those mocks to start your design. This helps you make high-quality designs.

    Explore it quickly to find relevant UI kits (e.g. mocks of existing products you can copy and fork)

Full system at `/projects/e6731c4b-a712-472f-beca-769e6d598409/`. Before producing any visuals, explore it: call `list_files("/projects/e6731c4b-a712-472f-beca-769e6d598409/")` to see the structure, then `read_file` the README/base.md or whatever index file it has. Don't guess at the design system's contents.

CSS tokens: the guide may describe tokens in prose, but the exact `--*` names are defined in the design system's stylesheet(s). Before writing any `var(--*)`, look up the real name in the design system's `.css` files (`list_files` + `read_file` under `/projects/e6731c4b-a712-472f-beca-769e6d598409/`). Never guess a token name — an unresolved `var()` silently falls back to the browser default.

For assets and UI kits beyond the guide: `read_file("/projects/e6731c4b-a712-472f-beca-769e6d598409/<path>")` and `copy_files` to bring them into the current project.
</attached-skill>




---

### 🤖 Claude

The design system is empty, so there's no existing context to pull from — I'll work entirely from your spec, which is exhaustively detailed (palette, fonts, sections, mobile order, data object, constraints). That's enough to build directly without a questions round.

Let me set up my plan and build.Now I'll build the portal. This is craft-heavy, so I'll write it carefully — mobile-first column as the foundation, desktop scatter as enhancement.

The design system is empty, so there's no existing context to pull from — I'll work entirely from your spec, which is exhaustively detailed (palette, fonts, sections, mobile order, data object, constraints). That's enough to build directly without a questions round.

Let me set up my plan and build.

Now I'll build the portal. This is craft-heavy, so I'll write it carefully — mobile-first column as the foundation, desktop scatter as enhancement.

> *[herramienta: `list_files`]*

> *[herramienta: `update_todos`]*

> *[herramienta: `write_file`]*

---
