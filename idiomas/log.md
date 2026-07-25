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
- Idioma: frances | portugues
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
- Cambio: se creó este vault (`idiomas/`) como carpeta hermana dentro del
  monorepo, con su propio `CLAUDE.md`, campo obligatorio `idioma` (frances,
  portugues, comparado), taxonomía de `subtype` (gramatica, vocabulario,
  expresion, pronunciacion, recurso) y página hub [[Idiomas]].
- Motivo: el humano quiere estudiar francés y portugués en un vault propio,
  aislado de los demás dominios, con la posibilidad de tejer comparaciones
  entre ambos idiomas mediante `idioma: comparado`.
- Páginas/archivos afectados: `idiomas/CLAUDE.md`, `idiomas/index.md`,
  [[Idiomas]], `../CLAUDE.md` (raíz, mapa de vaults).

## [2026-07-25] meta | Refinamiento del propósito
- Cambio: se precisó la sección 1 (Propósito y Alcance) de `CLAUDE.md` —
  las fuentes crudas de este vault serán sobre todo material de clase
  (apuntes propios, guías del profesor, ejercicios), no solo artículos
  externos; el flujo de ingesta trata "la clase de hoy" igual que cualquier
  otra fuente.
- Motivo: el humano aclaró que este vault guardará específicamente la
  información de sus clases de francés y portugués y sus propios apuntes.
- Páginas/archivos afectados: `idiomas/CLAUDE.md`.
