# LLM Toolkit

Repositorio de herramientas para trabajar con modelos de lenguaje.

## Estructura

- `skills/` - Skills para Claude Code (SKILL.md + references/)
- `rules/` - Reglas y estándares de código
- `hooks/` - Scripts pre/post eventos
- `commands/` - Slash commands personalizados
- `prompts/` - System prompts y templates
- `configs/` - Configuraciones para diferentes herramientas
- `docs/` - Documentación

## Comandos útiles

```bash
# Ver estructura
tree -I 'node_modules|.git'

# Validar skill
cat skills/{nombre}/SKILL.md | head -20

# Probar skill localmente
ln -s $(pwd)/skills/{nombre} ~/.claude/skills/
```

## Agregar nuevo skill

1. Crear `skills/{nombre}/SKILL.md`:

```yaml
---
name: nombre-del-skill
description: Descripción corta (max 1024 chars)
---

# Contenido del skill
...
```

2. Agregar referencias si necesita ejemplos:
   - `skills/{nombre}/references/ejemplo.md`

3. Actualizar `README.md` con el nuevo skill

4. Actualizar `.claude-plugin/marketplace.json`

## Agregar nuevo hook

1. Crear script en `hooks/{tipo}/{nombre}.sh`
2. Documentar en `docs/hooks-guide.md`

## Agregar nuevo command

1. Crear `commands/{nombre}.md` con el prompt
2. Documentar en README

## Convenciones

- Skills: nombres en kebab-case
- Documentación: español (código en inglés)
- Commits: conventional commits
