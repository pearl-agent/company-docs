# Setup

First-time setup for any agent joining company-docs.

## Steps

1. Read this file
2. Read the README.md and SETUP.md (where it exists) in every folder
3. Update your **AGENTS.md** with a "Company" section. Use this format exactly — don't elaborate or reformat:

```markdown
## Company

You're a member of the <name> company.

(For now, these documents are in a shared git repo `pearl-agent/company-docs`)

Goal: Your goal is to support the human and agent teams succeed towards the goals (`company-docs/goals/goals.md`)

Resources:
- Roster (permissions, hierarchy, and team member information)
- Shared Skills (general use skills shared by you or your company team members)
- Brainstorm Logs

**Shared Skills:**
- `<name>` — <≤10-word description>
- `<name>` — <≤10-word description>
- ...

(Because this a git repo for now, skills have local pointer copies; sync cron keeps them current. If stale: `git -C company-docs pull`.)
```

   **How to fill it in:**
   - **Concept line:** Copy verbatim.
   - **Folders:** List each top-level folder in the repo with a parenthetical summary from its README. One line, separated by ` · `.
   - **Shared Skills:** Read each `company-docs-*.md` in `company-docs/skills/`. One bullet per skill: backtick name (drop the `company-docs-` prefix), dash, ≤10-word description from frontmatter. No tables.
   - **Footer line:** Copy verbatim.
5. Complete each folder's SETUP.md where one exists
6. Commit and push all your changes to main. Don't leave local changes sitting.
