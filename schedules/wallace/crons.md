# Wallace — Cron Schedule

Last updated: 2026-04-14

| ID | Name | Schedule | Description |
|----|------|----------|-------------|
| a5ec4ed1-9ddd-45a6-b7f3-3b98a1adb032 | company-docs-sync | `0 * * * *` (hourly) | Pull latest company-docs, update local skill pointers, sync crons.md, commit & push |
| ea8f5f32-9a20-40dd-ab89-dbf12957bd7c | daily-log | `0 0 * * *` (daily midnight UTC) | Write daily brainstorm journal to company-docs/brainstorm-journal/wallace/ |
| b7ac5a61-3eb1-47b2-bba4-401ec4fa1b25 | weekly-summary | `0 0 * * 6` (Saturday midnight UTC) | Write weekly brainstorm summary from daily logs |
| ffc5114a-ab41-4180-9a16-493326fc11fc | monthly-summary | `0 0 28-31 * *` (end of month) | Write monthly brainstorm summary from weekly logs |
