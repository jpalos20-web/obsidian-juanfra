---
title: "Instalación de skill de emilkowalski"
source: "https://claude.ai/chat/378c7db9-07e1-42e0-acbe-bba57a825fab"
author:
published: 2026-07-01
created: 2026-09-15
description: "Claude conversation with 4 messages"
tags:
  - "clippings"
---
**You**

y ahora taste skill

---

**Claude**

Hay varias skills llamadas "taste" de distintos autores, pero la más popular con diferencia es **`taste-skill` de Leonxlnx** (design-taste-frontend), así que asumo que es esa. Voy a la vez a decirte algo importante antes de instalarla.

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

**Claude**

Como no incluiste el flag `--agent claude-code` esta vez, te está preguntando a qué agentes instalarlo, y por defecto **Claude Code no está entre los seleccionados** (mira la lista "Universal" — no aparece Claude Code ahí; está abajo en "Additional agents" sin marcar).

Para arreglarlo:

1. En el campo **Search**, escribe `claude` para filtrar la lista.
2. Verás la opción `Claude Code (.claude/skills)` — pulsa **espacio** para seleccionarla (aparecerá una bolita rellena).
3. Pulsa **Enter** para confirmar.

Ahora mismo tiene seleccionados un montón de agentes que no usas (Amp, Antigravity, Cursor, Warp, Zed, etc.) — no pasa nada grave si se quedan marcados porque solo van a copiar el mismo archivo `SKILL.md` a más carpetas dentro de `.agents/skills/`, pero si quieres mantenerlo limpio, puedes deseleccionar los que no vayas a usar con espacio antes de confirmar. Lo único imprescindible es que **Claude Code** quede marcado.

---

**Claude**

Instalación completada. Se copió a 12 agentes distintos (Amp, Antigravity, Cline, Codex, +8 más) — parece que quedaron marcados varios que no seleccionaste explícitamente, pero lo importante es que **Claude Code está incluido** en ese lote. Seguridad limpia otra vez (Safe / 0 alerts / Low Risk).

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