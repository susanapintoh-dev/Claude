# Vault personal (monorepo)

Repositorio de bases de conocimiento personales, mantenidas por un LLM: para
cada dominio, las fuentes crudas son inmutables, el wiki lo escribe y
mantiene el LLM, y las reglas de todo el proceso viven en cada `CLAUDE.md`.

Cada carpeta de vault es independiente, con su propio `CLAUDE.md`, catálogo
(`index.md`) y bitácora (`log.md`). Para abrir esto en Obsidian, se recomienda
usar **3 bóvedas separadas** (una por carpeta abierta de forma independiente):

- **[`profesional/`](profesional/index.md)** — ecosistemas de ciencia, tecnología e innovación: financiamiento de I+D+i empresarial, beneficios tributarios, valoración de la innovación, normativas por país.
  - **[`profesional/gestion-conocimiento/`](profesional/gestion-conocimiento/index.md)** — anidado a propósito dentro de `profesional/` para que ambos wikis compartan una misma bóveda de Obsidian y sus enlaces cruzados funcionen; sigue siendo un vault independiente con su propio `CLAUDE.md`. Teorías, frameworks, metodologías, herramientas y autores de gestión del conocimiento — conocimiento de trabajo profesional pasado, con impacto directo en innovación.
- **[`idiomas/`](idiomas/index.md)** — aprendizaje de francés y portugués (clases, apuntes, recursos).
- **[`ia/`](ia/index.md)** — inteligencia artificial: conceptos, modelos, herramientas, clases, artículos.

Ver `CLAUDE.md` (raíz) para las reglas de enlazado entre vaults.
