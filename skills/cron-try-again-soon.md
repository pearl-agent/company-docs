---
name: company-docs-cron-try-again-soon
description: Retry a failed operation with escalating delays. Use when an API call, data fetch, or lookup fails and should be retried.
---

# Cron — Try Again Soon

When something fails, set a one-off cron to retry with escalating delays.

## Suggested delays

| Attempt | Delay |
|---------|-------|
| 1 | 2 minutes |
| 2 | 5 minutes |
| 3 | 15 minutes |

These are suggestions, not hard limits. Adjust per situation.

## Max attempts

3 suggested, 5 absolute max. After the final attempt fails: skip the section and log why in raw data + report files.

## Cron settings

- `schedule.kind: "at"` with the calculated fire time
- `delivery.mode: "none"` — the session handles its own posting
- `sessionTarget: "isolated"`

## Prompt must include

1. **What failed** — the specific operation
2. **Error details** — the error code or message
3. **Which skill and step** — where you were when it failed
4. **Attempt number** — which attempt this is, out of how many
5. **Troubleshooting** — don't blindly retry. Investigate what's most relevant before retrying.
6. **Logging instructions** — where and in what format to log this attempt, as specified by the skill that triggered the retry. Every attempt MUST be logged — the calling skill dictates where and how.

## After all retries fail — or if retries are not relevant/possible

- Skip the section
- Log the final failure per the calling skill's logging instructions
- Note in any output (report, message, etc.): section unavailable, reason
- Escalate to a human: post in your team's channel describing what failed, whether retries were attempted or why they weren't possible, and ask for help. Tag the human whose specialty is most relevant (see `company-docs/roster/humans.md`).

## Cleanup

Failed one-off crons don't auto-delete. After a failed timer:
1. Note the failure
2. Follow retry procedure
3. Manually remove the stale cron job
