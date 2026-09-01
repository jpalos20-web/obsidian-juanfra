---
fuente: chat "Instalación de skill de emilkowalski"
fecha: 2026-07-01
relevancia: alta
tags:
  - research
  - tema/claude-code
---

# Instalar skills de diseño en Claude Code

## 📝 Resumen

Instalación de tres skills de diseño de terceros en el repo de Vera CRM: `emil-design-eng` (Emil Kowalski, animaciones/motion), `impeccable` (pbakaus, 23 comandos, cobertura amplia) y `design-taste-frontend` (Leonxlnx, "Taste Skill"). Claude Code no puede auto-instalarse skills (su terminal es un sandbox sin acceso al Mac real); hay que guiar al usuario paso a paso por su propia terminal.

## 💡 Insights principales

- Comando de instalación: `npx -y skills add <repo> --skill <nombre> --agent claude-code`, con scope **Project** (queda en `.claude/skills/` o `.agents/skills/` del repo, no global).
- Si falta `--agent claude-code`, hay que seleccionar manualmente "Claude Code" entre ~72 agentes disponibles en el instalador.
- Verificar cada skill instalada con `/skills` dentro de Claude Code.
- El instalador añade automáticamente `find-skills` (vercel-labs) como dependencia global.
- Las tres skills de diseño se solapan bastante entre sí (tipografía/color/layout "anti-AI slop") — usar `impeccable` como skill general principal, `emil-design-eng` solo para motion/animación, y valorar desinstalar `design-taste-frontend` si genera reglas contradictorias.

## 🛠 Aplicación práctica

- Orden de prioridad recomendado para auditar una app con estas skills: 1) pantallas cara al cliente (formularios públicos), 2) dashboard/pipeline, 3) flujo de contratación/firma, 4) onboarding, 5) toasts/notificaciones.

## 📎 Transcripción completa

- [[2026-07-01-instalaci-n-de-skill-de-emilkowalski|Instalación de skill de emilkowalski]]

## 🔗 Relacionado

- [[vera-crm]]
- [[nexus-media-lab]]
