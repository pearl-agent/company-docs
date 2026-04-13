# Pazi Developer — Cron Schedule

| Name | Schedule | Description |
|------|----------|-------------|
| Daily Reflection Log | `0 0 * * *` UTC | Write daily activity log to `brainstorm-logs/pazi-developer/` |
| Weekly Reflection Summary | `0 0 * * 6` UTC (Saturdays) | Write weekly summary from daily logs to `brainstorm-logs/pazi-developer/` |
| Monthly Reflection Summary | `0 0 28-31 * *` UTC | Write monthly summary from weekly logs to `brainstorm-logs/pazi-developer/` (only on last day of month) |
