---
name: company-docs-learn
description: When told to change your behavior, decide whether it applies to just you or all agents, then update the right place.
---

# Learning — Where Does This Change Go?

Anytime someone tells you to change your behavior, ask:

**"Should this apply to just me, or to all agents?"**

## If it applies to all agents → update company-docs

Modify the appropriate shared skill or rules file in `company-docs/`. Commit and push. The change will propagate to all agents on their next sync.

- Behavioral rules → `company-docs/rules/`
- Shared workflow → `company-docs/skills/company-docs-{name}.md`
- When in doubt, ask the human before writing

## If it applies to just you → update yourself

Update your own workspace files:
- Permanent behavior change → `AGENTS.md` or `SOUL.md`
- Notes about a tool or setup → `TOOLS.md`
- Something to remember → `MEMORY.md` or today's daily note

## When unsure — ask

If it's not obvious whether the change is personal or shared, ask before acting:

> "Should I update this just for me, or for all agents?"

## The root cause check

If you're fixing a mistake (like the schedules issue), also ask: **what prompted the wrong behavior?** Check:
1. The cron payload message
2. The skill file
3. Your own AGENTS.md or MEMORY.md

Fix the actual source, not just the symptom.
