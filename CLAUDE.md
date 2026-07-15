# {{SUBJECT}} Knowledge Module

> **First-time setup:** run `/knowledge-init "<Your Subject>"` to replace every
> `{{SUBJECT}}` placeholder in this repo with your subject's name. See
> `SETUP.md`.

This repository is {{SUBJECT}}'s shared, git-versioned knowledge base. The
committed `knowledge/` directory is the single source of truth about {{SUBJECT}}.

## Answering questions about {{SUBJECT}} (always-on recall)

Before answering ANY question about {{SUBJECT}}:

1. Read `knowledge/INDEX.md` to see which facts exist.
2. Open the relevant fact file(s) under `knowledge/facts/`.
3. Answer from those facts, and ALWAYS cite the fact slug and its `source`
   — e.g. "Registered at 12 Jalan X — `company-registration-address`
   (from `incorporation-cert.pdf`)".
4. If no fact covers the question, say so plainly. Do NOT answer from
   assumption or general knowledge. If the material might exist in `input/`,
   suggest running `/knowledge-ingest`.

This recall is instruction-following, not a database guarantee. Citing the
source on every answer is the safeguard: it lets the reader tell a grounded
answer from a guess.

## Directory map

- `input/` — drop zone for source docs (pdf/docx/pptx/md). GITIGNORED.
- `output/` — generated deliverables. GITIGNORED, regenerable.
- `knowledge/` — the committed shared brain:
  - `facts/` — atomic fact files (source of truth)
  - `INDEX.md` — one line per fact (recall + dedup)
  - `SOURCES.md` — manifest of ingested source files
  - `KNOWLEDGE.md` — human-readable digest (derived view)
- `.claude/skills/knowledge-module/` — shared reference material (fact
  format, taxonomy, deliverable scaffolds).

## Commands

- `/knowledge-init "<Subject>"` — one-time personalization of this template.
- `/knowledge-ingest` — synthesize new/changed files in `input/` into facts.
- `/knowledge-generate <deliverable>` — produce a cited deliverable into
  `output/` (e.g. `roadmap`, `market-study`, `gap-analysis`,
  `competitive-brief`, or a free-form request).

Do NOT hand-write files under `knowledge/` outside the `/knowledge-ingest`
flow unless explicitly asked — that flow keeps `INDEX.md`, `SOURCES.md`, and
`KNOWLEDGE.md` in sync.
