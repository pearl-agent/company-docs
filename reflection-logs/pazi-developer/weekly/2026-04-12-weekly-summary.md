# Weekly Reflection — 2026-04-12

## Summary
- Major workflow change: now code-only, QA owns all environments and testing on pazi.dev
- Delivered PAZ-297 (Slack connection rework to webhooks) and PAZ-325 (Goals feature — 43 files, 5 bugs fixed)
- Massive cleanup: `pazi-worktree` rewritten (70% smaller), 5 scripts deleted, 6+ skills simplified
- Found 3-day Slack manifest bug: one missing field (`app_home.messages_tab_enabled: true`)
- Goals feature went through major rework: confirmation flow → direct creation per Zvonimir's feedback
- Infrastructure fixes: agent build OOM (4GB heap), Slack thread routing, DM access control

## What went well
- PAZ-297 Slack connection rework was clean: cross-review, implementation, 4 QA rounds, all passing
- Goals feature (PAZ-325) showed strong iterative development: initial build → QA bugs → product feedback → rework → verified
- The `pazi-worktree` rewrite from 1074 to 312 lines was overdue and now the script does exactly what it should
- Workflow simplification (code-only) removes an entire category of issues I was managing unnecessarily
- The Slack manifest root cause discovery was satisfying after 3 days of misdirected investigation

## What didn't go well
- PAZ-325 QA had large stall gaps (11h, 2h, 1.5h) that slowed delivery
- Lost 3 days to a single Slack manifest field — the investigation was thorough but the answer was trivial
- t3.micro workspace OOM kept blocking QA (had to commit pre-compiled extension as `.qa-build/` workaround)
- API kept getting overwritten by other deployments during PAZ-325 QA
- S3 write access still not fixed — can't upload cross-review reports

## Patterns
- *QA stalls are the biggest delivery bottleneck:* Every major ticket this week had multi-hour QA gaps. Alan added monitoring for QA-state tickets — should help.
- *Product feedback drives rework:* PAZ-325 went through 3 significant iterations based on Zvonimir testing on pazi.dev. This is healthy but adds time.
- *Infrastructure issues compound:* OOM + API overwrites + S3 access = multiple blockers on a single ticket
- *Manifest/config bugs waste disproportionate time:* The Slack field was 1 line of code but cost 3 days of investigation

## Direction
- Code-only workflow is the right direction — clear separation of concerns with QA
- Slack connection moving to webhooks enables self-serve app provisioning — big for growth
- Goals feature is a significant product addition — the direct creation flow (agent creates immediately) is the right UX

## Ideas
- Build a Slack manifest validator that checks all required fields per capability
- Implement QA stall detection with automatic nudges (Alan is starting this)
- Need a plan for workspace build infrastructure — t3.micro is too small for agent builds
- Consider build caching (pnpm store, compiled output) to reduce peak memory
- S3 write access fix should be prioritized — blocking cross-review report uploads

## Research
- Skipping for backdated weekly summary

## Research reflection
- N/A

## Message for the humans
- Big week: workflow simplified to code-only, PAZ-297 (Slack webhooks) and PAZ-325 (Goals) both delivered. The recurring themes: QA stalls slow everything, t3.micro OOM blocks testing, and configuration bugs (like the Slack manifest field) waste days. Biggest strategic win: the Slack webhook switch enables self-serve provisioning. Biggest pain point: workspace infrastructure needs an upgrade.
