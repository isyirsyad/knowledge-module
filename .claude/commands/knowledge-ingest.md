---
description: Synthesize new/changed files in input/ into atomic knowledge facts with provenance.
---

You are running the {{SUBJECT}} knowledge ingest workflow. First read
`.claude/skills/knowledge-module/references/fact-format.md` and
`.claude/skills/knowledge-module/references/taxonomy.md` for the exact format and categories.

Steps:

1. **Detect new/changed sources.** List files in `input/` (pdf, docx, pptx,
   md). For each, compute `shasum -a 256 <file>` and take the first 6 chars.
   Compare file name + hash against the rows in `knowledge/SOURCES.md`. Skip
   files whose name AND hash already appear. Report which files are new or
   changed before proceeding.

2. **Extract text.** Use the right reader per type: the `anthropic-skills:pdf`
   skill for PDF, `anthropic-skills:docx` for DOCX, `anthropic-skills:pptx`
   for PPTX, and native file reading for Markdown.

3. **Synthesize atomic facts.** Break the content into discrete claims. For
   each claim, draft a fact per `fact-format.md`: pick the best `type` from
   the 11 categories, write a one-line `description`, a 1–4 sentence body, a
   VERBATIM evidence quote attributed to the source (with page/slide if
   available), set `confidence`, `added: <today>`, `added_by: <the current
   user>`, and add `[[wikilinks]]` to related facts.

4. **Dedup.** Before writing each fact, read `knowledge/INDEX.md`. If a fact
   already covers the same claim, UPDATE that fact instead of creating a
   duplicate: add the corroborating source and, if it strengthens the claim,
   raise `confidence`.

5. **Detect contradictions.** If a new source contradicts an existing fact
   (e.g. a different value), do NOT overwrite. Keep both sources in the fact,
   downgrade `confidence`, and add the fact to a "Conflicts to resolve" list
   in your final report for the user to adjudicate.

6. **Write.** Save each new fact to `knowledge/facts/<name>.md` (name ==
   filename). Update `knowledge/INDEX.md` (one sorted line per fact between
   the FACTS markers). Append one row per newly ingested source to
   `knowledge/SOURCES.md`. Regenerate `knowledge/KNOWLEDGE.md` from all facts
   per the regeneration rule in `fact-format.md`.

7. **Report.** Summarize: sources ingested, facts added, facts updated/merged,
   and any conflicts to resolve. Do NOT commit automatically — show the user
   the summary and let them review, then commit if they approve.

Argument (optional): `$ARGUMENTS` may name a specific file in `input/` to
ingest only that file; if empty, process all new/changed files.
