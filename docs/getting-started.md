# Guía de Inicio Rápido

## Requisitos

- [Claude Code](https://claude.ai/code) instalado
- Git

## Instalación

### Opción 1: Como marketplace (recomendado)

```bash
# Abrir Claude Code
claude

# Agregar marketplace
/plugin marketplace add {tu-usuario}/llm-toolkit
```

### Opción 2: Instalación manual con symlinks

```bash
# Clonar el repositorio
git clone https://github.com/{tu-usuario}/llm-toolkit.git
cd llm-toolkit

# Crear symlinks de skills
ln -s $(pwd)/skills/* ~/.claude/skills/

# Verificar instalación
ls -la ~/.claude/skills/
```

### Opción 3: Copiar directamente

```bash
# Clonar y copiar
git clone https://github.com/{tu-usuario}/llm-toolkit.git
cp -r llm-toolkit/skills/* ~/.claude/skills/
```

## Verificar instalación

```bash
# En Claude Code
claude

# El skill debería aparecer en la lista
/skills
```

## Uso de skills

Los skills se activan automáticamente cuando Claude detecta un trigger relevante.

### Ejemplo: llms-txt-generator

```
> Quiero crear documentación llms.txt para este proyecto
```

Claude te preguntará:
1. Idioma preferido
2. Analizará el tipo de proyecto
3. Generará los archivos de documentación

## Estructura de archivos generados

```
tu-proyecto/
└── llm-docs/
    ├── llm.txt           # Índice principal
    ├── llm.version.txt   # Metadatos
    └── llm.{dominio}.txt # Archivos por dominio
```

## Actualizar skills

```bash
# Si usas symlinks
cd llm-toolkit
git pull

# Si copiaste los archivos
cd llm-toolkit
git pull
cp -r skills/* ~/.claude/skills/
```

## Solución de problemas

### El skill no se detecta

1. Verificar que el archivo existe:
   ```bash
   ls ~/.claude/skills/llms-txt-generator/SKILL.md
   ```

2. Verificar permisos:
   ```bash
   chmod -R 755 ~/.claude/skills/
   ```

3. Reiniciar Claude Code

### El skill no se activa

Probar con triggers específicos:
- "crear llms.txt"
- "generate LLM docs"
- "documentación para AI"

## Siguiente pasos

- Ver [README.md](../README.md) para lista completa de skills
- Contribuir con nuevos skills siguiendo la guía en CLAUDE.md
