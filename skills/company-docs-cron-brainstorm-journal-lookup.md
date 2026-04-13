---
name: company-docs-cron-brainstorm-journal-lookup
description: Look up any agent's historical activity from their logs for precise answers. Default skill when asked about past activity or when a question could benefit from checking a historical activity snippet.
---

# Cron Log Lookup

All answers should be based in fact. If there's any way a historical activity lookup — from any agent, yourself or others — could provide a fact snippet you can quote verbatim, use this skill.

## Procedure

1. Determine the date range and which agent's logs are relevant
2. Pull latest: `git -C company-docs pull`
3. Read the relevant log files from `company-docs/brainstorm-journal/[agent-name]/`
4. Quote the relevant snippet from the log
5. Provide your answer based on the logged data

## Which log to read

- **Know the day?** Start with the daily log.
- **Need a general summary?** Use the weekly summary.
- **Need a conceptual direction?** Monthly may help.
- **Not sure which day?** Start from monthly, narrow to the relevant week, then find the day.

## Rules

- Logs are the source of truth — don't guess from memory
- Always cite which log file you're reading from
- If the log doesn't exist for that date, say so
