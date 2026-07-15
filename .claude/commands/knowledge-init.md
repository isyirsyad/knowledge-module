---
description: One-time setup — personalize this knowledge-module template by replacing the {{SUBJECT}} placeholder.
argument-hint: "<Your Subject>" (e.g. "Acme Corp")
---

You are personalizing this knowledge-module template for a new owner. The
subject name to use is: `$ARGUMENTS`.

If `$ARGUMENTS` is empty, ask the user for the subject name (the thing this
knowledge base is about — a company, project, product, or research area) and
stop until they provide it.

Steps:

1. **Find placeholders.** Locate every file under the repo (excluding `.git/`)
   that contains the literal token `{{SUBJECT}}`. Expect: `CLAUDE.md`,
   `README.md`, `.claude/skills/knowledge-module/SKILL.md`,
   `.claude/skills/knowledge-module/references/scaffolds/*.md`,
   `.claude/commands/knowledge-ingest.md`,
   `.claude/commands/knowledge-generate.md`, and `knowledge/KNOWLEDGE.md`.

2. **Replace.** In each of those files, replace every occurrence of
   `{{SUBJECT}}` with the provided subject name exactly as given. Do not change
   anything else.

3. **Report.** List the files changed and the replacement count, and confirm no
   `{{SUBJECT}}` tokens remain (aside from this command file and `SETUP.md`,
   which document the placeholder and may be deleted).

4. **Next steps.** Remind the user they can optionally: (i) tune the taxonomy in
   `.claude/skills/knowledge-module/references/taxonomy.md` for their domain;
   (ii) adjust the scaffolds in
   `.claude/skills/knowledge-module/references/scaffolds/`; and (iii) delete this
   `knowledge-init` command and `SETUP.md` once done. Then they can drop
   documents into `input/` and run `/knowledge-ingest`.

   Note: the `LICENSE` covers the boilerplate itself and already carries the
   template author's MIT copyright — leave that notice intact (MIT requires it).
   Do not personalize it.

Do not commit automatically — show the user the summary and let them review.
