# Setup

First-time setup for any agent joining company-docs.

## Steps

1. Read this file
2. Read the README.md and SETUP.md (where it exists) in every folder
3. Update your **SOUL** to note you're a collaborative company member, shared with agents and humans, with a shared git repo for collaboration — detailed in your memory
4. Update your **MEMORY** with a "Company Docs" section. **Use this template exactly** — don't elaborate or reformat:

```markdown
## Company Docs

Shared git repo (`pearl-agent/company-docs`) — single source of truth for company-wide reference.

**Folders:** direction/ (goals/strategy) · logs/ (daily/weekly/monthly per agent) · policies/ (rules) · roster/ (humans + agents) · schedules/ (cron per agent) · skills/ (shared, git = source of truth) · whiteboard/ (temp collab)

**Shared Skills:**
- `cron-log` — activity logging crons (daily/weekly/monthly)
- `cron-log-lookup` — look up any agent's historical activity
- `cron-set-reminder` — timed reminders and delayed follow-ups
- `cron-sync` — hourly repo sync, updates local pointer skills + this list
- `cron-try-again-soon` — retry failed ops with escalating delays
- `date-now` — date/time formats and how to get current time
- `skill-add-or-edit` — rules before creating/editing any skill
- `slack-rules` — when to reply vs stay silent in Slack
- `slack-users` — staff lookup (names, IDs, roles, permissions)

Skills have local pointer copies; sync cron keeps them current. If stale: `git -C company-docs pull`.
```

   **Rules:** Copy the concept line and folder list verbatim. For Shared Skills, read each `company-docs-*.md` in `company-docs/skills/` and add one bullet per skill: backtick name (drop the `company-docs-` prefix), dash, ≤10-word description. No tables. No elaboration.
5. Complete each folder's SETUP.md where one exists
6. Commit and push all your changes to main. Don't leave local changes sitting.
