# CLAUDE.md — Esquema de Gobernanza del Vault "Idiomas"

Este archivo es la constitución operativa de este vault. Defines cómo lees,
escribes, enlazas y mantienes sus páginas markdown. No es documentación para
humanos: son reglas que debes seguir de forma estricta cada vez que proceses
una fuente, respondas una consulta o ejecutes un lint.

Este vault vive dentro de un monorepo de varios vaults independientes — ver
`../CLAUDE.md` (raíz) para el mapa completo. A diferencia de `profesional/` y
`gestion-conocimiento/`, este vault **no tiene excepción de enlace cruzado**:
se mantiene aislado salvo que el humano pida lo contrario.

## 1. Propósito y Alcance

Este vault es la base de aprendizaje personal de **francés y portugués**:
gramática, vocabulario, expresiones, pronunciación y recursos (libros, apps,
cursos, tutores). El objetivo es poder consultar una regla o una lista de
vocabulario de forma aislada, y a la vez que el vault revele paralelismos y
"falsos amigos" entre los dos idiomas — comparaciones que no serían obvias
estudiando cada idioma por separado.

Como ambos idiomas conviven en el mismo vault, toda página DEBE declarar a
qué idioma pertenece con el campo `idioma` (ver regla 2) — esto es lo que
permite filtrar por idioma o, al contrario, cruzar ambos en una página de
tipo `synthesis` con `idioma: comparado`.

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
idioma: frances | portugues | comparado   # obligatorio en entity/concept/synthesis
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

- **`source`** (páginas en `20_Wiki/sources/`): añade `source_path` y
  `source_date`. No requiere `idioma` (una fuente puede cubrir ambos).
- **`entity`** / **`concept`** / **`synthesis`**: `related` debe listar toda
  página que la mencione o sea mencionada por ella — bidireccional (ver
  regla 4). DEBEN llevar `idioma` y (entity/concept) `subtype` de esta tabla:

  | `subtype` | Se usa para | Tipo (`type`) típico |
  |---|---|---|
  | `gramatica` | Reglas y estructuras gramaticales (ej. subjuntivo, concordancia) | `concept` |
  | `vocabulario` | Campos léxicos / listas de palabras temáticas | `concept` |
  | `expresion` | Modismos y expresiones idiomáticas | `concept` |
  | `pronunciacion` | Reglas fonéticas y de pronunciación | `concept` |
  | `recurso` | Libros, apps, cursos, tutores | `entity` |

  Usa `idioma: comparado` únicamente en páginas que contrastan francés y
  portugués explícitamente (ej. falsos amigos, diferencias de conjugación).
  Si una página nueva no encaja en ningún `subtype` de esta tabla, propón al
  humano uno nuevo antes de usarlo.
- **`query`** (páginas en `30_Queries/`): añade `question`.

Nunca dejes `updated` desactualizado tras una edición. Nunca inventes un campo
fuera de este esquema sin proponerlo antes al humano y documentarlo aquí.

## 3. Reglas de Nomenclatura y Formato

- Nombre de archivo en `kebab-case`, en español (idioma de trabajo del vault)
  aunque el contenido cite palabras en francés/portugués, ej:
  `20_Wiki/concepts/subjuntivo-presente-frances.md`.
- El nombre de archivo debe corresponder al `title` del frontmatter.
- El H1 (`# Título`) debe repetir exactamente el `title`.
- Usa wikilinks `[[Nombre de Página]]` para menciones a otras páginas del
  vault — nunca rutas relativas markdown para enlaces internos.
- Cita las fuentes crudas como rutas relativas normales:
  `[fuente](../../10_Raw/documento.md)`, nunca como wikilink.
- Estructura de secciones recomendada:
  1. Resumen (1–3 líneas)
  2. Cuerpo (secciones temáticas — ejemplos, tabla de conjugación, etc.)
  3. `## Contradicciones / Preguntas abiertas` (si aplica, ej. reglas con excepciones)
  4. `## Fuentes`
  5. `## Ver también` (incluye la página equivalente del otro idioma si existe)

## 4. Reglas de Enlazado

- Todo enlace debe ser bidireccional: si A enlaza a B, B debe listar A en su
  `related` y, si es relevante, en `## Ver también`.
- Antes de crear una página nueva, busca en `index.md` si ya existe una
  equivalente. Prefiere actualizar sobre duplicar.
- Ninguna página nueva debe quedar huérfana: enlázala desde al menos otra
  página existente y desde `index.md`.
- Si una regla de francés y su equivalente en portugués divergen o coinciden
  de forma interesante, considera crear o actualizar una página
  `idioma: comparado` que enlace a ambas.

## 5. Reglas de Actualización y Contradicciones

- Nunca borres contenido para "corregirlo". Si aprendes una excepción o
  matiz nuevo sobre una regla ya documentada, añádelo — no reescribas sin
  dejar rastro.
- Si dos fuentes (ej. dos profesores, dos apps) dan reglas distintas para lo
  mismo, documenta ambas en `## Contradicciones / Preguntas abiertas` sin
  elegir ganadora sin que el humano lo decida.
- Toda página `superseded` se conserva; muévela a `40_Archive/` si ya no
  aporta valor de navegación.

## 6. Flujo de Ingesta

1. Lee la fuente completa en `10_Raw/` (lección, apunte, artículo, video/transcripción).
2. Discute con el humano los puntos clave antes de escribir nada.
3. Crea o actualiza la página `source` en `20_Wiki/sources/`.
4. Actualiza toda página `entity`/`concept`/`synthesis` afectada, en el
   idioma correspondiente.
5. Actualiza `index.md`.
6. Añade una entrada en `log.md` (ver sección 9).

## 7. Flujo de Consulta

1. Lee `index.md` primero para localizar páginas relevantes (filtra mental o
   literalmente por `idioma`).
2. Profundiza solo en las páginas pertinentes.
3. Sintetiza citando páginas del vault.
4. Si la respuesta tiene valor duradero (ej. una comparación francés↔portugués),
   pregunta si debe archivarse en `30_Queries/`.
5. Si se archiva, actualiza `index.md` y `log.md`.

## 8. Flujo de Lint

- Páginas sin campo `idioma`.
- Páginas `entity`/`concept` sin `subtype` válido.
- Reglas gramaticales de un idioma sin verificar si existe equivalente en el
  otro — oportunidad de crear una página `comparado`.
- Páginas huérfanas o referencias cruzadas rotas.
- Vacíos de vocabulario/gramática que podrían llenarse con una fuente nueva.

## 9. Mantenimiento de `index.md` y `log.md`

- **Toda** operación que cree o modifique una página en `20_Wiki/` o
  `30_Queries/` debe terminar con una actualización de `index.md` y una
  entrada nueva en `log.md` (siempre, sin excepción).
- `log.md` es solo-anexo: nunca edites ni borres entradas pasadas.
