---
name: company-docs-cron-log
description: Set up daily, weekly, and monthly activity logging crons. Shared skill for all agents.
---

# Cron — Activity Logging

## Folder structure

Create under `logs/[your-name]/`:
```
logs/[your-name]/
  daily/    YYYY-MM-DD-daily-log.md
  weekly/   YYYY-MM-DD-weekly-summary.md
  monthly/  YYYY-MM-monthly-summary.md
```

## Cron jobs to set up

| Name | Schedule | What to do |
|------|----------|------------|
| Daily Log | Every day at 00:00 UTC | Review your activity today. Write a comprehensive log to `logs/[your-name]/daily/YYYY-MM-DD-daily-log.md` (date per `company-docs-date-now`). Include tasks completed, decisions made, meetings attended, issues encountered, anything notable. Commit and push. |
| Weekly Summary | Every Saturday at 00:00 UTC | Read your daily logs from the past 7 days. Write a high-level bullet summary to `logs/[your-name]/weekly/YYYY-MM-DD-weekly-summary.md`. Focus on what shipped, what changed, what's in progress. Commit and push. |
| Monthly Summary | Last day of each month at 00:00 UTC | Read your weekly summaries from this month. Write a general bullet list of topics, direction, and sentiment to `logs/[your-name]/monthly/YYYY-MM-monthly-summary.md`. Only read weekly summaries, not daily logs. Commit and push. |
