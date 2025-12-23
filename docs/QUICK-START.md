# Quick Start - llm-toolkit

Empieza a usar llm-toolkit en 5 minutos.

## Instalacion

### Opcion 1: Desde GitHub Marketplace (recomendado)

```bash
# Agregar el marketplace
claude plugin marketplace add Testacode/llm-toolkit

# Instalar el plugin
claude plugin install llm-toolkit
```

### Opcion 2: Desde repositorio local

```bash
# Clonar el repositorio
git clone https://github.com/Testacode/llm-toolkit.git

# Crear symlink al directorio de plugins
ln -s $(pwd)/llm-toolkit ~/.claude/plugins/llm-toolkit
```

## Verificar instalacion

```bash
# Ver skills disponibles
claude skills list

# Ver commands disponibles
claude commands list

# Ver agents disponibles
claude agents list
```

## Uso rapido

### Skills

Los skills son workflows guiados para tareas complejas:

```bash
# Generar documentacion llms.txt
/llms-txt-generator

# Mejorar CLAUDE.md de un proyecto
/claude-md-writer

# Crear proyecto Next.js con stack configurable
/nextjs-project-starter
```

### Commands

Los commands son utilidades rapidas:

```bash
# Generar commit convencional
/commit

# Explicar codigo
/explain path/to/file.ts

# Crear diagrama
/diagram arquitectura del sistema

# Simplificar codigo complejo
/simplify path/to/complex-file.ts
```

### Agents

Los agents son especialistas que puedes invocar:

```
Usa el agent codebase-analyst para entender este proyecto
Usa el agent nodejs-expert para optimizar esta funcion
Usa el agent vitest-expert para escribir tests
```

## Estructura del toolkit

```
llm-toolkit/
├── skills/           # Workflows guiados
│   ├── llms-txt-generator/
│   ├── claude-md-writer/
│   └── nextjs-project-starter/
├── commands/         # Utilidades rapidas
│   ├── git/         # commit
│   ├── code/        # explain, simplify, translate
│   ├── docs/        # diagram, document
│   └── dev/         # prototype, summary
├── agents/          # Especialistas
└── docs/            # Documentacion
```

## MCP Servers recomendados

Para mejorar la experiencia, configura estos MCP servers:

```bash
# Context7 - Documentacion actualizada de librerias
claude mcp add context7 npx -y @upstash/context7-mcp
```

Ver [mcp-servers-guide.md](./mcp-servers-guide.md) para mas opciones.

## Siguientes pasos

1. **Explorar skills**: Lee los SKILL.md de cada skill para entender su workflow
2. **Personalizar**: Copia y modifica commands/agents para tu caso de uso
3. **Contribuir**: PRs bienvenidos para nuevos skills, commands o agents

## Problemas comunes

### "Skill not found"

```bash
# Verificar que el plugin esta instalado
claude plugin list

# Reinstalar si es necesario
claude plugin uninstall llm-toolkit
claude plugin install llm-toolkit
```

### "Command not working"

```bash
# Verificar sintaxis
/help command-name
```

### MCP servers no cargan

1. Verificar que npm/npx esta instalado
2. Reiniciar Claude Code
3. Primera ejecucion puede ser lenta (descarga de paquetes)

## Recursos

- [README.md](../README.md) - Overview completo
- [claude-md-best-practices.md](./claude-md-best-practices.md) - Escribir CLAUDE.md efectivos
- [mcp-servers-guide.md](./mcp-servers-guide.md) - Guia de MCP servers
