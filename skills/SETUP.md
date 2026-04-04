# Skills Setup

Shared skills live here. Git is the single source of truth.

1. For each `company-docs-*.md` skill in this folder, create a local pointer skill in your workspace
2. The pointer just references the git file — don't copy the full content
3. The sync cron (`company-docs-cron-sync.md`) keeps these up to date — but if you notice a mismatch, update manually
4. **Add a shared skills reference chart to your MEMORY** — list each skill's `name` and one-line `description` (from frontmatter). This lets you know what's available without checking the folder each time. The sync cron will tell you to update this list when skills are added or removed.

## Pointer format

For a skill called `company-docs-date-now.md`, create:

```
skills/company-docs-date-now/SKILL.md
```

With contents:

```markdown
---
name: company-docs-date-now
description: Shared skill — source of truth is in company-docs.
---

See `company-docs/skills/company-docs-date-now.md`. If stale, run `git -C company-docs pull` first.
```
