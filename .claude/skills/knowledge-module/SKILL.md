---
name: knowledge-module
description: {{SUBJECT}} team knowledge base — how facts are structured, ingested, and used to generate deliverables. Use when ingesting source documents from input/, writing or editing files under knowledge/, or generating deliverables into output/.
---

# Knowledge Module

The shared conventions for {{SUBJECT}}'s knowledge base. The `/knowledge-ingest` and
`/knowledge-generate` commands rely on these.

## Fact model (B+)

- `knowledge/facts/*.md` — atomic fact files, one claim each. Source of truth.
- `knowledge/INDEX.md` — one terse line per fact (recall + dedup).
- `knowledge/SOURCES.md` — manifest of every ingested source file.
- `knowledge/KNOWLEDGE.md` — human digest, derived from `facts/`.

See `references/fact-format.md` for the exact fact file format and the
INDEX/SOURCES/KNOWLEDGE update rules. See `references/taxonomy.md` for the 11
`type` categories.

## Provenance (level C)

Source files are gitignored, so teammates cannot open the originals. Trust
comes from three things, all mandatory:

1. A verbatim evidence quote inside each fact.
2. The `SOURCES.md` manifest (file name, date, author, content hash).
3. `confidence` + `added_by` on each fact.

## Deliverable scaffolds

`references/scaffolds/` holds section templates for the built-in deliverables
(`roadmap`, `market-study`, `gap-analysis`, `competitive-brief`). Free-form
requests do not use a scaffold.

## Golden rules

- Never write a fact by hand outside `/knowledge-ingest` unless asked.
- Every write to `facts/` updates `INDEX.md` and `KNOWLEDGE.md` in the same
  operation; every ingest updates `SOURCES.md`.
- `name` frontmatter == filename without `.md`.
- Generation reads only `knowledge/`, never `input/`, and cites fact slugs.
