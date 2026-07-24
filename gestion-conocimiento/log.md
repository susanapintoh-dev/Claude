# Bitácora

Registro cronológico, solo-anexo, de toda operación sobre el wiki: ingestas,
consultas archivadas y lints. Nunca edites ni borres una entrada existente —
si algo se corrige, añade una entrada nueva que lo indique.

Cada entrada empieza con el prefijo `## [YYYY-MM-DD] tipo | Título`, donde
`tipo` es `ingest`, `query`, `lint` o `meta` (cambios al esquema/gobernanza en
`CLAUDE.md` — ver regla 1). Este prefijo consistente permite inspeccionar el
historial con herramientas unix, ej:

```sh
grep "^## \[" log.md | tail -5
```

Plantilla de entrada:

```markdown
## [YYYY-MM-DD] ingest | Título de la fuente
- Fuente: ruta en 10_Raw/
- Páginas creadas: [[Página A]], [[Página B]]
- Páginas actualizadas: [[Página C]]
- Notas: contradicciones detectadas, decisiones tomadas, etc.
```

```markdown
## [YYYY-MM-DD] query | Pregunta resumida
- Páginas consultadas: [[Página A]], [[Página B]]
- Archivada como: [[30_Queries/...]] (o "no archivada")
```

```markdown
## [YYYY-MM-DD] lint | Alcance del chequeo
- Hallazgos: ...
- Correcciones aplicadas: ...
- Pendiente de decisión humana: ...
```

```markdown
## [YYYY-MM-DD] meta | Cambio de esquema
- Cambio: ...
- Motivo: ...
- Páginas/archivos afectados: ...
```

---

## [2026-07-21] meta | Alcance del vault: gestión del conocimiento y taxonomía de subtipos
- Cambio: se añadió la sección 1 (Propósito y Alcance) a `CLAUDE.md`, declarando
  el vault como dedicado específicamente a investigación sobre gestión del
  conocimiento; se añadió el campo `subtype` (controlado: `teoria`, `framework`,
  `metodologia`, `herramienta`, `autor`, `organizacion`, `caso-de-estudio`) para
  páginas `entity`/`concept`; se renumeraron las secciones 2–9 de `CLAUDE.md`.
- Motivo: petición explícita del humano de especializar el vault para poder
  consultarlo con facilidad y conectar ideas del dominio entre sí.
- Páginas/archivos afectados: `CLAUDE.md`, `index.md` (nota de alcance + columna
  `Subtipo` en Entidades/Conceptos), [[Gestión del Conocimiento]] (página hub
  nueva en `20_Wiki/synthesis/`).

## [2026-07-24] meta | Migración a monorepo multi-vault
- Cambio: este vault se movió de la raíz del repositorio a la carpeta
  `gestion-conocimiento/` (todo su contenido intacto: `CLAUDE.md`, `index.md`,
  `log.md`, `00_Meta/`, `10_Raw/`, `20_Wiki/`, `30_Queries/`, `40_Archive/`).
  El repositorio ahora aloja varios vaults hermanos (`profesional/`,
  `idiomas/`, `ia/`), cada uno con su propio `CLAUDE.md`; un `CLAUDE.md` nuevo
  en la raíz del repo actúa como mapa y define la regla de enlaces cruzados
  con `profesional/` (única excepción al aislamiento entre vaults). Se añadió
  un enlace cruzado inicial de [[Gestión del Conocimiento]] hacia [[Profesional]].
- Motivo: el humano quiere organizar temáticas no relacionadas (gestión del
  conocimiento, profesional/I+D+i, idiomas, IA) sin diluir la taxonomía de
  `subtype` de cada dominio, manteniendo la opción de conectar ideas entre
  gestión del conocimiento y su vault profesional cuando sea genuinamente relevante.
- Páginas/archivos afectados: ruta completa del vault (sin cambios de
  contenido más allá de la ubicación), `../CLAUDE.md` (nuevo, raíz), `../README.md`
  (nuevo, mapa de vaults), [[Gestión del Conocimiento]] (nuevo enlace de salida).
