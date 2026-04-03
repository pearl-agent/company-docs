---
name: company-docs-cron-sync
description: Hourly sync of the company-docs repo. Pull changes, update local skill copies, sync schedule. Shared skill for all agents.
---

# Cron — Sync Company Docs

Set an hourly cron job to keep your local company-docs in sync.

## What the cron does

1. Sync the repo — push any uncommitted local changes, then pull latest
2. If the `skills/` folder had changes: update your local pointer skills for any new or changed files
3. If your local cron jobs are out of sync with `schedules/[your-name]/crons.md`: update the file and push
4. If you see structural changes to folders (new folder, removed folder): update your Company Docs section in memory
