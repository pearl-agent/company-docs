# Shared Skills Registry

> Single source of truth for all shared skills in company-docs.
> Skills live in `company-docs/skills/`. Each agent has a local pointer skill that references the canonical version here.
> Last updated: 2026-04-08 by George

---

| Skill Name | File | Owner | Version / Last Updated | Description | Consumers |
|-----------|------|-------|----------------------|-------------|-----------|
| `company-docs-cron-log` | `company-docs-cron-log.md` | George | 2026-04-03 | Set up daily/weekly/monthly activity logging crons | All agents |
| `company-docs-cron-log-lookup` | `company-docs-cron-log-lookup.md` | George | 2026-04-03 | Look up any agent's historical activity logs | All agents |
| `company-docs-cron-set-reminder` | `company-docs-cron-set-reminder.md` | George | 2026-04-03 | Timed reminders and delayed follow-ups via cron | All agents |
| `company-docs-cron-sync` | `company-docs-cron-sync.md` | George | 2026-04-03 | Hourly repo sync, updates local pointer skills | All agents |
| `company-docs-cron-try-again-soon` | `company-docs-cron-try-again-soon.md` | George | 2026-04-03 | Retry failed operations with escalating delays | All agents |
| `company-docs-date-now` | `company-docs-date-now.md` | George | 2026-04-03 | Date/time formats and how to get current time | All agents |
| `company-docs-host-meeting` | `company-docs-host-meeting.md` | George | 2026-04-06 | Run structured multi-agent brainstorming meetings | George (primary), any agent can trigger |
| `company-docs-skill-add-or-edit` | `company-docs-skill-add-or-edit.md` | George | 2026-04-03 | Rules before creating/editing any skill | All agents |
| `company-docs-slack-rules` | `company-docs-slack-rules.md` | George | 2026-04-03 | When to reply vs stay silent in Slack channels | All agents |
| `company-docs-slack-users` | `company-docs-slack-users.md` | Pearl | 2026-04-03 | Staff lookup (names, IDs, roles, permissions) | All agents |

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

## Skills Known to Exist (Agent-Local, Candidates for Promotion)

These skills were mentioned in the 2026-04-08 company structure meeting as potentially useful across agents. Owners should review and consider promoting to shared.

| Skill | Current Owner | Potential Consumers |
|-------|--------------|-------------------|
| `build-report` | Pazi QA | DevOps, Developer, George |
| `linear` | Pazi QA | Developer, George |
| Playwright/browser automation | Pazi QA | DevOps, Growth |
| Monitoring/health check | Pazi DevOps | George, QA |
| Deploy scripts | Pazi DevOps | (DevOps-only, but readable by all) |
