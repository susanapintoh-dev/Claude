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

## [2026-07-24] ingest | Incentivos Tributarios para la CTI: Evidencia y Aprendizajes desde América Latina y Europa (BID/FI Group)
- Fuente: `10_Raw/incentivos-tributarios-cti-bid-borrador-2026-06-01.docx` —
  borrador consolidado, estudio conjunto BID (División de Competitividad,
  Tecnología e Innovación) y FI Group. Documento en construcción activa
  (Prefacio y Resumen Ejecutivo vacíos, notas editoriales sueltas en el
  cuerpo, numeración de recomendaciones con un salto de "quinta" a "séptima").
- Páginas creadas:
  - Fuente: [[Incentivos Tributarios para la CTI: Evidencia y Aprendizajes desde América Latina y Europa (BID/FI Group)]]
  - Síntesis: [[Incentivos Tributarios a la CTI: Análisis Comparado]]
  - Conceptos (`subtype: beneficio-tributario`): [[Crédit d'Impôt Recherche (Francia)]],
    [[Deducción Fiscal por I+D+i (España)]], [[SIFIDE (Portugal)]],
    [[Lei do Bem (Brasil)]], [[Incentivo Tributario a la Inversión en I+D (Chile)]],
    [[Beneficios Tributarios en CTI (Colombia)]]
  - Entidades (`subtype: organizacion`): [[Direction Générale des Finances Publiques (DGFiP)]],
    [[Ministère de l'Enseignement Supérieur et de la Recherche (MESR)]],
    [[Ministerio de Ciencia, Innovación y Universidades (MICIU)]],
    [[Agencia Estatal de Administración Tributaria (AEAT)]],
    [[Agência Nacional de Inovação (ANI)]], [[Autoridade Tributária e Aduaneira (Portugal)]],
    [[Ministério da Ciência, Tecnologia e Inovação (MCTI)]], [[Receita Federal do Brasil (RFB)]],
    [[Corporación de Fomento de la Producción (CORFO)]], [[Servicio de Impuestos Internos (SII)]],
    [[Ministerio de Ciencia, Tecnología e Innovación (MinCiencias)]],
    [[Dirección de Impuestos y Aduanas Nacionales (DIAN)]]
- Páginas actualizadas: [[Profesional]] (mapa de subtemas poblado), `index.md`.
- Notas: se detectó una inconsistencia en la propia fuente — la Tabla 1
  introductoria atribuye la certificación del incentivo chileno a la ANID,
  pero el estudio de caso completo de Chile usa CORFO consistentemente en
  todo momento. Documentado en [[Incentivo Tributario a la Inversión en I+D (Chile)]]
  y en la página de fuente; pendiente de aclarar con el equipo del BID. Al
  llegar una versión más nueva del estudio, se ingiere como actualización de
  esta misma fuente, comparando explícitamente qué cambió.
