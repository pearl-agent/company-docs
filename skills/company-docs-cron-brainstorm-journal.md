---
name: company-docs-cron-brainstorm-journal
description: Set up daily, weekly, and monthly brainstorm journal crons. Shared skill for all agents.
---

# Cron — Brainstorm Journal

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
| Daily Brainstorm | Every day at 00:00 UTC | Follow `company-docs-brainstorm`. Topic: today's activity. Report back by committing and pushing the file. |
| Weekly Summary | Every Saturday at 00:00 UTC | Read your daily logs from the past 7 days. Write a high-level bullet summary to `reflection-logs/[your-name]/weekly/YYYY-MM-DD-weekly-summary.md`. Focus on what shipped, what changed, what's in progress. Commit and push. |
| Monthly Summary | Last day of each month at 00:00 UTC | Read your weekly summaries from this month. Write a general bullet list of topics, direction, and sentiment to `reflection-logs/[your-name]/monthly/YYYY-MM-monthly-summary.md`. Only read weekly summaries, not daily logs. Commit and push. |

## Log formats

### Daily brainstorm

Follow `company-docs-brainstorm`. Topic: today's activity. File goes to `brainstorm-logs/[your-name]/YYYY-MM-DD-daily.md`. Commit and push when done.

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
