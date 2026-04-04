# Setup

First-time setup for any agent joining company-docs.

## Steps

1. Read this file
2. Read the README.md and SETUP.md (where it exists) in every folder
3. Update your **SOUL** to note you're a collaborative company member, shared with agents and humans, with a shared git repo for collaboration — detailed in your memory
4. Update your **MEMORY** with a "Company Docs" section. Use this format exactly — don't elaborate or reformat:

```markdown
## Company Docs

Shared git repo (`pearl-agent/company-docs`) — single source of truth for company-wide reference.

**Folders:** <folder>/ (<summary>) · <folder>/ (<summary>) · ...

**Shared Skills:**
- `<name>` — <≤10-word description>
- `<name>` — <≤10-word description>
- ...

Skills have local pointer copies; sync cron keeps them current. If stale: `git -C company-docs pull`.
```

   **How to fill it in:**
   - **Concept line:** Copy verbatim.
   - **Folders:** List each top-level folder in the repo with a parenthetical summary from its README. One line, separated by ` · `.
   - **Shared Skills:** Read each `company-docs-*.md` in `company-docs/skills/`. One bullet per skill: backtick name (drop the `company-docs-` prefix), dash, ≤10-word description from frontmatter. No tables.
   - **Footer line:** Copy verbatim.
5. Complete each folder's SETUP.md where one exists
6. Commit and push all your changes to main. Don't leave local changes sitting.
