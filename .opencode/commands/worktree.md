---
description: Crea git worktree en .worktrees/
agent: build
subagent: false
---

Crea un git worktree a partir de `$ARGUMENTS`. No hagas nada más.

Pasos obligatorios:

1. Normaliza `$ARGUMENTS` a `WORKTREE_NAME` en kebab-case:
   - Minúsculas, sin acentos ni diacríticos.
   - Espacios y `_` -> `-`.
   - Conserva solo `[a-z0-9-]`, colapsa `--` a `-`, recorta `-` inicial/final.
   - Si supera 50 caracteres, simplifícalo: corta en el `-` anterior más cercano sin pasar 50 y recorta `-` final.
2. Ejecuta únicamente, sin cambiar de directorio:
   `mkdir -p .worktrees`
   `git worktree add .worktrees/WORKTREE_NAME`
3. No cambies de directorio, no muevas la sesión, no crees ramas manuales, no instales nada, no hagas nada adicional.

Nombre de entrada: $ARGUMENTS
