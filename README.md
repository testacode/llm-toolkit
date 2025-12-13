# LLM Toolkit

Colección de herramientas, configuraciones y extensiones para trabajar con modelos de lenguaje (Claude, GPT, Qwen, Mistral, etc.).

## Estructura del Repositorio

```
llm-toolkit/
├── skills/                 # Skills para Claude Code
├── rules/                  # Reglas y guidelines
├── hooks/                  # Hooks para Claude Code
├── commands/               # Slash commands personalizados
├── prompts/                # Prompts reutilizables
│   ├── system/             # System prompts
│   └── templates/          # Templates de prompts
├── configs/                # Configuraciones
│   ├── claude/             # Configs para Claude Code
│   └── cursor/             # Configs para Cursor IDE
├── docs/                   # Documentación
└── .claude-plugin/         # Configuración del marketplace
```

### Descripción de carpetas

| Carpeta | Descripción |
|---------|-------------|
| `skills/` | Skills que extienden las capacidades de Claude Code con conocimiento especializado |
| `rules/` | Reglas de código, estándares y guidelines reutilizables |
| `hooks/` | Scripts que se ejecutan en respuesta a eventos de Claude Code |
| `commands/` | Comandos slash personalizados (ej: `/commit`, `/review`) |
| `prompts/` | Prompts reutilizables para diferentes herramientas LLM |
| `configs/` | Archivos de configuración para diferentes IDEs y herramientas |
| `docs/` | Documentación del proyecto |

## Skills Disponibles

| Skill | Descripción | Trigger |
|-------|-------------|---------|
| [llms-txt-generator](skills/llms-txt-generator/) | Genera documentación optimizada para LLMs siguiendo el estándar llms.txt | "crear llms.txt", "generate LLM docs" |

## Compatibilidad

| Herramienta | Skills | Hooks | Commands | Prompts | Configs |
|-------------|--------|-------|----------|---------|---------|
| Claude Code | ✓ | ✓ | ✓ | ✓ | ✓ |
| Claude.ai | - | - | - | ✓ | - |
| Cursor | - | - | - | ✓ | ✓ |
| ChatGPT | - | - | - | ✓ | - |
| Copilot | - | - | - | - | ✓ |

## Instalación

### Claude Code (recomendado)

```bash
# Agregar como marketplace
claude
/plugin marketplace add {tu-usuario}/llm-toolkit
```

### Instalación manual

```bash
# Clonar repositorio
git clone https://github.com/{tu-usuario}/llm-toolkit.git

# Symlink de skills
ln -s $(pwd)/llm-toolkit/skills/* ~/.claude/skills/

# Symlink de commands (opcional)
ln -s $(pwd)/llm-toolkit/commands/* ~/.claude/commands/

# Copiar hooks (opcional)
cp -r llm-toolkit/hooks/* ~/.claude/hooks/
```

### Cursor

```bash
# Copiar reglas
cp -r llm-toolkit/configs/cursor/* .cursor/
```

## Uso

Una vez instalados los skills, Claude Code los detectará automáticamente. Por ejemplo:

```
> Crear documentación llms.txt para este proyecto
```

Claude Code activará el skill `llms-txt-generator` y te guiará por el proceso.

## Contribución

1. Fork el repositorio
2. Crear branch: `git checkout -b feature/mi-feature`
3. Seguir la estructura existente
4. Documentar en el README correspondiente
5. Crear PR

### Agregar un nuevo skill

1. Crear carpeta en `skills/{nombre-skill}/`
2. Crear `SKILL.md` con el formato requerido
3. Agregar referencias en `references/` si aplica
4. Documentar en este README

## Licencia

MIT
