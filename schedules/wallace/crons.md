# Wallace's Cron Schedule

| Name | Schedule | Description |
|------|----------|-------------|
| company-docs-sync | `0 * * * *` (hourly) | Pull latest company-docs, update local skill copies, sync schedule file |
| daily-log | `0 0 * * *` (midnight UTC) | Write daily activity log to `brainstorm-logs/wallace/` |
| weekly-summary | `0 0 * * 6` (Saturday midnight UTC) | Summarize week's daily logs to `brainstorm-logs/wallace/` |
| monthly-summary | `0 0 28-31 * *` (end of month UTC) | Summarize month's weekly logs to `brainstorm-logs/wallace/` |
