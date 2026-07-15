# Knowledge Module

A git-versioned, AI-assisted knowledge base you drive from
[Claude Code](https://claude.com/claude-code). Drop your source documents in,
and Claude synthesizes them into small, cited, committed facts that it then
recalls in conversation and uses to generate deliverables.

> This is a **template**. Click **Use this template** (or clone it), run one
> setup command, and you have your own knowledge base. See [Quick start](#quick-start).

## The idea

Most "knowledge bases" are either a pile of source files nobody reads or a wiki
that goes stale. This template takes a different shape:

```
   drop pdf/docx/pptx/md  ─►  input/   (private, gitignored)
            │
            │  /knowledge-ingest
            ▼
        knowledge/  ─►  facts/ + INDEX.md + SOURCES.md + KNOWLEDGE.md   (committed, shared)
            │
            ├── just chat  ─►  Claude auto-answers from the facts, with citations
            │
            └── /knowledge-generate roadmap  ─►  output/   (regenerable, gitignored)
```

- **Source files stay private.** `input/` is gitignored — the originals never
  leave your machine.
- **Knowledge is committed and shareable.** Each fact is an atomic Markdown file
  with provenance (which source, which page) and a verbatim evidence quote, so a
  teammate can trust it without the original file.
- **Recall is automatic.** A `CLAUDE.md` in the repo tells Claude to answer any
  question about your subject from the committed facts, always citing the source.
- **Deliverables are generated, not hand-written.** `/knowledge-generate` builds
  cited documents (roadmap, market study, gap analysis, competitive brief, or a
  free-form ask) into `output/`.

## Quick start

1. **Use this template** (GitHub) or clone the repo, and open it in Claude Code.
2. **Personalize it:** run `/knowledge-init "<Your Subject>"` — e.g.
   `/knowledge-init "Acme Corp"`. This replaces the `{{SUBJECT}}` placeholder
   throughout the repo. (Manual alternative in [SETUP.md](SETUP.md).)
3. *(Optional)* **Tune it to your domain** — edit the taxonomy and deliverable
   scaffolds (see [Customizing](#customizing)).
4. **Ingest:** drop documents into `input/` and run `/knowledge-ingest`. Claude
   synthesizes atomic facts into `knowledge/` and updates the index, source
   manifest, and human digest.
5. **Use it:** ask questions in plain chat (answers cite their sources), or run
   `/knowledge-generate <deliverable>`.

## What's committed vs. ignored

| Path | Committed? | Purpose |
|---|---|---|
| `knowledge/` | ✅ | The shared brain — atomic facts + index + sources + digest |
| `.claude/` | ✅ | The skill and slash commands |
| `README.md`, `SETUP.md`, `.gitignore` | ✅ | Project files |
| `input/` | ❌ (gitignored) | Drop zone for source documents |
| `output/` | ❌ (gitignored) | Generated, regenerable deliverables |

## The knowledge model

- `knowledge/facts/*.md` — one atomic fact per file, with YAML frontmatter
  (type, source, date, author, confidence) and a verbatim evidence quote. Source
  of truth.
- `knowledge/INDEX.md` — one terse line per fact (for recall + dedup).
- `knowledge/SOURCES.md` — a manifest of every ingested source file (name, date,
  who, hash). Because sources are gitignored, this is the auditable record of
  what the knowledge is built on.
- `knowledge/KNOWLEDGE.md` — a human-readable digest, grouped by type,
  regenerated from the facts.

Full format spec: [`.claude/skills/knowledge-module/references/fact-format.md`](.claude/skills/knowledge-module/references/fact-format.md).

## Commands

- `/knowledge-init "<Subject>"` — one-time personalization (replaces `{{SUBJECT}}`).
- `/knowledge-ingest` — synthesize new/changed files in `input/` into facts.
- `/knowledge-generate <deliverable>` — produce a cited deliverable into `output/`.

## Customizing

Two parts are opinionated defaults you should adapt to your domain:

- **Taxonomy** — [`.claude/skills/knowledge-module/references/taxonomy.md`](.claude/skills/knowledge-module/references/taxonomy.md)
  ships 11 categories suited to an organization/company knowledge base
  (`strategy`, `market`, `product`, `gtm`, …). For other domains (engineering,
  research, personal), edit this list. Types are just retrieval tags, so changing
  them later is cheap.
- **Deliverable scaffolds** — [`.claude/skills/knowledge-module/references/scaffolds/`](.claude/skills/knowledge-module/references/scaffolds/)
  holds section templates for `roadmap`, `market-study`, `gap-analysis`, and
  `competitive-brief`. Swap these for whatever your domain generates.

Everything else — the fact format, provenance model, ingest/generate flow, and
auto-recall — is domain-neutral.

## Requirements

[Claude Code](https://claude.com/claude-code). To ingest PDF/DOCX/PPTX,
Claude uses document-reading skills; plain Markdown needs nothing extra.

## License

[MIT](LICENSE) © 2026 Irsyad Saidin. The license covers the boilerplate itself
(skill, commands, scaffolds, and structure). Knowledge you create in your own
copy is your content and is not governed by this license — but per the MIT
terms, keep the copyright notice in `LICENSE` intact when redistributing the
template.

## Credits

Built with the [Superpowers](https://github.com/obra/superpowers) workflow for
Claude Code.
