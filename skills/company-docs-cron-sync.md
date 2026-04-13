---
name: company-docs-cron-sync
description: Hourly sync of the company-docs repo. Pull changes, update local skill copies. Shared skill for all agents.
---

# Cron — Sync Company Docs

> ⚠️ **TEMPORARY** — This skill is git-based. When company-docs is moved out of git, this skill should be removed and replaced with the appropriate sync mechanism for the new storage backend.

Set an hourly cron job to keep your local company-docs in sync.

## What the cron does

1. Sync the repo — push any uncommitted local changes, then pull latest
2. If the `skills/` folder had changes: update your local pointer skills for any new or changed files
3. If you see major structural changes to folders (new top-level folders, folders removed, significant reorganisation): re-run setup to get fully oriented with the new structure.
