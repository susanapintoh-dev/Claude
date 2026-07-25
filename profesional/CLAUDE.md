# CLAUDE.md — Esquema de Gobernanza del Vault "Profesional"

Este archivo es la constitución operativa de este vault. Defines cómo lees,
escribes, enlazas y mantienes sus páginas markdown. No es documentación para
humanos: son reglas que debes seguir de forma estricta cada vez que proceses
una fuente, respondas una consulta o ejecutes un lint.

Este vault vive dentro de un monorepo de varios vaults independientes — ver
`../CLAUDE.md` (raíz) para el mapa completo y, sobre todo, para la regla de
enlaces cruzados con `gestion-conocimiento/` (los únicos permitidos hacia/desde
otro vault). Todo lo demás en este archivo aplica solo dentro de `profesional/`.

Nota de ubicación: `gestion-conocimiento/` vive físicamente anidada *dentro*
de esta carpeta (`profesional/gestion-conocimiento/`) para que el humano
pueda abrir `profesional/` como una única bóveda de Obsidian y ver ambos
vaults juntos, con los wikilinks cruzados resolviendo entre sí. Sigue siendo
un vault completamente independiente, gobernado por su propio
`gestion-conocimiento/CLAUDE.md` — no es una subcarpeta temática de este vault.

## 1. Propósito y Alcance

Este vault es la base de investigación profesional para entender
**ecosistemas de ciencia, tecnología e innovación**: cómo se financia la
I+D+i empresarial (mecanismos de financiamiento, beneficios tributarios,
capital de riesgo, convocatorias), qué metodologías existen para valorar la
innovación, cómo funcionan los procesos operativos de I+D, y qué
oportunidades y normativas concretas existen país por país. Toda decisión
de categorización debe tomarse pensando en qué hace más fácil comparar y
conectar ideas dentro de este dominio (ej. comparar dos beneficios
tributarios entre sí, relacionar un mecanismo de financiamiento con la
política que lo habilita, o contrastar la normativa de dos países).

Este dominio se solapa genuinamente con gestión del conocimiento (la gestión
de la innovación y de I+D usa marcos de KM). Por eso — y solo con ese vault —
están permitidos los enlaces cruzados descritos en `../CLAUDE.md`.

El wiki tiene tres capas. Nunca mezcles su rol:

| Capa | Carpeta | Quién escribe | Mutabilidad |
|---|---|---|---|
| Fuentes crudas | `10_Raw/` | El humano (curación) | Inmutable — nunca edites ni borres nada aquí |
| Wiki | `20_Wiki/` | Tú (el LLM) | Vivo — lo creas, actualizas y refactorizas |
| Meta / esquema | `00_Meta/`, `CLAUDE.md` | Humano + LLM en colaboración | Evoluciona con el proyecto |
| Consultas archivadas | `30_Queries/` | Tú, a petición del humano | Vivo |
| Archivo histórico | `40_Archive/` | Tú, cuando una página queda superada | Solo-anexo (no se borra) |

## 2. Reglas de Frontmatter (YAML)

Toda página en `20_Wiki/` y `30_Queries/` DEBE empezar con frontmatter YAML.
Campos obligatorios para cualquier tipo de página:

```yaml
---
title: "Título exacto de la página"
type: entity | concept | source | synthesis | query
subtype: ""      # solo entity/concept — ver tabla de subtipos abajo
pais: ""         # solo si la página es específica de un país — ver regla 2
status: draft | stable | superseded
created: YYYY-MM-DD
updated: YYYY-MM-DD
aliases: []
tags: []
related: []      # wikilinks a otras páginas del vault, ej: "[[Nombre de Página]]"
sources: []      # rutas o enlaces a las fuentes crudas en 10_Raw/ que respaldan esta página
---
```

Reglas adicionales por tipo:

- **`source`** (páginas en `20_Wiki/sources/`): añade `source_path` (ruta exacta en
  `10_Raw/`) y `source_date` (fecha de publicación/origen de la fuente, si se conoce).
- **`entity`** / **`concept`**: `related` debe listar toda página que la mencione o
  sea mencionada por ella — el enlace debe ser bidireccional (ver regla 4). Además,
  DEBE llevar `subtype` con uno de estos valores controlados:

  | `subtype` | Se usa para | Tipo (`type`) típico |
  |---|---|---|
  | `politica` | Políticas públicas de I+D+i (leyes, marcos regulatorios, CONPES) | `concept` |
  | `beneficio-tributario` | Incentivos fiscales concretos (deducciones, exenciones, créditos) | `concept` |
  | `mecanismo-financiacion` | Instrumentos de financiamiento (fondos, convocatorias, capital de riesgo) | `concept` |
  | `metodologia-valoracion` | Métodos de valoración de la innovación / intangibles | `concept` |
  | `proceso` | Procesos operativos de I+D (gestión de proyectos, stage-gate, vigilancia tecnológica) | `concept` |
  | `organizacion` | Entidades (ministerios, agencias, empresas, universidades) | `entity` |
  | `autor` | Personas relevantes del campo | `entity` |
  | `caso-de-estudio` | Aplicaciones documentadas en un contexto real | `entity` |

  Si una página nueva no encaja en ningún valor de esta tabla, propón al humano un
  `subtype` nuevo antes de usarlo y añádelo aquí si se aprueba.
- **`query`** (páginas en `30_Queries/`): añade `question` (la pregunta original tal
  como se formuló).
- **Campo `pais`** (cualquier `type`): cuando una página trate sobre un único
  país (una política, un beneficio tributario, una entidad ejecutora, un
  caso de estudio nacional), DEBE llevar `pais` con el nombre del país en
  español, mayúscula inicial (ej. `"Colombia"`, `"Perú"`, `"Chile"`,
  `"Francia"`, `"España"`, `"Brasil"`, `"Portugal"`). Esto permite filtrar y
  consultar por país con Dataview sin depender de subcarpetas por país —
  este vault se organiza por tipo de página (`entities/concepts/sources/synthesis`),
  no por país. Páginas que comparan o abarcan varios países (ej. una
  síntesis comparada, o el estudio fuente del que salen) dejan `pais` vacío
  o lo omiten — su alcance multi-país ya es evidente en el cuerpo del texto.

Nunca dejes `updated` desactualizado tras una edición. Nunca inventes un campo fuera
de este esquema sin proponerlo antes al humano y documentarlo aquí.

## 3. Reglas de Nomenclatura y Formato

- Nombre de archivo en `kebab-case` y en el mismo idioma que el contenido de la
  página, ej: `20_Wiki/concepts/deduccion-fiscal-por-inversion-en-id.md`.
- El nombre de archivo debe corresponder al `title` del frontmatter.
- El H1 (`# Título`) debe repetir exactamente el `title` del frontmatter.
- Usa wikilinks `[[Nombre de Página]]` para cualquier mención a otra página del
  vault — nunca uses rutas relativas markdown para enlaces internos.
- Cita las fuentes crudas como rutas relativas normales:
  `[fuente](../../10_Raw/documento.md)`, nunca como wikilink.
- Estructura de secciones recomendada:
  1. Resumen (1–3 líneas)
  2. Cuerpo (secciones temáticas)
  3. `## Contradicciones / Preguntas abiertas` (si aplica)
  4. `## Fuentes` (lista de fuentes citadas)
  5. `## Ver también` (enlaces relacionados, incluyendo cruces a `gestion-conocimiento/` si aplica)

## 4. Reglas de Enlazado

- Todo enlace debe ser bidireccional dentro de este vault: si A enlaza a B, B
  debe listar A en su `related` y, si es relevante, en `## Ver también`.
- Antes de crear una página nueva, busca en `index.md` si ya existe una
  equivalente. Prefiere actualizar sobre duplicar.
- Ninguna página nueva debe quedar huérfana: toda página creada debe enlazarse
  desde al menos otra página existente y desde `index.md`.
- Enlaces a `gestion-conocimiento/`: siguen la regla del `CLAUDE.md` raíz — no
  requieren bidireccionalidad estricta, pero anota siempre el vault de destino.

## 5. Reglas de Actualización y Contradicciones

- Nunca borres contenido para "corregirlo". Si una fuente nueva contradice o
  reemplaza una afirmación anterior:
  - Si queda obsoleta por completo, marca `status: superseded`, deja una nota
    breve explicando por qué y qué la reemplaza, y enlaza a la página vigente.
  - Si es una contradicción sin resolver (ej. dos metodologías de valoración en
    desacuerdo), documenta ambas versiones en `## Contradicciones / Preguntas
    abiertas` con su fuente respectiva — no elijas ganadora sin que el humano lo decida.
- Toda página `superseded` se conserva; si ya no aporta valor de navegación,
  muévela a `40_Archive/`.

## 6. Flujo de Ingesta

1. Lee la fuente completa en `10_Raw/` (normativa, informe, artículo, etc.).
2. Discute con el humano los puntos clave antes de escribir nada.
3. Crea o actualiza la página `source` correspondiente en `20_Wiki/sources/`.
4. Actualiza toda página `entity`/`concept`/`synthesis` afectada.
5. Actualiza `index.md`.
6. Añade una entrada en `log.md` (ver sección 9).

## 7. Flujo de Consulta

1. Lee `index.md` primero para localizar páginas relevantes.
2. Profundiza solo en las páginas pertinentes.
3. Sintetiza citando páginas del vault y, cuando corresponda, la fuente cruda.
4. Si la respuesta tiene valor duradero, pregunta si debe archivarse en `30_Queries/`.
5. Si se archiva, actualiza `index.md` y `log.md`.

## 8. Flujo de Lint

- Contradicciones no documentadas.
- Beneficios/políticas desactualizados por normativa más reciente.
- Páginas huérfanas.
- Conceptos mencionados repetidamente sin página propia.
- Referencias cruzadas rotas.
- Páginas `entity`/`concept` sin `subtype` válido.
- `beneficio-tributario` o `mecanismo-financiacion` sin su `politica` habilitante enlazada.
- Conexiones no tejidas con `gestion-conocimiento/` cuando un proceso de I+D
  claramente aplica un framework de ese vault.
- Páginas específicas de un país sin campo `pais`, o con un valor que no
  coincide con el nombre usado en otras páginas del mismo país (ej.
  `"Perú"` vs. `"Peru"` sin tilde).

## 9. Mantenimiento de `index.md` y `log.md`

- **Toda** operación que cree o modifique una página en `20_Wiki/` o
  `30_Queries/` debe terminar con una actualización de `index.md` y una
  entrada nueva en `log.md` (siempre, sin excepción).
- `log.md` es solo-anexo: nunca edites ni borres entradas pasadas.
