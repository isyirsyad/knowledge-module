---
description: Generate a cited deliverable (roadmap, market-study, gap-analysis, competitive-brief, or free-form) into output/ from the knowledge base.
argument-hint: <deliverable> [extra instructions]
---

You are running the {{SUBJECT}} knowledge generation workflow. The requested
deliverable is: `$ARGUMENTS`.

Rules:
- Read ONLY from `knowledge/` (facts, INDEX). NEVER read `input/`.
- Cite the fact slugs you used; include a Sources section listing them.
- Weight firmer facts: prefer `confidence: high`; flag where you relied on
  `low`-confidence facts or found no supporting fact (a gap).

Steps:

1. **Parse the request.** If the first word of `$ARGUMENTS` is one of
   `roadmap`, `market-study`, `gap-analysis`, `competitive-brief`, load the
   matching scaffold from
   `.claude/skills/knowledge-module/references/scaffolds/`. Otherwise treat
   the whole argument as a free-form request (no scaffold).

2. **Retrieve.** Read `knowledge/INDEX.md`. Select relevant facts by `type`
   filter, description match, and by following `[[wikilinks]]` from seed
   facts. Open those fact files.

3. **Generate.** Fill the scaffold (or answer the free-form request) grounded
   in the retrieved facts. Every non-obvious claim should trace to a fact
   slug. Where the knowledge base lacks support, say so explicitly rather
   than inventing — surface it as a gap. Resolve any `{...}` placeholders in the scaffold (e.g. `{PERIOD}`, `{COMPETITOR}`) from `$ARGUMENTS` and any extra instructions; if a placeholder has no applicable value, replace it with a sensible default or omit it — never leave a literal `{...}` token in the output.

4. **Write** the result to `output/<today>-<deliverable-slug>.md`. End the
   document with a `## Sources` section listing every fact slug cited.

5. **Report** the output path and a one-paragraph summary, plus any gaps
   where the knowledge base was thin. `output/` is gitignored, so nothing to
   commit.
