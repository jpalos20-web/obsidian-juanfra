---
title: Guía de prompting de Claude
tags:
  - resources
  - tema/claude
---

# Guía de prompting de Claude

*(fuente: proyecto "How to use Claude" — guía oficial de Anthropic, 2026-04-30)*

## Consejos generales

1. **Sé claro y específico** — indica la tarea al principio, da contexto y detalles, y divide tareas complejas en pasos.
2. **Usa ejemplos** — muestra el formato/tono que buscas con un ejemplo concreto en vez de describirlo en abstracto.
3. **Fomenta el razonamiento** — pide "piensa paso a paso" o "explica tu razonamiento" en tareas complejas; da estructura guiada (ej. una lista de factores a considerar) y pide un resumen final.
4. **Refinamiento iterativo** — en vez de "hazlo mejor", da instrucciones concretas: qué tono, qué añadir, qué acortar.
5. **Aprovecha el conocimiento de Claude** — pide explicaciones/contexto de fondo con el marco de uso explícito, no solo la pregunta pelada.
6. **Usa role-playing** — pide a Claude que adopte una perspectiva concreta (ej. "eres mi proveedor de tela, dame 3 objeciones a mi petición de bajar el precio un 10%") para explorar varios ángulos de una negociación o decisión.

## Por tipo de tarea

**Creación de contenido**
- Especifica la audiencia (nivel técnico, tono esperado).
- Define tono/estilo, idealmente con referencia a una guía de marca.
- Da una estructura básica (secciones, nº de palabras, qué visualización usar en cada sección).

**Resumen y preguntas sobre documentos**
- Sé específico sobre qué aspecto resumir, no "resume esto".
- Refiérete a los documentos adjuntos por su nombre.
- Pide citas de secciones/páginas concretas en las respuestas.

**Análisis y visualización de datos**
- Especifica el formato de salida exacto (resumen ejecutivo, métricas clave, tendencias, recomendaciones) en vez de "analiza esto".
- Pide sugerencias de visualización después del análisis.

**Brainstorming**
- Acota el tema y pide cantidad concreta de ideas, con categorización.
- Pide formato tabla/lista para comparaciones (ej. comparar herramientas por varios criterios).

## Minimizar alucinaciones y maximizar rendimiento

- Permite explícitamente que Claude admita incertidumbre ("si no lo sabes, dilo").
- Divide tareas grandes en pasos más pequeños si Claude se salta partes.
- Claude no retiene contexto entre conversaciones — incluye todo el contexto necesario en cada conversación nueva.

## Patrón de prompt "bueno" combinado

Los mejores prompts combinan varias técnicas a la vez: asignar un rol específico (ej. "consultor de marketing senior"), desglosar la tarea en secciones numeradas con su propio formato de salida, pedir razonamiento/ejemplos donde aporte, y cerrar pidiendo que anticipe objeciones o preguntas de seguimiento y las responda de antemano.

## 🔗 Relacionado

- [[skills-claude-code-instalacion]]
