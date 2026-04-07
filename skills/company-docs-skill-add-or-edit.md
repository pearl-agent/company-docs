---
name: company-docs-skill-add-or-edit
description: Rules for creating or editing skills. Read this before making any skill changes. Covers one source of truth, modularity, templates, and reporting changes to the human.
---

# Skill Add or Edit

Read this before creating or editing any skill.

## Rules

### One source of truth
- If information could be referenced by more than one skill, put it in ONE skill and reference it from the others
- Before adding anything, check existing skills — does this already exist somewhere?
- If it does, don't duplicate it. Add a reference: "See `skills/skill-name/SKILL.md`"
- When editing, check if other skills reference or duplicate the thing you're changing

### Templates, not examples
- Use template patterns: `YYYY-MM-DD`, `<@USER_ID>`, `[paste verbatim]`
- Never use concrete examples as templates — no hardcoded dates, names, or values that could be mistaken for instructions
- If you must show an example, use placeholders that are obviously not real data

### Modularity
- Always lean towards creating multiple smaller skills over one large skill
- If there's any chance a piece of logic could be used in more than one place, make it its own skill
- A skill should do one thing

### Local pointer skill
- When creating a **new** shared skill in `company-docs/skills/`, you MUST also create a local pointer skill at `skills/company-docs-{name}/SKILL.md` in your workspace
- The pointer must include a `description` in its frontmatter that matches the skill's purpose — this is how the skill gets discovered at session start
- When editing an existing skill's description or name, update the local pointer too
- Do NOT rely on `cron-sync` to create pointers — the skill is invisible until the pointer exists

### Report changes to your human
When confirming a skill add or edit is done, list each skill touched by name, then under each:
- Bullet the targeted areas
- Quote the snippet if short, or summarize if more than 5 words
