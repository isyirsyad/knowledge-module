# Fact File Format

## Example

```markdown
---
name: competitor-acme-weakness
description: Acme lacks SSO below enterprise tier — recurring competitive loss reason
metadata:
  type: competitive
  source: acme-teardown-2026.pdf
  source_page: 14
  added: 2026-07-14
  added_by: irsyad
  confidence: high
---

Acme does not offer SSO on any plan below their Enterprise tier ($2k/mo).
Mid-market buyers repeatedly cite this as the reason they switch to us.

> "SSO and SCIM are available exclusively on Enterprise plans."
> — acme-teardown-2026.pdf, p.14

Related: [[pricing-tier-structure]], [[icp-mid-market-saas]]
```

## Rules

- Filename = `<name>.md`, kebab-case. `name` frontmatter MUST match it.
- Required frontmatter: `name`, `description`, `metadata.type`,
  `metadata.source`, `metadata.added` (YYYY-MM-DD), `metadata.added_by`,
  `metadata.confidence`. `metadata.source_page` optional.
- `type` ∈ the 11 taxonomy values. `confidence` ∈ {high, medium, low}.
- Body: 1–4 sentences, the synthesized claim in plain words.
- Evidence quote: a `>` blockquote with a VERBATIM excerpt from the source,
  attributed with file name and locator. If the source cannot be quoted
  verbatim (e.g. a chart), paraphrase and mark it `(paraphrased)`.
- `Related:` line with `[[wikilinks]]` to related fact slugs (omit if none).

## INDEX.md update rule

For each fact, ensure exactly one line exists between the `FACTS:START` and
`FACTS:END` markers, sorted alphabetically by slug:

```
- [competitor-acme-weakness](facts/competitor-acme-weakness.md) `competitive` — Acme lacks sub-enterprise SSO
```

## SOURCES.md update rule

On ingest, append one row per newly ingested source file:

```
| acme-teardown-2026.pdf | 2026-07-14 | irsyad | a1b2c3 | Competitor teardown of Acme |
```

`Hash` = first 6 chars of the file's SHA-256 (`shasum -a 256 <file>`).

## KNOWLEDGE.md regeneration rule

Rebuild the digest from all files in `facts/`:
- One `##` heading per type, canonical order (see taxonomy), 11 total — preserve the exact heading text as originally scaffolded, including the all-caps `GTM`.
- Under each heading, one short paragraph or bullet per fact of that type,
  written for a human reader, ending with the slug in parentheses.
- Replace the `_No facts yet._` placeholder when a type gains its first fact.
- Update the `_Last regenerated:_` line to today's date.
