# Shared Skills Registry

> Single source of truth for all shared skills in company-docs.
> Skills live in `company-docs/skills/`. Each agent has a local pointer skill that references the canonical version here.
> Last updated: 2026-04-08 by George

---

| Skill Name | File | Last Updated | Description |
|-----------|------|-------------|-------------|
| `company-docs-cron-brainstorm-journal` | `company-docs-cron-brainstorm-journal.md` | 2026-04-05 03:42:11 UTC | Set up daily/weekly/monthly brainstorm journal crons |
| `company-docs-cron-log-lookup` | `company-docs-cron-log-lookup.md` | 2026-04-05 02:10:48 UTC | Look up any agent's historical activity logs |
| `company-docs-cron-set-reminder` | `company-docs-cron-set-reminder.md` | 2026-04-06 02:23:09 UTC | Timed reminders and delayed follow-ups via cron |
| `company-docs-cron-sync` | `company-docs-cron-sync.md` | 2026-04-04 02:15:16 UTC | Hourly repo sync, updates local pointer skills |
| `company-docs-cron-try-again-soon` | `company-docs-cron-try-again-soon.md` | 2026-04-03 05:53:04 UTC | Retry failed operations with escalating delays |
| `company-docs-date-now` | `company-docs-date-now.md` | 2026-04-06 02:23:09 UTC | Date/time formats and how to get current time |
| `company-docs-host-meeting-tree-rules` | `company-docs-host-meeting-tree-rules.md` | 2026-04-09 00:24:59 UTC | Run structured multi-agent brainstorming meetings |
| `company-docs-host-meeting-tree-ffa` | `company-docs-host-meeting-tree-ffa.md` | 2026-04-09 04:03:00 UTC | Run structured multi-agent brainstorming meetings (free-for-all variant) |
| `company-docs-skill-add-or-edit` | `company-docs-skill-add-or-edit.md` | 2026-04-07 05:52:50 UTC | Rules before creating/editing any skill |
| `company-docs-slack-rules` | `company-docs-slack-rules.md` | 2026-04-03 05:53:04 UTC | When to reply vs stay silent in Slack channels |
| `company-docs-slack-users` | `company-docs-slack-users.md` | 2026-04-06 02:23:58 UTC | Staff lookup (names, IDs, roles, permissions) |

---

## Rules for Adding a Skill

1. Add the skill file to `company-docs/skills/`
2. Add a row to this registry with owner, date, and description
3. Create local pointer skills for all agents that should consume it (don't wait for sync cron)
4. One owner per skill — others consume the published version, not their own copy
5. If you improve a shared skill, update the `Version / Last Updated` field and notify affected agents

## Rules for Consuming a Skill

- Read the canonical version here before building your own equivalent
- If a shared skill almost does what you need, propose an improvement to the owner rather than forking it
- Local pointer skills should reference the canonical file path, not maintain their own content

---


