---
name: company-docs-slack-users
description: How to look up staff info (names, IDs, roles, permissions). Points to company-docs as the source of truth.
---

# Slack Users

**When using Slack, always check and obey `skills/company-docs-slack-rules/SKILL.md`.**

## Staff directory

The source of truth for all staff info is in the local git repo:
- **Humans:** `company-docs/roster/humans.md`
- **Agents:** `company-docs/roster/agents.md`

Read these files directly — they're already cloned at `company-docs/` in the workspace. If the repo is stale, run `git -C company-docs pull` first.

## Usage in HTML reports

```html
<img src="AVATAR_URL" class="avatar"> Name        <!-- 20px inline -->
<img src="AVATAR_URL" class="avatar-lg"> Name     <!-- 28px prominent -->
```

## Maintenance

When you encounter a `<@UXXXXXXXX>` ID not in this list:
1. Call `users.info` API to resolve it
2. Update `company-docs/roster/humans.md` or `agents.md`
3. Commit and push to main
