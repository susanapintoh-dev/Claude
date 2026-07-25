# CLAUDE.md (raíz) — Mapa de Vaults

Este repositorio ya no es un único wiki: es un **monorepo de varios vaults
independientes**, uno por cada área de conocimiento del humano. Cada vault
vive en su propia carpeta de primer nivel y tiene su propio `CLAUDE.md` con
las reglas completas de gobernanza (frontmatter, nomenclatura, enlazado,
flujos de ingesta/consulta/lint) — ese `CLAUDE.md` de carpeta es la autoridad
para todo lo que ocurra dentro de ella. Este archivo raíz **no repite esas
reglas**; solo cubre lo que aplica a todo el repositorio.

## Vaults existentes

| Carpeta | Dominio | Gobernanza |
|---|---|---|
| `profesional/` | Ecosistemas de ciencia, tecnología e innovación: financiamiento de I+D+i empresarial, beneficios tributarios, valoración de la innovación, normativas por país | `profesional/CLAUDE.md` |
| `profesional/gestion-conocimiento/` | Teorías, frameworks, metodologías, herramientas y autores de gestión del conocimiento (conocimiento de trabajo profesional pasado, con impacto directo en innovación) | `profesional/gestion-conocimiento/CLAUDE.md` |
| `idiomas/` | Aprendizaje de francés y portugués (clases, apuntes, recursos) | `idiomas/CLAUDE.md` |
| `ia/` | Inteligencia artificial — conceptos, modelos, herramientas, clases, artículos | `ia/CLAUDE.md` |

Cuando el humano te pida trabajar en un vault, entra a esa carpeta, lee su
`CLAUDE.md` primero, y opera exclusivamente con las reglas de esa carpeta
(su propio `index.md`, `log.md`, `10_Raw/`, `20_Wiki/`, etc.).

**Nota de carpetas vs. bóvedas de Obsidian**: `gestion-conocimiento/` vive
anidada *dentro* de `profesional/` a propósito, no porque sea parte de ese
vault — es para que el humano pueda abrir `profesional/` como una sola
bóveda de Obsidian y ver ambos vaults juntos, con los wikilinks cruzados
resolviendo entre sí (ver regla de enlaces cruzados abajo). En la práctica,
el humano trabaja con **3 bóvedas de Obsidian abiertas por separado**:
`profesional/` (incluye gestión del conocimiento), `idiomas/`, e `ia/`. Cada
una sigue siendo gobernada únicamente por su propio `CLAUDE.md` — la
anidación de carpetas no implica ninguna relación de contenido entre
`profesional/` e `ia/` o `idiomas/`, que permanecen totalmente aislados.

## Regla única de alcance repo-wide: enlaces cruzados entre vaults

Por defecto, cada vault es autónomo y sus wikilinks (`[[Página]]`) solo deben
apuntar a páginas de su propio vault — no mezcles taxonomías de `subtype` de
un dominio con otro.

Excepción explícita: **`profesional/` y `gestion-conocimiento/` pueden
enlazarse entre sí** cuando una página de uno realmente depende de un
concepto del otro (ej. un proceso de I+D que aplica un framework de gestión
del conocimiento). Reglas para estos enlaces cruzados:

- Se escriben como un wikilink normal `[[Nombre de Página]]` — Obsidian los
  resuelve igual siempre que los nombres de archivo sean únicos en todo el
  repositorio (ya lo son, por la convención de nomenclatura kebab-case).
- El enlace se anota siempre con el vault de destino entre paréntesis para
  que un lector humano no se confunda de dominio, ej:
  `[[Gestión del Conocimiento]] (vault: gestion-conocimiento)`.
- No aplica la regla de bidireccionalidad estricta de cada `CLAUDE.md` de
  carpeta a través de esta frontera — es decir, no es obligatorio que la
  página del otro vault liste esta de vuelta en su `related`, aunque es
  bienvenido si aporta valor de navegación.
- `idiomas/` e `ia/` no tienen esta excepción — se mantienen aislados salvo
  que el humano pida explícitamente lo contrario y lo documentemos aquí.

## Crear un vault nuevo

Si el humano pide un dominio nuevo sin relación con los existentes, créalo
como una carpeta hermana siguiendo exactamente la misma plantilla que las
demás (`CLAUDE.md`, `index.md`, `log.md`, `00_Meta/`, `10_Raw/`, `20_Wiki/`
con `entities/concepts/sources/synthesis`, `30_Queries/`, `40_Archive/`), y
añádelo a la tabla de arriba.
