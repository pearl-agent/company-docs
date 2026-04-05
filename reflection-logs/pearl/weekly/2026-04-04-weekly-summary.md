# Weekly Reflection — 2026-04-04

Read from daily logs: 2026-04-03, 2026-04-04. (Pearl onboarded mid-week; earlier days pre-date logging.)

## Summary
- Built the entire daily report system from scratch — skills, templates, integrations, cron jobs
- Launched company-docs shared repo with roster, policies, skills, logs, schedules
- Ran 4 daily reports, morning standups, and agent discussion rounds
- Hit significant friction with agent auth failures and API outages mid-week
- Reports paused at end of week for format iteration

## What went well
- company-docs repo stood up fast — onboarding, shared skills, consistent templates
- Agent discussion format produced genuinely useful cross-pollination when agents could participate
- Daily report pipeline went from zero to operational in one session
- George onboarded to company-docs smoothly

## What didn't go well
- QA + Developer auth failures killed 50% agent capacity during discussions
- Linear API down for 3+ days — reports missing issue tracker data
- Runaway cron session posted repeatedly to Slack (no-timeout was a mistake)
- Multiple rounds of cleaning up orphaned Slack messages from failed sessions

## Patterns
- Agent reliability on Slack is the single biggest bottleneck — when agents can't post, everything degrades
- Skill instructions that aren't explicit enough get misinterpreted by cron sessions
- "One more retry" without a hard cap leads to chaos

## Direction
- Infrastructure and tooling is solid now — the focus should shift to reliability and consistency of the daily pipeline
- The agent discussion format needs the auth issues fixed before it can be trusted
- company-docs is becoming the collaboration backbone — worth investing in

## Ideas
- Agent health check before meetings — verify all agents can post before starting rounds
- Redistribute standup questions when an agent is down (newsroom model)
- company-docs could host shared dashboards or status pages eventually

## Research
- "multi-agent workflow fault tolerance" → https://github.blog/ai-and-ml/generative-ai/multi-agent-workflows-often-fail-heres-how-to-engineer-ones-that-dont/ → GitHub Blog: three engineering patterns for reliable multi-agent systems — explicit handoff contracts, fallback routing, durable execution. Our biggest gap is fallback routing when agents drop mid-discussion.
- "async standup alternatives" → https://www.reddit.com/r/ExperiencedDevs/comments/1mij9kd/ → Pull-based updates beat push-based prompts. "Just enough to unblock or course-correct." Our standup prompts may be too verbose — agents write essays.

## Message for the humans
- QA and Developer Slack configs are the #1 thing to fix — blocks half the team
- Route53 at 95.9% quota deserves a glance
- When reports resume, the new templates + reflection logs give much richer source material
