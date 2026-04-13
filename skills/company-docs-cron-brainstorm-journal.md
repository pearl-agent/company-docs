---
name: company-docs-cron-brainstorm-journal
description: Set up daily, weekly, and monthly brainstorm journal crons. Shared skill for all agents.
---

# Cron — Brainstorm Journal

## Folder structure

Create under `brainstorm-logs/[your-name]/`:
```
brainstorm-logs/[your-name]/
  daily/    YYYY-MM-DD-daily-log.md
  weekly/   YYYY-MM-DD-weekly-summary.md
  monthly/  YYYY-MM-monthly-summary.md
```

## Cron jobs to set up

| Name | Schedule | What to do |
|------|----------|------------|
| Daily Brainstorm | Every day at 00:00 UTC | Review the full day's activity — check session logs, tasks completed, decisions made, and general time spent. Then follow `company-docs-brainstorm` with that as your data. File goes to `brainstorm-logs/[your-name]/YYYY-MM-DD-daily.md`. Commit and push. |
| Weekly Brainstorm | Every Saturday at 00:00 UTC | Read all your daily brainstorm logs from the past 7 days. Summarize the big-picture multi-day accomplishments, patterns, and direction. Then follow `company-docs-brainstorm` with that summary as your data. File goes to `brainstorm-logs/[your-name]/YYYY-MM-DD-weekly.md`. Commit and push. |
| Monthly Brainstorm | Last day of each month at 00:00 UTC | Read your weekly brainstorm logs from this month only — do not re-read daily logs. Identify the biggest themes, shifts, and strategic signals across the month. Then follow `company-docs-brainstorm` with that as your data. File goes to `brainstorm-logs/[your-name]/YYYY-MM-monthly.md`. Commit and push. |

## Log formats

### Daily brainstorm

Review the full day's activity — session logs, tasks completed, decisions made, general time spent. Use that as your data and follow `company-docs-brainstorm`. File: `brainstorm-logs/[your-name]/YYYY-MM-DD-daily.md`. Commit and push.

### Weekly brainstorm

Read all your daily brainstorm logs from the past 7 days. Summarize the big-picture multi-day accomplishments, patterns, and direction — use that summary as your data and follow `company-docs-brainstorm`. File: `brainstorm-logs/[your-name]/YYYY-MM-DD-weekly.md`. Commit and push.

### Monthly brainstorm

Read your weekly brainstorm logs from this month only — do not re-read daily logs. Identify the biggest themes, shifts, and strategic signals across the month — use that as your data and follow `company-docs-brainstorm`. File: `brainstorm-logs/[your-name]/YYYY-MM-monthly.md`. Commit and push.
