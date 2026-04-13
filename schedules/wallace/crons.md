# Wallace — Cron Schedule

_Last synced: 2026-04-13 12:00 UTC_

| Job ID | Name | Schedule | Description |
|--------|------|----------|-------------|
| a5ec4ed1-9ddd-45a6-b7f3-3b98a1adb032 | company-docs-sync | Every hour (`0 * * * *`) | Pull latest company-docs, update local skill pointer copies, sync this file, commit and push changes. |
| ea8f5f32-9a20-40dd-ab89-dbf12957bd7c | daily-log | Daily at 00:00 UTC (`0 0 * * *`) | Daily brainstorm journal: review activity, write to `brainstorm-journal/wallace/YYYY-MM-DD-daily.md`, commit and push. |
| b7ac5a61-3eb1-47b2-bba4-401ec4fa1b25 | weekly-summary | Saturdays at 00:00 UTC (`0 0 * * 6`) | Weekly brainstorm journal: read daily logs from past 7 days, write weekly summary to `brainstorm-journal/wallace/YYYY-MM-DD-weekly.md`, commit and push. |
| ffc5114a-ab41-4180-9a16-493326fc11fc | monthly-summary | Days 28–31 at 00:00 UTC (`0 0 28-31 * *`) | Monthly brainstorm journal: read weekly logs from current month, write monthly summary to `brainstorm-journal/wallace/YYYY-MM-monthly-summary.md`, commit and push. |
