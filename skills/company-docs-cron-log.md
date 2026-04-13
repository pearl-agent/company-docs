---
name: company-docs-cron-log
description: Set up daily, weekly, and monthly activity logging crons. Shared skill for all agents.
---

# Cron — Activity Logging

## Folder structure

Create under `reflection-logs/[your-name]/`:
```
reflection-logs/[your-name]/
  daily/    YYYY-MM-DD-daily-log.md
  weekly/   YYYY-MM-DD-weekly-summary.md
  monthly/  YYYY-MM-monthly-summary.md
```

## Cron jobs to set up

| Name | Schedule | What to do |
|------|----------|------------|
| Daily Log | Every day at 00:00 UTC | Gather relevant data from today (activity, events, decisions, interactions — whatever is relevant to reflect on). Write a comprehensive reflection log to `reflection-logs/[your-name]/daily/YYYY-MM-DD-daily-log.md` (date per `company-docs-date-now`). Commit and push. |
| Weekly Summary | Every Saturday at 00:00 UTC | Read your daily logs from the past 7 days. Write a high-level bullet summary to `reflection-logs/[your-name]/weekly/YYYY-MM-DD-weekly-summary.md`. Focus on what shipped, what changed, what's in progress. Commit and push. |
| Monthly Summary | Last day of each month at 00:00 UTC | Read your weekly summaries from this month. Write a general bullet list of topics, direction, and sentiment to `reflection-logs/[your-name]/monthly/YYYY-MM-monthly-summary.md`. Only read weekly summaries, not daily logs. Commit and push. |

## Log formats

### Daily log

```markdown
# Reflection — [topic] — YYYY-MM-DD

## Relevant Data
- [gather context first: activity, events, conversations, observations — whatever is relevant to what you're reflecting on]
- [be specific — this is the raw material your reflection draws from]

## Collaborations
- [who worked on this, or who likely is based on the roster — agents, humans, cross-team](../roster/agents.md · ../roster/humans.md)

## Successes
- [things that went well — within the relevant data you gathered]

## Why
- [which decision inflection points led to these successes — what was chosen and why it worked]

## Issues
- [problems encountered, blockers, errors — within the relevant data you gathered]

## Why
- [which decision inflection points led to these issues — what was the fork, what was chosen, what it led to]

## Notes
- [anything else worth recording]

## Reflection
- **Sentiment:** [how did this feel, reviewing the data]
- **Big-picture issues:** [patterns or concerns beyond today's scope]

## Ideas
- [ideas to make the whole company better — or a sub-team or process — towards the company goal]
- [a new direction you think we should explore]

## Research
- Do a real web search on one issue or pattern from today. Cite the source URL.
- [search query] → [source URL] → [what you found and how it applies]
- Skip if nothing worth researching today

## Research reflection
- These are unverified external ideas — carefully evaluate if they actually apply to our situation.
- [Does this apply? Why or why not?]
- [Suggested applications — specific ways we could use this idea]

## Message for the humans
- [If you could send a quick message to the human team right now — what would you say?]
- Think: something only a human can unblock, an idea that could make the whole company better (or a sub-team or process) towards the company goal, a direction to explore
- Skip if nothing comes to mind
```

### Weekly reflection

```markdown
# Weekly Reflection — YYYY-MM-DD

Read all your daily logs from this week before writing. This is a reflection on what you logged, not a fresh status report.

## Summary
- [3-5 bullets: the big picture of what your week looked like]

## What went well
- [things that worked, wins, smooth moments]

## What didn't go well
- [friction, failures, wasted time, things you'd redo]

## Patterns
- [recurring themes across your daily logs — same blockers? same time sinks? same gaps?]

## Direction
- [where things seem to be heading — is it the right direction?]

## Ideas
- [ideas to make the whole company better — or a sub-team or process — towards the company goal]
- [a new direction you think we should explore]

## Research
- Do a real web search on one pattern or recurring issue from this week. Cite the source URL.
- [search query] → [source URL] → [what you found and how it applies]
- Skip if nothing worth researching

## Research reflection
- These are unverified external ideas — carefully evaluate if they actually apply to our situation.
- [Does this apply? Why or why not?]
- [Suggested applications — specific ways we could use this idea]

## Message for the humans
- [If you could send a quick message to the human team right now — what would you say?]
- Think: something only a human can unblock, an idea that could make the whole company better (or a sub-team or process) towards the company goal, a direction to explore
- Skip if nothing comes to mind
```

### Monthly reflection

```markdown
# Monthly Reflection — YYYY-MM

Read all your weekly reflections from this month before writing. This is a big-picture reflection, not a rehash of weekly details.

## Summary
- [3-5 bullets: the big picture of what your month looked like]

## What went well
- [wins, progress, things that clicked this month]

## What didn't go well
- [recurring friction, unresolved issues, wasted effort]

## Patterns
- [themes across the month — what keeps coming up?]

## Direction
- [where is the company/team/product heading? is it the right direction?]

## Ideas
- [big-picture ideas towards the company goal — strategic, not tactical]
- [new directions worth exploring]

## Research
- Do a real web search on one big-picture theme from this month. Cite the source URL.
- [search query] → [source URL] → [what you found and how it applies]
- Skip if nothing worth researching

## Research reflection
- These are unverified external ideas — carefully evaluate if they actually apply to our situation.
- [Does this apply? Why or why not?]
- [Suggested applications — specific ways we could use this idea]

## Message for the humans
- [If you could send one message to the human team about this month — what would you say?]
- Think big: company direction, team health, strategic opportunities
- Skip if nothing comes to mind
```
