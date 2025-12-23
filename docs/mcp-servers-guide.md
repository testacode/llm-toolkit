# Guia de MCP Servers para llm-toolkit

Los **Model Context Protocol (MCP) Servers** son puentes que permiten a Claude Code interactuar con APIs externas, bases de datos, sistemas de archivos y herramientas en tiempo real.

## Por que usar MCP Servers?

- **Evitar alucinaciones**: Context7 provee docs actualizados de librerias
- **Automatizacion**: GitHub MCP gestiona repos, PRs, issues
- **Productividad**: Playwright automatiza testing E2E

## Servers Recomendados

### Tier 1: Esenciales (instalar siempre)

| Server | Caso de uso | Por que es esencial |
|--------|-------------|---------------------|
| **Context7** | Docs actualizados | Evita alucinaciones, docs por version |
| **GitHub** | Repos, PRs, issues | Todo proyecto usa git |

#### Context7

Resuelve el problema de docs desactualizados. Cuando preguntas sobre React 19 o Next.js 15, Context7 inyecta documentacion actual en el contexto.

```bash
claude mcp add context7 npx -y @upstash/context7-mcp
```

**Como funciona:**
```
Tu: "Como usar useActionState en React 19?"
    ↓
Claude llama a Context7
    ↓
Context7 busca docs de React 19.x
    ↓
Respuesta con API real, no alucinada
```

#### GitHub

Gestiona repositorios, pull requests e issues sin salir de Claude.

```bash
claude mcp add github npx -y @modelcontextprotocol/server-github
```

Requiere variable de entorno:
```bash
export GITHUB_TOKEN="tu-token-aqui"
```

### Tier 2: Productividad (segun necesidad)

| Server | Caso de uso | Cuando usar |
|--------|-------------|-------------|
| **Playwright** | Testing E2E | Proyectos web con tests |
| **DuckDuckGo** | Busquedas web | Research durante desarrollo |
| **Memory Bank** | Persistencia | Proyectos largos |

#### Playwright

Automatiza browser para testing y scraping.

```bash
claude mcp add playwright npx @playwright/mcp@latest
```

#### Sequential Thinking

Workspace estructurado para problemas complejos. Claude puede pensar paso a paso, revisar y explorar alternativas.

```bash
claude mcp add sequential-thinking npx -y @modelcontextprotocol/server-sequential-thinking
```

**Util para**: Arquitectura compleja, debugging, decisiones con trade-offs
**NO necesario para**: Tareas simples, preguntas directas

### Tier 3: Especificos por Stack

| Server | Stack | Proposito |
|--------|-------|-----------|
| **PostgreSQL** | Apps con Postgres | Queries en lenguaje natural |
| **Supabase** | Stack Supabase | DB + Auth + Storage |
| **Figma** | Design → Code | Traducir disenos a codigo |
| **Notion** | Knowledge base | Acceso a documentacion |

#### Supabase

```bash
claude mcp add supabase npx -y @supabase/mcp-server-supabase
```

Requiere variables de entorno:
```bash
export SUPABASE_URL="tu-url"
export SUPABASE_KEY="tu-key"
```

## Configuracion por Proyecto

### Estrategia recomendada

Define MCPs **globalmente** y agrega especificos **por proyecto**:

**Global** (`~/.claude.json`):
```json
{
  "mcpServers": {
    "context7": {
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    }
  }
}
```

**Proyecto con Supabase** (`~/Projects/mi-app/.mcp.json`):
```json
{
  "mcpServers": {
    "supabase": {
      "command": "npx",
      "args": ["-y", "@supabase/mcp-server-supabase"],
      "env": {
        "SUPABASE_URL": "${SUPABASE_URL}",
        "SUPABASE_KEY": "${SUPABASE_KEY}"
      }
    }
  }
}
```

**Proyecto sin MCPs extra** (`~/Work/proyecto/.mcp.json`):
```json
{
  "mcpServers": {}
}
```

### Deshabilitar MCPs por defecto

Si queres definir TODO globalmente pero deshabilitar algunos:

```json
// ~/.claude/settings.json
{
  "disabledMcpjsonServers": ["supabase", "playwright"]
}
```

Y re-habilitar en proyectos especificos:
```json
// ~/Projects/app/.claude/settings.json
{
  "disabledMcpjsonServers": []
}
```

## Tokens y Overhead

```
MCP instalado pero NO usado  → 0 tokens extra
MCP usado (tool call)        → tokens del output
Tool descriptions            → ~100-500 tokens por server
```

**Recomendacion**: 3-5 MCPs esenciales siempre activos. El resto activar segun proyecto.

## Troubleshooting

### MCP no carga

1. Verificar npm/npx instalado:
   ```bash
   which npx
   ```

2. Primera ejecucion es lenta (descarga paquetes)

3. Reiniciar Claude Code despues de agregar MCP

### Variables de entorno no funcionan

Usar `${VAR_NAME}` en configuracion, no `$VAR_NAME`:

```json
{
  "env": {
    "GITHUB_TOKEN": "${GITHUB_TOKEN}"  // Correcto
  }
}
```

### MCP no aparece en la lista

```bash
# Verificar configuracion
claude mcp list

# Ver logs de debug
claude --debug
```

## Recursos

- [mcp.so](https://mcp.so) - Directorio de servers
- [mcpmarket.com](https://mcpmarket.com) - Marketplace
- [awesome-mcp-servers](https://github.com/punkpeye/awesome-mcp-servers) - Lista curada
- [Context7 GitHub](https://github.com/upstash/context7)
- [Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code)
