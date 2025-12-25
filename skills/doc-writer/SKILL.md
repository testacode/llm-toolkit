---
name: doc-writer
description: Organiza documentos de specs, planes y documentacion tecnica en la carpeta docs/ del proyecto. Usa esta skill cuando el usuario pida escribir specs, planes de implementacion, documentacion tecnica, ADRs, o cualquier documento que deba guardarse en docs/. Detecta automaticamente el contexto (trabajo/personal) y sugiere la categoria apropiada.
allowed-tools: Read, Glob, Grep, Write, Edit, Bash, LS
---

# Doc Writer

Skill para organizar y crear documentos tecnicos en la estructura correcta del proyecto.

## Cuando usar esta Skill

- Usuario pide escribir una spec o especificacion
- Usuario pide crear un plan de implementacion
- Usuario pide documentar una decision arquitectonica (ADR)
- Usuario pide crear documentacion de referencia
- Cualquier documento que deba ir en `docs/`

## Proceso

### Paso 1: Detectar contexto

Determinar si es contexto **trabajo** o **personal**:

```bash
# Verificar usuario git
git config user.name

# Verificar directorio actual
pwd
```

**TRABAJO** si:
- `git config user.name` contiene "carlos-monti" O
- El directorio actual esta dentro de `~/Despegar/`

**PERSONAL** si:
- Cualquier otro caso

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

#### Trabajo (basado en estructura Despegar):
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

## Ejemplo de uso

Usuario: "Escribime una spec para el sistema de autenticacion"

1. Detectar contexto: Personal (no es carlos-monti, no es ~/Despegar/)
2. Buscar docs/: Existe, tiene subcarpetas `specs/`, `plans/`
3. Categoria: `specs/` (es una especificacion)
4. Nombre: `2025-12-25-15-30-authentication-system.md`
5. Crear: `docs/specs/2025-12-25-15-30-authentication-system.md` con Spec Template
