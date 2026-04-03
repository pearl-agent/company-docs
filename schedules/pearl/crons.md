# Pearl — Cron Jobs

| Name | Schedule | UTC | Prompt |
|------|----------|-----|--------|
| Morning Standup | Daily | 21:30 | Run the slack-agent-morning-standup skill. |
| Daily Report | Daily | 22:30 | Run the slack-daily-report skill. |
| Daily Log | Daily | 00:00 | Write daily log to `logs/pearl/daily/`. |
| Weekly Summary | Saturday | 00:00 | Summarize week's daily logs to `logs/pearl/weekly/`. |
| Monthly Summary | Last day of month | 00:00 | Summarize month's weekly logs to `logs/pearl/monthly/`. |
