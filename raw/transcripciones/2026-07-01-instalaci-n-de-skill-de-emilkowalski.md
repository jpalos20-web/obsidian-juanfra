---
title: "Instalación de skill de emilkowalski"
uuid: 378c7db9-07e1-42e0-acbe-bba57a825fab
fecha: 2026-07-01
fuente: conversations.json
tags:
  - transcripcion
---

# Instalación de skill de emilkowalski

*Conversación completa, 2026-07-01. Exportada de Claude.ai, sin resumir.*

---

### 🧑 Juanfra

como instalo la skill de emilkowalski

---

### 🤖 Claude

I'm not sure what "the emilkowalski skill" refers to—it could be related to the design and animation work emilkowalski is known for, possibly something in Claude's skills ecosystem. Let me search for more context about this.
```
This block is not supported on your current device yet.
```

Es un skill de terceros (de Emil Kowalski, creador de Sonner y del curso animations.dev) que aplica su filosofía de animaciones/microinteracciones a Claude Code. No es un skill oficial de Anthropic, así que se instala vía el paquete `skills` de npx, no desde `/mnt/skills`.

**Pasos:**

1. Abre una terminal en el proyecto donde uses Claude Code (por ejemplo, en Vera CRM).
2. Ejecuta:

```bash
npx -y skills add emilkowalski/skill --skill emil-design-eng --agent claude-code
```

Esto lo instala en `.claude/skills/` del proyecto actual (no es global, así que si lo quieres en otro repo tendrás que repetirlo ahí).

3. Verifica que se instaló bien dentro de Claude Code escribiendo:

```
/skills
```

Debería aparecer `emil-design-eng` en la lista.

4. No hace falta invocarlo a mano — una vez instalado, Claude Code lo activa automáticamente cuando trabajas en animaciones, transiciones, hover states, modales, etc. Trae reglas concretas tipo: animaciones de UI bajo 300ms, usar curvas de easing custom en vez de las de CSS por defecto, evitar `ease-in` para elementos que entran, no animar acciones de alta frecuencia, etc.

Como para ti tiene sentido en el contexto de Vera CRM (React 18), esto podría venirte bien para pulir transiciones del dashboard o del cuestionario público sin tener que pensarlo tú mismo cada vez.

---

### 🧑 Juanfra

como lo utilizo para mejorar vera?

---

### 🤖 Claude

Now I'm thinking through how to apply this in a real Vera CRM setup with a React 18 and esbuild frontend—what the actual workflow would look like and what kinds of prompts would be most useful in that context.Una vez instalado en el repo de Vera (`/Users/alba/VERA`), no necesitas invocarlo explícitamente — Claude Code lo detecta solo cuando la tarea toca animaciones o interacción UI. Pero para sacarle partido de verdad, conviene guiarlo un poco. Así es como lo usarías en la práctica:

**1. Instálalo en el repo correcto**

```bash
cd /Users/alba/VERA
npx -y skills add emilkowalski/skill --skill emil-design-eng --agent claude-code
```

**2. Pídele auditorías de componentes concretos**, no "mejora la app" en genérico. Por ejemplo, sobre partes de Vera que ya tienes construidas:

- El modal/dossier de gating para el cuestionario público (`/q/:token`)
- Las transiciones del pipeline de estados (donde tienes el bug del stage count)
- El flujo de contratación / firma de contrato
- Los toasts/notificaciones (aquí encaja especialmente bien porque Emil es el autor de Sonner)

Prompt tipo:
```
Revisa las animaciones del modal de contratación en src/components/ContractModal.jsx 
usando el skill de Emil Kowalski. Dame la tabla antes/después.
```

**3. Aprovecha que el skill da tablas antes/después.** Le pides que audite un componente y te devuelve reglas concretas aplicadas: duración, easing, qué anima y qué no. Es fácil de revisar antes de aceptar cambios.

**4. Casos donde más rinde en Vera concretamente:**
- **Onboarding de fotógrafos beta** (7 usuarios ahora) — primeras impresiones importan, y el skill es bueno puliendo micro-interacciones de "sensación de calidad"
- **Cuestionario público con token** — es lo que ven tus clientes finales (como Alisha y Alex), así que cualquier torpeza de animación ahí se nota
- **Dashboard principal** — si usas transiciones al cambiar de pipeline stage o al abrir/cerrar paneles

**5. No es sustituto de arreglar bugs funcionales.** El bug del pipeline stage count, por ejemplo, es lógica de backend/estado, no algo que este skill toque — sigue siendo tarea normal de Claude Code.

Si quieres, puedo ayudarte a redactar el primer prompt de auditoría apuntando a un componente específico de Vera que ya tengas hecho.

---

### 🧑 Juanfra

lo puedes instalar tu?

---

### 🤖 Claude

The user is asking me to install something, but I'm realizing there's a fundamental limitation here — my bash tool runs in a sandboxed Ubuntu container with restricted network access, not on their local machine. I don't have access to their actual filesystem at /Users/alba/VERA on their Mac, so I can't install anything into their real project directory even though I could theoretically reach npm registry.No puedo instalarlo en tu proyecto real. El terminal al que tengo acceso desde este chat es un contenedor Linux aislado mío, no tu Mac — no tengo acceso a `/Users/alba/VERA` ni a tu repo de Vera.

Lo que sí puedo hacer es confirmarte que el comando funciona y mostrarte exactamente qué instala, para que lo copies y pegues tú en tu terminal:
```
This block is not supported on your current device yet.
```

I should try adding a timeout to the request or query the npm registry directly instead.
```
This block is not supported on your current device yet.
```

The CLI is working as expected—it cloned the repo, displayed the skills list, and I selected one before it hit the interactive installation scope prompt. Now I'll demonstrate this to the user and explain they'll need to run it interactively in their own environment, then clean up the sandbox directory.Confirmado: el comando funciona bien. Clona el repo de Emil Kowalski (`github.com/emilkowalski/skill.git`), encuentra 3 skills disponibles y selecciona `emil-design-eng` como pediste. Después te pregunta el alcance de instalación (local al proyecto o global).

Para que quede en tu repo de Vera, tú tienes que ejecutarlo así:

```bash
cd /Users/alba/VERA
npx -y skills add emilkowalski/skill --skill emil-design-eng --agent claude-code
```

Cuando te pregunte el **scope**, elige **local al proyecto** (no global) para que quede en `.claude/skills/` dentro de Vera y no se mezcle con tus otros proyectos (Nexus Media Lab, etc.).

Después verifica con `/skills` dentro de Claude Code que aparece `emil-design-eng` en la lista, y ya puedes pedirle auditorías de componentes como comentamos (el modal de contratación, el cuestionario público, etc.).

---

### 🤖 Claude

`command not found: npx` significa que Node.js no está instalado (o no está en el PATH) en esa máquina/usuario (`alba@MacBook-Pro-de-Juan-Fra`).

Comprueba primero si tienes Node instalado en absoluto:

```bash
which node
node -v
```

**Si no devuelve nada:** no tienes Node instalado. Instálalo con Homebrew (lo más simple en Mac):

```bash
brew install node
```

Si tampoco tienes Homebrew:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

y luego `brew install node`.

**Si `node -v` sí funciona** pero `npx` no se encuentra, probablemente Node está instalado mediante algo como nvm en otra shell/perfil y esta terminal no lo está cargando. En ese caso dime qué te devuelve `node -v` y `echo $PATH` y lo resolvemos sin reinstalar nada.

Una vez tengas `npx -v` funcionando, repites el comando de instalación del skill tal cual.

---

### 🤖 Claude

Node se instaló correctamente (v26.4.0). Ahora simplemente ejecuta el comando del skill otra vez:

```bash
npx -y skills add emilkowalski/skill --skill emil-design-eng --agent claude-code
```

Cuando te pregunte el **scope de instalación**, elige la opción **local/project** (no global), para que quede dentro de `.claude/skills/` en tu repo de Vera.

Si por lo que sea `npx` sigue sin encontrarse justo después de instalar Homebrew/Node, cierra y vuelve a abrir la terminal (o ejecuta `source ~/.zshrc`) para que cargue el PATH nuevo, y prueba `node -v` de nuevo antes de repetir el comando.

---

### 🤖 Claude

The agent name got corrupted during input—"claude-code" and "npx" merged together without proper spacing, likely from a copy-paste error that combined two separate commands into one malformed argument.El problema es que el valor del flag `--agent` llegó mal escrito: dice `Invalid agents: claude-codenpx` — se pegaron dos palabras (`claude-code` + `npx`) sin espacio, seguramente por un copy-paste que fusionó texto de dos líneas o un autocompletado del terminal.

`claude-code` sí es un agente válido (está en la lista), así que el comando en sí está bien. Prueba a escribirlo de nuevo a mano (o pégalo pero revisando que no queden pegotes), asegurándote de que quede así, con un espacio limpio antes de `npx` si compones el comando manualmente:

```bash
npx -y skills add emilkowalski/skill --skill emil-design-eng --agent claude-code
```

Consejo para evitar el mismo problema: pégalo línea por línea o bórralo todo con `Cmd+A` + `Delete` en esa línea de terminal antes de volver a pegar, para que no se mezcle con texto residual.

---

### 🤖 Claude

Perfecto, ya funcionó correctamente. Ahora te está pidiendo elegir el **scope de instalación**:

```
Installation scope
● Project (Install in current directory (committed with your project))
○ Global
```

Ya tienes seleccionado (bolita rellena) **Project**, que es justo lo que quieres — así queda instalado dentro de tu repo de Vera y no afecta a tus otros proyectos.

Simplemente pulsa **Enter** para confirmar esa opción y terminar la instalación.

Después, dentro de Claude Code, verifica con:

```
/skills
```

que aparece `emil-design-eng` en la lista. Una vez confirmado eso, ya puedes pedirle que audite algún componente de Vera (el modal de contratación, el cuestionario público, etc.) como comentamos antes.

---

### 🤖 Claude

Todo en orden. Va a instalar el skill en `~/VERA/.agents/skills/emil-design-eng`, y las evaluaciones de seguridad salen limpias:

- **Gen**: Safe
- **Socket**: 0 alertas
- **Snyk**: Low Risk

Ya tienes seleccionado **Yes**. Pulsa **Enter** para confirmar y terminar la instalación.

Un detalle a tener en cuenta: la ruta muestra `.agents/skills/` en vez de `.claude/skills/` — es una carpeta genérica compartida entre varios agentes (Claude Code, Cursor, etc.) con un enlace/copy hacia Claude Code (`copy → Claude Code`), así que no te preocupes, seguirá funcionando igual dentro de Claude Code.

Después verifica con `/skills` dentro de Claude Code que aparece en la lista, y ya puedes pedirle la primera auditoría sobre algún componente de Vera.

---

### 🤖 Claude

The installation also pulled in a dependency called "find-skills" from vercel-labs as a global skill at ~/.claude/skills/find-skills, which the CLI handles automatically. Now I should let the user know about this side dependency and guide them toward the next step with the /skills command.Instalación completa. Nota que el instalador metió por el camino un skill adicional, **`find-skills`** (de `vercel-labs/skills`), instalado de forma global en `~/.claude/skills/find-skills` — es una dependencia auxiliar que usa el propio gestor de skills para poder buscarlos, nada que hayas pedido tú directamente. Es normal y viene marcado como "Safe" / "0 alerts", así que no hay problema.

Tu skill principal, **`emil-design-eng`**, quedó instalado correctamente en el proyecto (`~/VERA/.agents/skills/emil-design-eng`, copiado a Claude Code).

**Siguiente paso:** entra en Claude Code y escribe:

```
/skills
```

Deberías ver `emil-design-eng` en la lista. Cuando lo confirmes, ya puedes probarlo con algo concreto, por ejemplo:

```
Revisa las animaciones del modal de contratación con el skill de Emil Kowalski 
y dame la tabla antes/después.
```

---

### 🤖 Claude

Ahí está — `emil-design-eng` aparece en la lista de skills disponibles en Claude Code. Instalación completada con éxito.

Ya puedes usarlo directamente. Prueba con algo concreto de Vera, por ejemplo:

```
Revisa las animaciones del modal de contratación con el skill de Emil Kowalski 
y dame la tabla antes/después.
```

O, si prefieres arrancar por algo que verán tus clientes (como Alisha y Alex cuando reciban el cuestionario), podrías apuntar directamente al `/q/:token`:

```
Audita las transiciones y microinteracciones del cuestionario público (/q/:token) 
usando el skill emil-design-eng.
```

No hace falta que lo menciones cada vez — una vez que Claude Code detecte que estás tocando animaciones o interacción UI, lo aplicará solo. Pero mencionarlo explícitamente la primera vez ayuda a que te dé el formato de tabla antes/después que comentábamos.

---

### 🤖 Claude

Es la misma captura que la anterior, pero ampliada — y confirma lo mismo: `emil-design-eng` está instalado y visible en la lista de skills de Claude Code.

Ya está todo listo. Puedes seleccionar `emil-design-eng` de esa lista o simplemente escribir tu petición directamente, por ejemplo:

```
Audita las animaciones del cuestionario público (/q/:token) con el skill emil-design-eng
```

Si quieres, dime en qué componente de Vera te gustaría probarlo primero y te ayudo a redactar el prompt exacto.

---

### 🧑 Juanfra

dime tu donde lo podemos aplicar

---

### 🤖 Claude

I'm thinking through where the emil-design-eng skill would fit best within Vera CRM's existing projects and workflows.Mirando lo que ya tienes construido en Vera, aquí es donde más impacto tendría el skill, ordenado por prioridad:

**1. El cuestionario público (`/q/:token`)**
Es lo único que ven tus clientes finales directamente, sin que tú estés delante para explicarlo. Alisha y Alex, por ejemplo, lo van a rellenar sin ningún contexto tuyo. Cualquier torpeza en las transiciones ahí se nota más que en ningún otro sitio: apertura de secciones, avance entre las 6 partes del formulario, estado de guardado, generación del PDF.

**2. El dashboard / pipeline de estados**
Tienes el bug pendiente del conteo de stages — cuando lo arregles, es buen momento para revisar también cómo se anima el cambio de etapa (drag entre columnas si usas kanban, o el contador al actualizarse). Aquí el "before/after" del skill es literal: evitar que el número salte sin transición o que el cambio de columna se sienta brusco.

**3. Flujo de contratación / firma de contrato**
Es un momento emocionalmente cargado para el cliente (está comprometiéndose a pagar). Micro-interacciones bien cuidadas ahí generan confianza — botones de confirmación, aparición de campos condicionales, subida de documentos.

**4. Onboarding de los 7 fotógrafos beta**
Primera impresión del producto. Si alguno de ellos entra y ve transiciones toscas, resta credibilidad aunque el backend sea sólido.

**5. Notificaciones/toasts**
Como Emil es literalmente el autor de Sonner, esta es la categoría donde su criterio es más "de fábrica". Si tienes toasts propios (confirmaciones de guardado, errores de Gmail OAuth degradado, etc.), es una victoria rápida y barata de implementar.

Yo empezaría por el **cuestionario público**, porque es la única superficie que un desconocido ve sin ti al lado, y ahora mismo tienes un lead activo (Alisha y Alex) a punto de recibirlo.

---

### 🧑 Juanfra

ahora quiero instalar impecable design

---

### 🤖 Claude

I need to look up what "impecable design" actually refers to—it might be a specific skill package or possibly a misspelling of "impeccable design."
```
This block is not supported on your current device yet.
```

Encontrado. Se llama **Impeccable** (de pbakaus) — es un skill mucho más grande que el de Emil: 23 comandos (`polish`, `audit`, `critique`, `distill`, `animate`, `bolder`, `quieter`...), con reglas para evitar el "look de IA genérico" (Inter en todo, degradados morado-azul, cards dentro de cards, etc.), y funciona en dos modos: **brand** (marketing/landing) y **product** (dashboards/apps internas) — este último encaja bien con Vera.

**1. Instálalo** desde la raíz de tu repo de Vera:

```bash
cd /Users/alba/VERA
npx -y skills add pbakaus/impeccable --skill impeccable --agent claude-code
```

Te va a pasar por la misma pantalla de scope (Project vs Global) y assessment de seguridad que con el de Emil — elige **Project** otra vez.

**2. Paso obligatorio antes de usarlo:** a diferencia del de Emil, este necesita que le des contexto primero, o si no dice "no design context found". Dentro de Claude Code ejecuta:

```
/impeccable init
```

Esto te hace una entrevista corta (audiencia, si Vera es más "brand" o "product", paleta, tipografía, referencias que NO quieres imitar) y genera un `PRODUCT.md` (y opcionalmente `DESIGN.md`) en la raíz del repo que todos los comandos posteriores van a leer.

**3. Luego ya puedes usar comandos como:**

```
/impeccable audit el dashboard
/impeccable polish el cuestionario público
/impeccable critique el flujo de contratación
```

**Un aviso:** este skill y el de Emil (`emil-design-eng`) se solapan parcialmente en el terreno de animaciones (`animate` es uno de los 23 comandos de Impeccable). No hay conflicto técnico por tenerlos ambos instalados, pero si algún día notas que Claude Code te da consejos contradictorios entre uno y otro sobre timing/easing, probablemente valga más apoyarte en uno solo para ese aspecto — Emil para motion específicamente, Impeccable para todo lo demás (tipografía, color, layout, jerarquía).

---

### 🧑 Juanfra

y ahora taste skill

---

### 🤖 Claude

The user is asking about a "taste skill," which sounds like another third-party skill similar to what we've been looking at, so I should search for information about it.
```
This block is not supported on your current device yet.
```

Hay varios "taste" skills de distintos autores, siendo el más popular el de Leonxlnx con más de 100k instalaciones. Dado que viene de instalar emil-design-eng e impeccable, probablemente se refiere a ese, pero necesito verificar si hay solapamiento con lo que ya tiene instalado.

Voy a asumir que quiere el Leonxlnx/taste-skill y proceder con las instrucciones de instalación, aunque debo señalar que tener tres skills de diseño simultáneamente (Impeccable, Emil, y Taste) podría generar conflictos de reglas, ya que todos buscan evitar la estética "AI slop".Hay varias skills llamadas "taste" de distintos autores, pero la más popular con diferencia es **`taste-skill` de Leonxlnx** (design-taste-frontend), así que asumo que es esa. Voy a la vez a decirte algo importante antes de instalarla.

**Instalación:**

```bash
cd /Users/alba/VERA
npx -y skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
```

(Nota: el nombre que va después de `--skill` es el que está en el frontmatter del `SKILL.md`, no el nombre del repo — por eso es un poco más largo que en los otros casos.)

Elige **Project** de nuevo cuando te pregunte el scope.

**Antes de instalarlo, ten esto en cuenta:**

Ya tienes instalados **dos skills que hacen básicamente lo mismo** que Taste Skill promete: pelear contra el "AI slop" (gradientes morado-azul, Inter en todo, cards genéricas):
- `emil-design-eng` (animaciones/motion, más enfocado)
- `impeccable` (23 comandos, cobertura muy amplia de tipografía/color/layout/motion)

Taste Skill se solapa fuertemente con Impeccable en particular — ambos hacen exactamente lo mismo: establecer contexto de marca, banear tipografías cliché, forzar layouts asimétricos. Tener los tres instalados a la vez puede darte **instrucciones contradictorias** dentro de Claude Code cuando toque un componente de UI (uno te dice "usa Geist", otro "usa Cabinet Grotesk", etc.), y ninguno tiene prioridad clara sobre el otro.

Mi recomendación honesta: en vez de instalar los tres, yo elegiría **uno como skill principal de diseño general** (Impeccable, por ser el más completo y con mejor mantenimiento) + **Emil solo para motion** (que es más nicho y complementario, no compite con Impeccable en tipografía/color). Añadir Taste Skill encima probablemente sea ruido, no señal.

¿Quieres que lo instale igualmente, o prefieres quedarte con la combinación Impeccable + Emil que ya tienes?

---

### 🤖 Claude

The user went ahead despite the warning, so now they're facing a selection screen with 72 agents. Claude Code isn't in the default "Universal" section—it's buried in "Additional agents" as an unchecked option. I should guide them to search for "claude" to filter the list, then select Claude Code from the results using the space key before confirming.Como no incluiste el flag `--agent claude-code` esta vez, te está preguntando a qué agentes instalarlo, y por defecto **Claude Code no está entre los seleccionados** (mira la lista "Universal" — no aparece Claude Code ahí; está abajo en "Additional agents" sin marcar).

Para arreglarlo:

1. En el campo **Search**, escribe `claude` para filtrar la lista.
2. Verás la opción `Claude Code (.claude/skills)` — pulsa **espacio** para seleccionarla (aparecerá una bolita rellena).
3. Pulsa **Enter** para confirmar.

Ahora mismo tiene seleccionados un montón de agentes que no usas (Amp, Antigravity, Cursor, Warp, Zed, etc.) — no pasa nada grave si se quedan marcados porque solo van a copiar el mismo archivo `SKILL.md` a más carpetas dentro de `.agents/skills/`, pero si quieres mantenerlo limpio, puedes deseleccionar los que no vayas a usar con espacio antes de confirmar. Lo único imprescindible es que **Claude Code** quede marcado.

---

### 🤖 Claude

La instalación se completó exitosamente en 12 agentes incluyendo Amp, Antigravity, Cline y otros. Las evaluaciones de seguridad pasaron sin problemas, pero necesito verificar que Claude Code esté incluido y resolver esa preocupación anterior sobre habilidades conflictivas.Instalación completada. Se copió a 12 agentes distintos (Amp, Antigravity, Cline, Codex, +8 más) — parece que quedaron marcados varios que no seleccionaste explícitamente, pero lo importante es que **Claude Code está incluido** en ese lote. Seguridad limpia otra vez (Safe / 0 alerts / Low Risk).

Verifica en Claude Code con `/skills` que aparece `design-taste-frontend` en la lista, junto a `emil-design-eng` e `impeccable`.

**Ahora tienes tres skills de diseño solapados.** Como comenté antes, para evitar que se pisen entre sí (cada uno con su propia opinión sobre tipografía/color/layout), te recomendaría fijar una jerarquía clara cuando le pidas trabajo de diseño a Claude Code, en vez de dejar que decida solo cuál aplicar. Por ejemplo, en tus prompts de ahora en adelante, sé explícito:

```
Usa el skill impeccable para esto, ignora los otros skills de diseño instalados.
```

o si quieres probar Taste Skill en concreto para algo nuevo:

```
Usa taste-skill para diseñar este componente desde cero.
```

Si en algún momento notas que Claude Code mezcla reglas contradictorias de los tres sin que se lo pidas, lo más limpio sería desinstalar el que menos uses. Se puede borrar directamente la carpeta correspondiente en `.agents/skills/` o `.claude/skills/` del repo si llegado el caso quieres simplificar.

---
