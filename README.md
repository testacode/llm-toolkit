# LLM Toolkit

Colección de herramientas, configuraciones y extensiones para trabajar con modelos de lenguaje (Claude, GPT, Qwen, Mistral, etc.).

## Estructura del Repositorio

```
llm-toolkit/
├── skills/                 # Skills para Claude Code
├── agents/                 # Agentes especializados
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
| `agents/` | Agentes especializados para tareas específicas (investigación, expertos técnicos) |
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
| [claude-md-writer](skills/claude-md-writer/) | Guía para escribir y mejorar archivos CLAUDE.md siguiendo best practices | "crear CLAUDE.md", "revisar CLAUDE.md" |
| [nextjs-project-starter](skills/nextjs-project-starter/) | Crea proyectos Next.js con stack configurable (Mantine, Supabase, Zustand) | "crear proyecto", "new nextjs project" |

## Commands Disponibles

| Command | Descripción | Uso |
|---------|-------------|-----|
| [commit](commands/commit.md) | Genera commits siguiendo conventional commits | `/commit` |
| [diagram](commands/diagram.md) | Genera diagramas ASCII o Mermaid | `/diagram` |
| [document](commands/document.md) | Genera documentación automática | `/document` |
| [explain](commands/explain.md) | Explica código o arquitectura | `/explain` |
| [prototype](commands/prototype.md) | Crea proof-of-concepts rápidos | `/prototype` |
| [simplify](commands/simplify.md) | Refactoriza código complejo | `/simplify` |
| [summary](commands/summary.md) | Resume conversaciones largas | `/summary` |
| [translate](commands/translate.md) | Traduce código entre lenguajes | `/translate` |

## Agents Disponibles

| Agent | Descripción | Modelo |
|-------|-------------|--------|
| [codebase-analyst](agents/codebase-analyst.md) | Análisis profundo de codebases | sonnet |
| [github-actions-expert](agents/github-actions-expert.md) | Experto en GitHub Actions y CI/CD | sonnet |
| [grafana-expert](agents/grafana-expert.md) | Experto en dashboards y visualización Grafana | sonnet |
| [java-expert](agents/java-expert.md) | Experto en desarrollo Java | opus |
| [loki-expert](agents/loki-expert.md) | Experto en agregación de logs con Loki | sonnet |
| [nodejs-expert](agents/nodejs-expert.md) | Experto en Node.js y programación asíncrona | opus |
| [scala-expert](agents/scala-expert.md) | Experto en Scala y programación funcional | opus |
| [tech-researcher](agents/tech-researcher.md) | Investigador técnico para frameworks y librerías | sonnet |
| [vitest-expert](agents/vitest-expert.md) | Experto en unit testing con Vitest | opus |
| [web-researcher](agents/web-researcher.md) | Investigador general para cualquier tema | sonnet |

## Compatibilidad

| Herramienta | Skills | Agents | Hooks | Commands | Prompts | Configs |
|-------------|--------|--------|-------|----------|---------|---------|
| Claude Code | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Claude.ai | - | - | - | - | ✓ | - |
| Cursor | - | - | - | - | ✓ | ✓ |
| ChatGPT | - | - | - | - | ✓ | - |
| Copilot | - | - | - | - | - | ✓ |

## Instalación

### Claude Code (recomendado)

```bash
# Agregar como marketplace
claude
/plugin marketplace add testacode/llm-toolkit
```

### Instalación manual

```bash
# Clonar repositorio
git clone https://github.com/testacode/llm-toolkit.git

# Symlink de skills
ln -s $(pwd)/llm-toolkit/skills/* ~/.claude/skills/

# Symlink de agents
ln -s $(pwd)/llm-toolkit/agents/* ~/.claude/agents/

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

Para usar los commands:

```
> /commit
> /explain src/main.ts
> /diagram arquitectura del sistema
```

## Documentación

| Documento | Descripción |
|-----------|-------------|
| [Getting Started](docs/getting-started.md) | Guía de inicio rápido |
| [CLAUDE.md Best Practices](docs/claude-md-best-practices.md) | Best practices para escribir CLAUDE.md |
| [LLM Toolkit Plan](docs/llm-toolkit-plan.md) | Plan original del proyecto |

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
5. Actualizar `.claude-plugin/marketplace.json`

### Agregar un nuevo agent

1. Crear archivo en `agents/{nombre-agent}.md`
2. Usar formato YAML frontmatter con: name, description, tools, model
3. Documentar en este README

### Agregar un nuevo command

1. Crear archivo en `commands/{nombre}.md`
2. Escribir el prompt del comando
3. Documentar en este README

## Licencia

MIT
