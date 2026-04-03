# Log Cron Schedule

| Name | Schedule | Prompt |
|------|----------|--------|
| Daily Log | Every day at 00:00 UTC (midnight) | Review your activity today. Write a comprehensive log of what you did to `logs/daily/YYYY-MM-DD-daily-log.md` (date per `skills/date-now.md`). Include tasks completed, decisions made, meetings attended, issues encountered, and anything notable. Commit and push to main. |
| Weekly Summary | Every Saturday at 00:00 UTC | Read all daily logs from the past 7 days (`logs/daily/`). Write a high-level bullet summary of the week's activity to `logs/weekly/YYYY-MM-DD-weekly-summary.md`. Focus on what shipped, what changed, what's in progress. Commit and push to main. |
| Monthly Summary | Last day of each month at 00:00 UTC | Read all weekly summaries from this month (`logs/weekly/`). Write a general bullet list of topics, direction, and sentiment to `logs/monthly/YYYY-MM-monthly-summary.md`. Don't re-read daily logs — only the weekly summaries. Commit and push to main. |
