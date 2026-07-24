# Bitácora

Registro cronológico, solo-anexo, de toda operación sobre este vault:
ingestas, consultas archivadas, lints y cambios de esquema. Nunca edites ni
borres una entrada existente — si algo se corrige, añade una entrada nueva
que lo indique.

Cada entrada empieza con el prefijo `## [YYYY-MM-DD] tipo | Título`, donde
`tipo` es `ingest`, `query`, `lint` o `meta`. Este prefijo consistente
permite inspeccionar el historial con herramientas unix, ej:

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

## [2026-07-24] meta | Creación del vault
- Cambio: se creó este vault (`profesional/`) como carpeta hermana dentro del
  monorepo, con su propio `CLAUDE.md`, taxonomía de `subtype` (politica,
  beneficio-tributario, mecanismo-financiacion, metodologia-valoracion,
  proceso, organizacion, autor, caso-de-estudio) y página hub [[Profesional]].
- Motivo: el humano pidió separar su investigación profesional (I+D+i,
  beneficios tributarios, financiamiento y valoración de la innovación) de
  gestión del conocimiento, manteniendo la posibilidad de enlaces cruzados
  intencionales entre ambos (ver `../CLAUDE.md`).
- Páginas/archivos afectados: `profesional/CLAUDE.md`, `profesional/index.md`,
  [[Profesional]], `../CLAUDE.md` (raíz, actualizado con el mapa de vaults).
