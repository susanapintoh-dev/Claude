# Bitácora

Registro cronológico, solo-anexo, de toda operación sobre el wiki: ingestas,
consultas archivadas y lints. Nunca edites ni borres una entrada existente —
si algo se corrige, añade una entrada nueva que lo indique.

Cada entrada empieza con el prefijo `## [YYYY-MM-DD] tipo | Título`, donde
`tipo` es `ingest`, `query` o `lint`. Este prefijo consistente permite
inspeccionar el historial con herramientas unix, ej:

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

---

_(sin entradas todavía — la primera ingesta o consulta añade la primera línea aquí)_
