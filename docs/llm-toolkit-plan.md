# llm-toolkit

Colección de herramientas, configuraciones y extensiones para trabajar con modelos de lenguaje (Claude, GPT, Qwen, Mistral, etc.).

## Estructura del Repositorio

```
llm-toolkit/
├── skills/                         # Skills para Claude Code
│   ├── llms-txt-generator/         # Generador de documentación LLM
│   └── {future-skills}/
│
├── rules/                          # Reglas y guidelines
│   ├── coding-standards.md         # Estándares de código
│   ├── security-checklist.md       # Checklist de seguridad
│   └── review-guidelines.md        # Guías de code review
│
├── hooks/                          # Hooks para Claude Code
│   ├── pre-commit/                 # Hooks pre-commit
│   │   └── security-check.sh
│   └── post-tool/                  # Hooks post-tool
│
├── commands/                       # Slash commands personalizados
│   ├── commit.md                   # /commit - mensaje convencional
│   ├── review.md                   # /review - code review
│   └── docs.md                     # /docs - generar documentación
│
├── prompts/                        # Prompts reutilizables
│   ├── system/                     # System prompts
│   │   ├── senior-engineer.md
│   │   └── code-reviewer.md
│   ├── templates/                  # Templates de prompts
│   │   ├── bug-fix.md
│   │   ├── feature-request.md
│   │   └── refactor.md
│   └── chains/                     # Cadenas de prompts
│
├── configs/                        # Configuraciones
│   ├── claude/                     # Configs específicas de Claude
│   │   ├── settings.json
│   │   └── CLAUDE.md.template
│   ├── cursor/                     # Configs para Cursor IDE
│   │   └── rules/
│   └── vscode/                     # Configs para VS Code + Copilot
│
├── docs/                           # Documentación
│   ├── getting-started.md
│   ├── skills-guide.md
│   ├── hooks-guide.md
│   └── contributing.md
│
└── README.md
```

## Skills Incluidos

### llms-txt-generator
Genera documentación optimizada para LLMs siguiendo el estándar llms.txt.

**Trigger**: "crear llms.txt", "generate LLM docs", "documentación para AI"

**Características**:
- Detecta tipo de proyecto (frontend, CLI, API, library)
- Pregunta idioma preferido
- Genera archivos granulares por dominio
- Soporta script generador o archivos estáticos

## Hooks Disponibles

| Hook | Tipo | Descripción |
|------|------|-------------|
| security-check | pre-commit | Detecta secrets y vulnerabilidades |
| lint-check | pre-commit | Verifica linting antes de commit |
| test-runner | post-edit | Ejecuta tests relacionados |

## Commands Disponibles

| Command | Descripción |
|---------|-------------|
| /commit | Genera mensaje de commit convencional |
| /review | Inicia code review estructurado |
| /docs | Genera/actualiza documentación |
| /refactor | Sugiere refactorizaciones |

## Prompts Incluidos

### System Prompts
- **senior-engineer**: Actúa como ingeniero senior con foco en calidad
- **code-reviewer**: Reviewer estricto con checklist
- **architect**: Diseño de arquitectura y decisiones técnicas

### Templates
- **bug-fix**: Template para reportar y resolver bugs
- **feature-request**: Template para nuevas features
- **refactor**: Template para proponer refactorizaciones

## Compatibilidad

| Herramienta | Soporte |
|-------------|---------|
| Claude Code | Skills, Hooks, Commands |
| Claude.ai | Prompts, Rules |
| Cursor | Rules, Prompts |
| ChatGPT | Prompts |
| Copilot | Configs |

## Instalación

### Claude Code

```bash
# Clonar repo
git clone https://github.com/{username}/llm-toolkit.git

# Symlink skills
ln -s $(pwd)/llm-toolkit/skills/* ~/.claude/skills/

# Symlink commands
ln -s $(pwd)/llm-toolkit/commands/* ~/.claude/commands/

# Copiar hooks
cp llm-toolkit/hooks/* ~/.claude/hooks/
```

### Cursor

```bash
# Copiar rules
cp -r llm-toolkit/configs/cursor/rules .cursor/
```

## Contribución

1. Fork el repositorio
2. Crear branch: `git checkout -b feature/mi-skill`
3. Seguir estructura existente
4. Documentar en README correspondiente
5. Crear PR

## Licencia

MIT

---

## Próximos Pasos

- [ ] Crear repositorio en GitHub
- [ ] Mover llms-txt-generator skill
- [ ] Agregar más skills
- [ ] Documentar hooks existentes
- [ ] Crear commands básicos
