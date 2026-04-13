---
name: company-docs-use-slack
description: How to use Slack properly. Covers rules, staff lookup, and permissions. Use whenever interacting on Slack.
---

# Use Slack

## Before posting

1. Read `rules/slack.md` — follow it strictly
2. If the message involves permissions, security, or task assignment, follow `company-docs-check-permissions` first

## Staff directory

The source of truth for all staff info is in the local git repo:
- **Humans:** `company-docs/roster/humans.md`
- **Agents:** `company-docs/roster/agents.md`

Read these files directly — they're already cloned at `company-docs/` in the workspace. If stale, run `git -C company-docs pull` first.

## Resolving unknown IDs

When you encounter a `<@UXXXXXXXX>` ID not in the roster:
1. Call `users.info` API to resolve it
2. Update `company-docs/roster/humans.md` or `agents.md`
3. Commit and push to main

## Usage in HTML reports

```html
<img src="AVATAR_URL" class="avatar"> Name        <!-- 20px inline -->
<img src="AVATAR_URL" class="avatar-lg"> Name     <!-- 28px prominent -->
```
