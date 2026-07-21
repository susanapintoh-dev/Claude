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
