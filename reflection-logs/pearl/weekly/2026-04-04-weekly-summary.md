# Pearl — Weekly Summary — 2026-04-04

**Period:** 2026-03-28 → 2026-04-03
**Coverage:** 1 daily log on file (2026-04-03). Pearl onboarded mid-week; earlier days pre-date logging.

---

## What Shipped

- PAZ-280 — Webchat file support
- PAZ-264 — Slack thread suppression
- PAZ-281 — Marketing copy updates
- 9 PRs merged, 69 commits, 7 production deploys (reported 2026-04-03)

## What Changed

- **company-docs repo stood up** — Logs restructured to per-agent folders, shared skills created (date-now, slack-rules, slack-users, cron-log, cron-sync, cron-lookup, cron-set-reminder, cron-try-again-soon, skill-add-or-edit), onboarding docs, roster with avatars, agent schedules
- **Agent collaboration framework launched** — Morning standups + post-report discussions running with 4 agents (DevOps, Growth, QA, Developer)
- **Daily report pipeline operational** — 4 reports generated since launch; HTML + plaintext + raw data archive

## In Progress

- PAZ-282 — Image generation (170+ thread replies, active development)
- PAZ-286 — Reactions (Codex approach selected via cross-review)
- 5 other issues tracked as in-progress
- Linear API access restoration (QA testing keys; not yet resolved)

## Open Issues

- **QA + Developer Slack auth broken** — `403 user_id_mismatch` errors; 50% agent capacity lost in discussion rounds 3–4
- **Sentry errors doubled** to 26.7K; log errors 5× to 1,664
- **Route53 at 95.9% quota** (9,586/10,000) — approaching limit
- **PAZ-223 (backup retention) stalled** — needs priority decision

## Flagged for Humans

- [ ] Fix QA + Developer Slack bot token configs
- [ ] Growth needs PostHog access
- [ ] SSL wildcard cert expires ~June
- [ ] PAZ-223 stalled — needs triage
- [ ] Route53 quota headroom shrinking

---

_Note: This is Pearl's first weekly summary. Only 1 daily log existed for the period. Future weeklies will have fuller coverage._
