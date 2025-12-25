---
name: doc-writer
description: Crea y organiza documentos tecnicos en docs/. Usa esta skill para escribir specs, planes, ADRs, o documentacion de referencia. Tambien puede reorganizar documentos existentes, analizando su contenido y sugiriendo categorias (specs/, plans/, architecture/, reference/). Pregunta al usuario por las categorias antes de mover archivos.
allowed-tools: Read, Glob, Grep, Write, Edit, Bash, LS
---

# Doc Writer

Skill para organizar y crear documentos tecnicos en la estructura correcta del proyecto.

## Cuando usar esta Skill

### Crear documentos
- Usuario pide escribir una spec o especificacion
- Usuario pide crear un plan de implementacion
- Usuario pide documentar una decision arquitectonica (ADR)
- Usuario pide crear documentacion de referencia
- Cualquier documento que deba ir en `docs/`

### Organizar documentos
- Usuario pide "organizar", "reorganizar", "categorizar" documentos
- Usuario pide "ordenar docs" o "mover documentos a carpetas"
- Se detectan archivos `.md` sueltos directamente en `docs/` sin subcarpeta

## Proceso

### Paso 0: Detectar modo (Crear vs Organizar)

Primero determinar qué quiere hacer el usuario:

**MODO ORGANIZAR** si:
- El usuario menciona "organizar", "reorganizar", "categorizar", "ordenar" documentos
- Se detectan archivos `.md` directamente en `docs/` sin subcarpeta → sugerir organizar

**MODO CREAR** si:
- El usuario pide escribir, crear, documentar algo nuevo
- No aplican las condiciones de organización

Si es modo ORGANIZAR → ir a "Proceso de Organización"
Si es modo CREAR → continuar con Paso 1

---

## Proceso de Creación

### Paso 1: Detectar contexto

Determinar si es contexto **trabajo** o **personal**:

```bash
# Verificar directorio actual
pwd

# Buscar indicadores de proyecto corporativo
ls .github/ .gitlab/ 2>/dev/null
```

**TRABAJO** si:
- El directorio tiene estructura corporativa (múltiples owners, CI/CD complejo)
- El proyecto tiene guías de contribución empresariales

**PERSONAL** si:
- Proyecto individual o side-project
- Sin estructura corporativa evidente

### Paso 2: Buscar estructura de docs existente

```bash
# Buscar carpeta docs
ls -la docs/ 2>/dev/null

# Listar subcarpetas existentes
ls -d docs/*/ 2>/dev/null
```

### Paso 3: Determinar categoria

**Si existen subcarpetas en docs/**: Usar las existentes como opciones.

**Si no existen subcarpetas**, usar categorias base segun contexto:

#### Trabajo (estructura corporativa):
| Categoria | Uso |
|-----------|-----|
| `backlog/` | Features pendientes, ideas futuras |
| `work-in-progress/` | Documentacion de trabajo activo |
| `completed/` | Features terminadas |
| `history/` | Changelog, decisiones historicas |
| `reference/` | Docs tecnicos de referencia |

#### Personal:
| Categoria | Uso |
|-----------|-----|
| `specs/` | Especificaciones de features/sistemas |
| `plans/` | Planes de implementacion |
| `architecture/` | ADRs, decisiones arquitectonicas |
| `reference/` | Documentacion tecnica de referencia |

**IMPORTANTE**: Si hay ambiguedad sobre la categoria, preguntar al usuario.

### Paso 4: Generar nombre de archivo

Formato: `YYYY-MM-DD-HH-MM-<feature-name>.md`

- Usar fecha y hora actual
- `<feature-name>` en kebab-case, descriptivo, sin espacios

Ejemplo: `2025-12-25-14-30-user-authentication.md`

### Paso 5: Crear el documento

1. Crear subcarpeta si no existe
2. Aplicar template segun tipo de documento
3. Escribir archivo en la ubicacion correcta

## Templates

### Spec Template

Usar cuando el usuario pide una especificacion o spec de feature:

```markdown
# [Feature Name] - Specification

## Overview
Brief description of what this feature does.

## Requirements
- [ ] Requirement 1
- [ ] Requirement 2

## Technical Approach
How this will be implemented.

## Dependencies
- Dependency 1

## Open Questions
- Question 1?
```

### Plan Template

Usar cuando el usuario pide un plan de implementacion:

```markdown
# [Feature Name] - Implementation Plan

## Goal
What we're trying to achieve.

## Steps
1. Step 1
2. Step 2

## Considerations
- Risk/consideration 1

## Success Criteria
- [ ] Criteria 1
```

### Architecture Template (ADR)

Usar cuando el usuario pide documentar una decision arquitectonica:

```markdown
# ADR: [Decision Title]

## Status
Proposed | Accepted | Deprecated | Superseded

## Context
What is the issue that we're seeing that is motivating this decision?

## Decision
What is the change that we're proposing and/or doing?

## Consequences
What becomes easier or more difficult because of this change?
```

### Reference Template

Usar cuando el usuario pide documentacion de referencia:

```markdown
# [Topic] Reference

## Overview
What this document covers.

## Details
Technical details and usage.

## Examples
Code or usage examples.

## Related
- Link to related docs
```

---

## Proceso de Organización

### Paso O1: Inspeccionar estado actual

```bash
# Archivos sueltos en docs/ (sin subcarpeta)
ls docs/*.md 2>/dev/null

# Carpetas existentes y su contenido
ls -la docs/*/ 2>/dev/null

# Contar todos los archivos md
find docs -name "*.md" -type f 2>/dev/null
```

### Paso O2: Preguntar por categorías

Presentar al usuario las opciones disponibles:

1. **Categorías existentes** detectadas en el proyecto
2. **Categorías sugeridas** si no existen:

| Categoría | Uso |
|-----------|-----|
| `specs/` | Especificaciones de features/sistemas |
| `plans/` | Planes de implementación |
| `architecture/` | ADRs, decisiones arquitectónicas |
| `reference/` | Documentación técnica de referencia |

Formato de pregunta:
```
Categorías disponibles:
☐ specs/ - Especificaciones de features/sistemas
☐ plans/ - Planes de implementación
☐ architecture/ - ADRs, decisiones arquitectónicas
☐ reference/ - Documentación técnica de referencia
☐ [Crear nueva categoría]

¿Cuáles quieres usar para organizar?
```

### Paso O3: Analizar documentos y sugerir categorización

Para cada documento encontrado:

1. Leer contenido (primeras ~50 líneas)
2. Detectar tipo por keywords:

| Keywords detectados | Categoría sugerida |
|---------------------|-------------------|
| "ADR", "Decision", "Status: Accepted/Proposed", "Context", "Consequences" | `architecture/` |
| "Specification", "Requirements", "Spec", "Technical Approach" | `specs/` |
| "Plan", "Implementation", "Steps", "Timeline", "Goal" | `plans/` |
| "Reference", "Guide", "How to", "Examples", "Usage" | `reference/` |

3. Presentar sugerencias al usuario:

```
Análisis de documentos:

📄 authentication-notes.md
   Detectado: Menciona "requirements" y "technical approach"
   Sugerencia: specs/
   ¿Mover a specs/? [Y/n/otra categoría]

📄 db-migration-decision.md
   Detectado: Contiene "Status: Accepted", "Context", "Decision"
   Sugerencia: architecture/ (es un ADR)
   ¿Mover a architecture/? [Y/n/otra categoría]
```

### Paso O4: Ejecutar reorganización

Para cada documento confirmado:

1. Crear carpeta destino si no existe:
```bash
mkdir -p docs/<categoria>/
```

2. Mover archivo preservando historial git:
```bash
git mv docs/<archivo>.md docs/<categoria>/<archivo>.md
```

3. Renombrar al formato estándar si no lo tiene:
   - Formato: `YYYY-MM-DD-HH-MM-<name>.md`
   - Ejemplo: `2025-12-25-15-30-authentication-notes.md`

### Paso O5: Resumen final

Mostrar resultado de la organización:

```
✅ Organización completada:
- 3 archivos movidos a specs/
- 2 archivos movidos a architecture/
- 1 archivo movido a plans/
- 0 archivos sin categorizar

Archivos reorganizados:
- docs/specs/2025-12-25-15-30-authentication-notes.md
- docs/architecture/2025-12-25-15-31-db-migration-decision.md
- ...
```

---

## Ejemplos de uso

### Ejemplo: Crear documento

Usuario: "Escribime una spec para el sistema de autenticacion"

1. Detectar modo: CREAR (pide escribir algo nuevo)
2. Detectar contexto: Personal (proyecto individual)
3. Buscar docs/: Existe, tiene subcarpetas `specs/`, `plans/`
4. Categoria: `specs/` (es una especificacion)
5. Nombre: `2025-12-25-15-30-authentication-system.md`
6. Crear: `docs/specs/2025-12-25-15-30-authentication-system.md` con Spec Template

### Ejemplo: Organizar documentos

Usuario: "Organiza los documentos en docs/"

1. Detectar modo: ORGANIZAR (keyword "organiza")
2. Inspeccionar: Encuentra 3 archivos .md sueltos en docs/
3. Preguntar categorías: Usuario selecciona specs/, plans/, architecture/
4. Analizar cada archivo y sugerir categoría
5. Usuario confirma movimientos
6. Ejecutar: `git mv` para cada archivo
7. Mostrar resumen: "3 archivos reorganizados"
