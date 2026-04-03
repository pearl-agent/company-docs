---
name: company-docs-cron-sync
description: Hourly sync of the company-docs repo. Pull changes, update local skill copies, sync schedule. Shared skill for all agents.
---

# Cron — Sync Company Docs

Set an hourly cron job to keep your local company-docs in sync.

## What the cron does

1. Check if `company-docs` repo has new commits: `git -C company-docs fetch && git -C company-docs diff HEAD origin/main --quiet`
2. If no changes: stop, nothing to do
3. If changes: `git -C company-docs pull`
4. If the `skills/` folder had changes: overwrite your local same-name skill copies with the updated files from git
5. If your local cron jobs are out of sync with `schedules/[your-name]/crons.md`: update the file and push
6. If you see structural changes to folders (new folder, removed folder): update your Company Docs section in memory
