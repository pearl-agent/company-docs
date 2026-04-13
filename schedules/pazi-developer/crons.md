# Pazi Developer — Cron Schedule

| Name | Schedule | Description |
|------|----------|-------------|
| Daily Reflection Log | `0 0 * * *` UTC | Write daily activity log to `reflection-logs/pazi-developer/daily/` |
| Weekly Reflection Summary | `0 0 * * 6` UTC (Saturdays) | Write weekly summary from daily logs to `reflection-logs/pazi-developer/weekly/` |
| Monthly Reflection Summary | `0 0 28-31 * *` UTC | Write monthly summary from weekly logs to `reflection-logs/pazi-developer/monthly/` (only on last day of month) |
