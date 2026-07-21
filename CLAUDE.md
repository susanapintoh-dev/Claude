# CLAUDE.md — Esquema de Gobernanza del Wiki

Este archivo es la constitución operativa del wiki. Defines cómo lees, escribes,
enlazas y mantienes las páginas markdown de este repositorio. No es documentación
para humanos: son reglas que debes seguir de forma estricta cada vez que proceses
una fuente, respondas una consulta o ejecutes un lint.

## 1. Propósito y Alcance

Este vault es específicamente la base de investigación personal sobre **gestión
del conocimiento** (knowledge management): teorías, modelos, frameworks,
metodologías, herramientas, autores/pensadores y casos de estudio del campo, más
las conexiones entre todos ellos. No es un vault de propósito general — toda
decisión de categorización (ver `subtype` en la regla 2) debe tomarse pensando en
qué hace más fácil comparar y conectar ideas dentro de este dominio.

El objetivo explícito es doble: (1) que cualquier página pueda consultarse de
forma aislada y autosuficiente, y (2) que el conjunto del wiki revele conexiones
entre ideas que no serían obvias leyendo las fuentes por separado — esa síntesis
es el valor que este vault añade sobre las fuentes crudas.

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
status: draft | stable | superseded
created: YYYY-MM-DD
updated: YYYY-MM-DD
aliases: []
tags: []
related: []      # wikilinks a otras páginas del wiki, ej: "[[Nombre de Página]]"
sources: []      # rutas o enlaces a las fuentes crudas en 10_Raw/ que respaldan esta página
---
```

Reglas adicionales por tipo:

- **`source`** (páginas en `20_Wiki/sources/`): añade `source_path` (ruta exacta en
  `10_Raw/`) y `source_date` (fecha de publicación/origen de la fuente, si se conoce).
- **`entity`** / **`concept`**: `related` debe listar toda página que la mencione o
  sea mencionada por ella — el enlace debe ser bidireccional (ver regla 4). Además,
  DEBE llevar `subtype` con uno de estos valores controlados (propios del dominio
  de gestión del conocimiento):

  | `subtype` | Se usa para | Tipo (`type`) típico |
  |---|---|---|
  | `teoria` | Teorías explicativas (ej. creación de conocimiento, aprendizaje organizacional) | `concept` |
  | `framework` | Modelos/frameworks estructurados (ej. SECI, DIKW) | `concept` |
  | `metodologia` | Prácticas o procesos aplicados (ej. comunidades de práctica, retrospectivas) | `concept` |
  | `herramienta` | Software o sistemas concretos (ej. Obsidian, un wiki interno) | `entity` |
  | `autor` | Personas — pensadores, investigadores, practicantes | `entity` |
  | `organizacion` | Empresas, instituciones, comunidades | `entity` |
  | `caso-de-estudio` | Aplicaciones documentadas en un contexto real | `entity` |

  Si una página nueva no encaja en ningún valor de esta tabla, propón al humano un
  `subtype` nuevo antes de usarlo y añádelo aquí si se aprueba — no inventes valores
  sueltos.
- **`query`** (páginas en `30_Queries/`): añade `question` (la pregunta original tal
  como se formuló).

Nunca dejes `updated` desactualizado tras una edición. Nunca inventes un campo fuera
de este esquema sin proponerlo antes al humano y documentarlo aquí.

## 3. Reglas de Nomenclatura y Formato

- Nombre de archivo en `kebab-case` y en el mismo idioma que el contenido de la
  página, ej: `20_Wiki/entities/juan-perez.md`.
- El nombre de archivo debe corresponder al `title` del frontmatter (sin tildes ni
  caracteres especiales, pero el `title` sí puede llevarlos).
- El H1 (`# Título`) debe repetir exactamente el `title` del frontmatter.
- Usa wikilinks `[[Nombre de Página]]` para cualquier mención a otra página del
  wiki — nunca uses rutas relativas markdown (`[texto](ruta.md)`) para enlaces
  internos del wiki.
- Cita las fuentes crudas como rutas relativas normales:
  `[fuente](../../10_Raw/articulo.md)`, nunca como wikilink.
- Estructura de secciones recomendada (adapta según el tipo de página, pero no
  reordenes sin razón — la consistencia ayuda a la navegación):
  1. Resumen (1–3 líneas)
  2. Cuerpo (secciones temáticas)
  3. `## Contradicciones / Preguntas abiertas` (si aplica)
  4. `## Fuentes` (lista de fuentes citadas)
  5. `## Ver también` (enlaces relacionados no cubiertos ya en el cuerpo)

## 4. Reglas de Enlazado

- Todo enlace debe ser bidireccional: si la página A enlaza a B, B debe listar A en
  su `related` (frontmatter) y, si es relevante, en su sección `## Ver también`.
- Antes de crear una página nueva, busca en `index.md` si ya existe una página
  equivalente. Prefiere actualizar sobre duplicar.
- Ninguna página nueva debe quedar huérfana: toda página creada debe enlazarse desde
  al menos otra página existente y desde `index.md`.
- Si un concepto se menciona repetidamente sin tener página propia, propón al humano
  crear una página dedicada en el siguiente lint.

## 5. Reglas de Actualización y Contradicciones

- Nunca borres contenido para "corregirlo". Si una fuente nueva contradice o
  reemplaza una afirmación anterior:
  - Si la afirmación anterior queda obsoleta por completo, marca la página con
    `status: superseded`, deja una nota breve explicando por qué y qué la
    reemplaza, y enlaza a la página vigente.
  - Si es una contradicción sin resolver (dos fuentes en desacuerdo), documenta
    ambas versiones en `## Contradicciones / Preguntas abiertas` con su fuente
    respectiva — no elijas una ganadora sin que el humano lo decida.
- Toda página movida a estado `superseded` se conserva (no se borra el archivo);
  si ya no aporta valor de navegación, muévela a `40_Archive/` conservando su
  historial de frontmatter.

## 6. Flujo de Ingesta

Cuando el humano indique procesar una fuente nueva en `10_Raw/`:

1. Lee la fuente completa (y las imágenes asociadas si existen, en una pasada
   separada — ver nota de imágenes más abajo).
2. Discute con el humano los puntos clave antes de escribir nada (a menos que se
   pida ingesta por lote sin supervisión).
3. Crea o actualiza la página `source` correspondiente en `20_Wiki/sources/`.
4. Actualiza toda página de `entity`/`concept`/`synthesis` afectada por la nueva
   información — no te limites a la página de la fuente.
5. Actualiza `index.md` con cualquier página nueva o modificada.
6. Añade una entrada en `log.md` (ver formato en la sección 9).

Nota sobre imágenes: no puedes leer markdown con imágenes inline en una sola
pasada. Lee primero el texto, luego revisa las imágenes referenciadas por separado
si aportan contexto necesario.

## 7. Flujo de Consulta

Cuando el humano haga una pregunta contra el wiki:

1. Lee `index.md` primero para localizar páginas relevantes antes de leer
   contenido completo.
2. Profundiza solo en las páginas pertinentes.
3. Sintetiza una respuesta citando las páginas del wiki (wikilinks) y, cuando
   corresponda, la fuente cruda original.
4. Si la respuesta tiene valor duradero (una comparación, un análisis, una
   conexión nueva), pregunta al humano si debe archivarse como página nueva en
   `30_Queries/` siguiendo las reglas de frontmatter y enlazado ya descritas.
5. Si se archiva, actualiza `index.md` y `log.md` igual que en una ingesta.

## 8. Flujo de Lint

Cuando el humano pida un chequeo de salud del wiki, revisa:

- Contradicciones entre páginas no documentadas.
- Afirmaciones desactualizadas por fuentes más recientes.
- Páginas huérfanas (sin enlaces entrantes).
- Conceptos mencionados repetidamente sin página propia.
- Referencias cruzadas faltantes o rotas (wikilinks a páginas inexistentes).
- Vacíos de información que podrían llenarse con una fuente nueva o búsqueda web.
- Páginas `entity`/`concept` sin `subtype` o con un `subtype` fuera de la tabla
  de la regla 2.
- Páginas del mismo `subtype` que nunca se comparan entre sí en ninguna síntesis
  (ej. dos `framework` sin una página que los contraste) — señal de una conexión
  todavía sin tejer.

Reporta hallazgos al humano antes de aplicar cambios masivos; aplica solo las
correcciones triviales (enlaces rotos, `updated` desactualizado) de forma directa.
Registra el lint en `log.md` con las páginas tocadas.

## 9. Mantenimiento de `index.md` y `log.md`

Ver `index.md` y `log.md` para su estructura exacta. Regla general:

- **Toda** operación que cree o modifique una página en `20_Wiki/` o `30_Queries/`
  debe terminar con una actualización de `index.md` (si cambia el catálogo) y una
  entrada nueva en `log.md` (siempre, sin excepción).
- `log.md` es solo-anexo: nunca edites ni borres entradas pasadas.
