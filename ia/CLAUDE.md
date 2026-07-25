# CLAUDE.md — Esquema de Gobernanza del Vault "IA"

Este archivo es la constitución operativa de este vault. Defines cómo lees,
escribes, enlazas y mantienes sus páginas markdown. No es documentación para
humanos: son reglas que debes seguir de forma estricta cada vez que proceses
una fuente, respondas una consulta o ejecutes un lint.

Este vault vive dentro de un monorepo de varios vaults independientes — ver
`../CLAUDE.md` (raíz) para el mapa completo. Este vault **no tiene excepción
de enlace cruzado** con ningún otro (a diferencia de `profesional/` ↔
`gestion-conocimiento/`); se mantiene aislado salvo que el humano pida lo
contrario y lo documentemos en `../CLAUDE.md`.

## 1. Propósito y Alcance

Este vault es la base para entender **inteligencia artificial** de manera
integral: conceptos técnicos, modelos concretos, herramientas/frameworks,
organizaciones/laboratorios, investigadores, publicaciones seminales y casos
de estudio de aplicación práctica. Las fuentes crudas en `10_Raw/` vienen de
investigación propia, clases, artículos y otros recursos por igual — el
flujo de ingesta (regla 6) trata "una clase de hoy" con el mismo cuidado que
un paper. El humano está aprendiendo IA de forma continua (a diario), así
que este vault debe optimizarse para acumular entendimiento incremental —
cada fuente nueva debe conectarse con lo que ya existe, no quedar aislada.

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
related: []      # wikilinks a otras páginas del vault, ej: "[[Nombre de Página]]"
sources: []      # rutas o enlaces a las fuentes crudas en 10_Raw/ que respaldan esta página
---
```

Reglas adicionales por tipo:

- **`source`** (páginas en `20_Wiki/sources/`): añade `source_path` (ruta
  exacta en `10_Raw/`) y `source_date`.
- **`entity`** / **`concept`**: `related` debe listar toda página que la
  mencione o sea mencionada por ella — bidireccional (ver regla 4). Además,
  DEBE llevar `subtype` con uno de estos valores controlados:

  | `subtype` | Se usa para | Tipo (`type`) típico |
  |---|---|---|
  | `concepto-tecnico` | Conceptos y técnicas (ej. attention, RAG, fine-tuning) | `concept` |
  | `modelo` | Modelos de IA concretos (ej. Claude, GPT-4, Llama) | `entity` |
  | `herramienta` | Frameworks/herramientas (ej. LangChain, Claude Code) | `entity` |
  | `organizacion` | Empresas/laboratorios de IA | `entity` |
  | `autor` | Investigadores/pensadores | `entity` |
  | `publicacion` | Papers o publicaciones seminales tratados como entidad propia | `entity` |
  | `caso-de-estudio` | Aplicaciones prácticas documentadas | `entity` |

  Si una página nueva no encaja en ningún valor de esta tabla, propón al
  humano un `subtype` nuevo antes de usarlo y añádelo aquí si se aprueba.
- **`query`** (páginas en `30_Queries/`): añade `question`.

Nunca dejes `updated` desactualizado tras una edición. Nunca inventes un campo
fuera de este esquema sin proponerlo antes al humano y documentarlo aquí.

## 3. Reglas de Nomenclatura y Formato

- Nombre de archivo en `kebab-case`, ej: `20_Wiki/concepts/mecanismo-de-atencion.md`.
- El nombre de archivo debe corresponder al `title` del frontmatter.
- El H1 (`# Título`) debe repetir exactamente el `title`.
- Usa wikilinks `[[Nombre de Página]]` para menciones a otras páginas del
  vault — nunca rutas relativas markdown para enlaces internos.
- Cita las fuentes crudas como rutas relativas normales:
  `[fuente](../../10_Raw/documento.md)`, nunca como wikilink.
- Estructura de secciones recomendada:
  1. Resumen (1–3 líneas)
  2. Cuerpo (secciones temáticas)
  3. `## Contradicciones / Preguntas abiertas` (si aplica — ej. benchmarks en desacuerdo)
  4. `## Fuentes`
  5. `## Ver también`

## 4. Reglas de Enlazado

- Todo enlace debe ser bidireccional: si A enlaza a B, B debe listar A en su
  `related` y, si es relevante, en `## Ver también`.
- Antes de crear una página nueva, busca en `index.md` si ya existe una
  equivalente. Prefiere actualizar sobre duplicar.
- Ninguna página nueva debe quedar huérfana: enlázala desde al menos otra
  página existente y desde `index.md`.
- Si un `modelo` usa una `herramienta` o implementa un `concepto-tecnico`,
  enlázalos explícitamente — esa es la conexión más valiosa de este vault.

## 5. Reglas de Actualización y Contradicciones

- Nunca borres contenido para "corregirlo". El campo se mueve rápido: si un
  modelo nuevo o un paper reciente contradice o reemplaza una afirmación:
  - Si queda obsoleta por completo, marca `status: superseded`, deja una nota
    breve explicando por qué y qué la reemplaza, y enlaza a la página vigente.
  - Si es una contradicción sin resolver (ej. benchmarks contradictorios entre
    labs), documenta ambas versiones en `## Contradicciones / Preguntas
    abiertas` con su fuente — no elijas ganadora sin que el humano lo decida.
- Toda página `superseded` se conserva; muévela a `40_Archive/` si ya no
  aporta valor de navegación.

## 6. Flujo de Ingesta

1. Lee la fuente completa en `10_Raw/` (paper, artículo, post técnico, video/transcripción).
2. Discute con el humano los puntos clave antes de escribir nada.
3. Crea o actualiza la página `source` en `20_Wiki/sources/`.
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

- Contradicciones no documentadas (ej. benchmarks o afirmaciones de capacidad
  desactualizadas por un modelo/paper más reciente).
- Páginas huérfanas.
- Conceptos técnicos mencionados repetidamente sin página propia.
- Referencias cruzadas rotas.
- Páginas `entity`/`concept` sin `subtype` válido.
- `modelo` sin ninguna `herramienta` o `concepto-tecnico` enlazado — señal de
  que falta profundizar en cómo funciona.

## 9. Mantenimiento de `index.md` y `log.md`

- **Toda** operación que cree o modifique una página en `20_Wiki/` o
  `30_Queries/` debe terminar con una actualización de `index.md` y una
  entrada nueva en `log.md` (siempre, sin excepción).
- `log.md` es solo-anexo: nunca edites ni borres entradas pasadas.
