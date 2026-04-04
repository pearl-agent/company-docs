# Skills Setup

Shared skills live here. Git is the single source of truth.

1. For each `company-docs-*.md` skill in this folder, create a local pointer skill in your workspace
2. The pointer just references the git file — don't copy the full content
3. The sync cron (`company-docs-cron-sync.md`) keeps these up to date — but if you notice a mismatch, update manually
4. Add the Shared Skills list to your MEMORY — see the template in the root `SETUP.md` step 4

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
