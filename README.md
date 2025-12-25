# LLM Toolkit

Coleccion de herramientas, configuraciones y extensiones para trabajar con modelos de lenguaje (Claude, GPT, Qwen, Mistral, etc.).

> **Quick Start**: Ver [docs/QUICK-START.md](docs/QUICK-START.md) para empezar en 5 minutos.

## Estructura del Repositorio

```
llm-toolkit/
├── skills/                 # Skills para Claude Code
│   ├── llms-txt-generator/
│   ├── claude-md-writer/
│   ├── nextjs-project-starter/
│   └── doc-writer/
├── agents/                 # Agentes especializados
├── commands/               # Slash commands organizados
│   ├── git/               # commit
│   ├── code/              # explain, simplify, translate
│   ├── docs/              # diagram, document
│   └── dev/               # prototype, summary
├── docs/                   # Documentacion
├── .claude-plugin/         # Configuracion del marketplace
│   ├── marketplace.json
│   └── plugin.json        # Declaracion de todo el contenido
├── .claude/               # Configuracion local
│   └── settings.template.json
├── rules/                  # Reglas y guidelines (futuro)
├── hooks/                  # Hooks para Claude Code (futuro)
├── prompts/                # Prompts reutilizables (futuro)
└── configs/                # Configuraciones por IDE (futuro)
```

## Skills Disponibles

| Skill | Descripcion | Trigger |
|-------|-------------|---------|
| [llms-txt-generator](skills/llms-txt-generator/) | Genera documentacion optimizada para LLMs siguiendo el estandar llms.txt | "crear llms.txt", "generate LLM docs" |
| [claude-md-writer](skills/claude-md-writer/) | Guia para escribir y mejorar archivos CLAUDE.md siguiendo best practices | "crear CLAUDE.md", "revisar CLAUDE.md" |
| [nextjs-project-starter](skills/nextjs-project-starter/) | Crea proyectos Next.js con stack configurable (Mantine, Supabase, Zustand) | "crear proyecto", "new nextjs project" |
| [doc-writer](skills/doc-writer/) | Organiza specs, planes y docs tecnicos en docs/ con categorias y naming automatico | "escribir spec", "crear plan", "documentar ADR" |

## Commands Disponibles

### Git
| Command | Descripcion | Uso |
|---------|-------------|-----|
| [commit](commands/git/commit.md) | Genera commits siguiendo conventional commits | `/commit` |

### Code
| Command | Descripcion | Uso |
|---------|-------------|-----|
| [explain](commands/code/explain.md) | Explica codigo o arquitectura | `/explain` |
| [simplify](commands/code/simplify.md) | Refactoriza codigo complejo | `/simplify` |
| [translate](commands/code/translate.md) | Traduce codigo entre lenguajes | `/translate` |

### Docs
| Command | Descripcion | Uso |
|---------|-------------|-----|
| [diagram](commands/docs/diagram.md) | Genera diagramas ASCII o Mermaid | `/diagram` |
| [document](commands/docs/document.md) | Genera documentacion automatica | `/document` |

### Dev
| Command | Descripcion | Uso |
|---------|-------------|-----|
| [prototype](commands/dev/prototype.md) | Crea proof-of-concepts rapidos | `/prototype` |
| [summary](commands/dev/summary.md) | Resume conversaciones largas | `/summary` |

## Agents Disponibles

| Agent | Descripcion | Modelo |
|-------|-------------|--------|
| [codebase-analyst](agents/codebase-analyst.md) | Analisis profundo de codebases | sonnet |
| [github-actions-expert](agents/github-actions-expert.md) | Experto en GitHub Actions y CI/CD | sonnet |
| [grafana-expert](agents/grafana-expert.md) | Experto en dashboards y visualizacion Grafana | sonnet |
| [java-expert](agents/java-expert.md) | Experto en desarrollo Java | opus |
| [loki-expert](agents/loki-expert.md) | Experto en agregacion de logs con Loki | sonnet |
| [nodejs-expert](agents/nodejs-expert.md) | Experto en Node.js y programacion asincrona | opus |
| [scala-expert](agents/scala-expert.md) | Experto en Scala y programacion funcional | opus |
| [tech-researcher](agents/tech-researcher.md) | Investigador tecnico para frameworks y librerias | sonnet |
| [vitest-expert](agents/vitest-expert.md) | Experto en unit testing con Vitest | opus |
| [web-researcher](agents/web-researcher.md) | Investigador general para cualquier tema | sonnet |

## MCP Servers Recomendados

El toolkit incluye configuracion para MCP servers que mejoran la experiencia:

| Server | Proposito |
|--------|-----------|
| **Context7** | Documentacion actualizada de librerias - evita alucinaciones |

Ver [docs/mcp-servers-guide.md](docs/mcp-servers-guide.md) para la guia completa con tiers y configuracion.

## Instalacion

### Claude Code (recomendado)

```bash
# Agregar como marketplace
claude plugin marketplace add Testacode/llm-toolkit

# Instalar el plugin
claude plugin install llm-toolkit
```

### Instalacion manual

```bash
# Clonar repositorio
git clone https://github.com/Testacode/llm-toolkit.git

# Symlink de skills
ln -s $(pwd)/llm-toolkit/skills/* ~/.claude/skills/

# Symlink de agents
ln -s $(pwd)/llm-toolkit/agents/* ~/.claude/agents/
```

## Uso

Una vez instalados los skills, Claude Code los detectara automaticamente:

```
> Crear documentacion llms.txt para este proyecto
> Mejorar el CLAUDE.md de este proyecto
> Crear un nuevo proyecto Next.js con Supabase
```

Para usar los commands:

```
> /commit
> /explain src/main.ts
> /diagram arquitectura del sistema
> /simplify path/to/complex-file.ts
```

## Documentacion

| Documento | Descripcion |
|-----------|-------------|
| [Quick Start](docs/QUICK-START.md) | Empieza en 5 minutos |
| [MCP Servers Guide](docs/mcp-servers-guide.md) | Guia de MCP servers con tiers |
| [Getting Started](docs/getting-started.md) | Guia detallada de inicio |
| [CLAUDE.md Best Practices](docs/claude-md-best-practices.md) | Best practices para CLAUDE.md |

## Contribucion

1. Fork el repositorio
2. Crear branch: `git checkout -b feature/mi-feature`
3. Seguir la estructura existente
4. Documentar en el README correspondiente
5. Crear PR

### Agregar un nuevo skill

1. Crear carpeta en `skills/{nombre-skill}/`
2. Crear `SKILL.md` con el formato requerido
3. Agregar referencias en `references/` si aplica
4. Actualizar `plugin.json` y `marketplace.json`

### Agregar un nuevo agent

1. Crear archivo en `agents/{nombre-agent}.md`
2. Usar formato YAML frontmatter con: name, description, tools, model
3. Actualizar `plugin.json`

### Agregar un nuevo command

1. Crear archivo en `commands/{categoria}/{nombre}.md`
2. Categorias: `git/`, `code/`, `docs/`, `dev/`
3. Actualizar `plugin.json`

## Licencia

MIT
