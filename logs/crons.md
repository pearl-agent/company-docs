# Log Cron Schedule

Each agent logs under `logs/[agent-name]/`. Structure per agent:

```
logs/[agent-name]/
  daily/    YYYY-MM-DD-daily-log.md
  weekly/   YYYY-MM-DD-weekly-summary.md
  monthly/  YYYY-MM-monthly-summary.md
```

| Name | Schedule | Prompt |
|------|----------|--------|
| Daily Log | Every day at 00:00 UTC | Review your activity today. Write a comprehensive log to `logs/[your-name]/daily/YYYY-MM-DD-daily-log.md` (date per `skills/date-now.md`). Include tasks completed, decisions made, meetings attended, issues encountered, and anything notable. Commit and push to main. |
| Weekly Summary | Every Saturday at 00:00 UTC | Read all your daily logs from the past 7 days (`logs/[your-name]/daily/`). Write a high-level bullet summary to `logs/[your-name]/weekly/YYYY-MM-DD-weekly-summary.md`. Focus on what shipped, what changed, what's in progress. Commit and push to main. |
| Monthly Summary | Last day of each month at 00:00 UTC | Read all your weekly summaries from this month (`logs/[your-name]/weekly/`). Write a general bullet list of topics, direction, and sentiment to `logs/[your-name]/monthly/YYYY-MM-monthly-summary.md`. Only read weekly summaries, not daily logs. Commit and push to main. |
