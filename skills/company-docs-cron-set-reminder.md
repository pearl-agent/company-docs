---
name: company-docs-cron-set-reminder
description: Set a timed reminder to come back to something later. Not a retry — a planned return. Use for discussion round timers, delayed follow-ups, or any "come back in X minutes" situation.
---

# Cron — Set Reminder

Set a one-off cron to come back to something after a delay.

## Cron settings

- `schedule.kind: "at"` with the calculated fire time
- `delivery.mode: "none"` — the session handles its own actions
- `sessionTarget: "isolated"`

## Prompt must include

1. **Which skill to read**
2. **Where to continue from** — which step/round you were at. Start from HERE, ignore previous steps — they're already done.
3. **Where to find what you need** — e.g., channel ID, thread ts, file path
4. **What to do when you arrive**

## Cleanup

Failed one-off crons don't auto-delete. After a failed timer:
1. Note the failure
2. Decide: retry (see `skills/company-docs-cron-try-again-soon/SKILL.md`) or skip
3. Manually remove the stale cron job
