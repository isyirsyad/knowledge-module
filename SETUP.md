# Setup

One-time steps to turn this template into your own knowledge base.

## 1. Personalize the subject name

This template uses the placeholder `{{SUBJECT}}` for whatever your knowledge
base is about (a company, project, product, research area, etc.).

**Recommended — run the init command in Claude Code:**

```
/knowledge-init "Your Subject"
```

It replaces every `{{SUBJECT}}` across `CLAUDE.md`, `README.md`, the skill, the
commands, the scaffolds, and the digest title, then reports what changed.

**Manual alternative** (any editor / shell):

```bash
# macOS
grep -rl '{{SUBJECT}}' . --exclude-dir=.git | xargs sed -i '' 's/{{SUBJECT}}/Your Subject/g'
# Linux
grep -rl '{{SUBJECT}}' . --exclude-dir=.git | xargs sed -i    's/{{SUBJECT}}/Your Subject/g'
```

## 2. (Optional) Tune the taxonomy to your domain

`.claude/skills/knowledge-module/references/taxonomy.md` defines the fact
categories. The default 11 suit a company/organization. For other domains, edit
that list. Types are just retrieval tags — changing them later is cheap and does
not require migrating existing facts.

## 3. (Optional) Adjust the deliverable scaffolds

`.claude/skills/knowledge-module/references/scaffolds/` holds section templates
for `roadmap`, `market-study`, `gap-analysis`, and `competitive-brief`. Replace
or add scaffolds to match what your domain generates. `/knowledge-generate` also
accepts free-form requests with no scaffold.

## 4. Start using it

1. Drop source documents into `input/` (pdf, docx, pptx, md).
2. Run `/knowledge-ingest`.
3. Ask questions in plain chat, or run `/knowledge-generate <deliverable>`.

## 5. (Optional) Clean up

Once set up, you can delete this `SETUP.md` and the
`.claude/commands/knowledge-init.md` command — they are only needed once.
