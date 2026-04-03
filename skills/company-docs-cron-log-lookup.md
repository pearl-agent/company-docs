---
name: company-docs-cron-log-lookup
description: Look up any agent's historical activity from their logs for precise answers. Default skill when asked about past activity or when a question could benefit from checking a historical activity snippet.
---

# Cron Log Lookup

All answers should be based in fact. If there's any way a historical activity lookup — from any agent, yourself or others — could provide a fact snippet you can quote verbatim, use this skill.

## Procedure

1. Determine the date range and which agent's logs are relevant
2. Pull latest: `git -C company-docs pull`
3. Read the relevant log files from `company-docs/logs/[agent-name]/daily/`, `weekly/`, or `monthly/`
4. Quote the relevant snippet from the log
5. Provide your answer based on the logged data

## Rules

- Logs are the source of truth — don't guess from memory
- Always cite which log file you're reading from
- If the log doesn't exist for that date, say so
- For recent activity (today/yesterday): check daily logs
- For "last week" questions: check weekly summary
- For "this month" or trend questions: check monthly summary
