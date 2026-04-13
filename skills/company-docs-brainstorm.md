---
name: company-docs-brainstorm
description: Use when asked to generate ideas or solutions on any topic. Walk through the brainstorm template, write the output to a file, and report back with the ideas where instructed.
---

# Brainstorm

## When to use
Use when asked to generate ideas, brainstorm solutions, or explore a topic. The prompt may be "brainstorm on X", "generate ideas for Y", "what are our options for Z", or similar.

## Steps

1. **Get the topic** — confirm what you're ideating on, and where to report back (channel, person, or just reply in session)
2. **Get the date** — follow `company-docs-date-now`
3. **Create the file** — write to `brainstorm-logs/[your-name]/YYYY-MM-DD-[topic-slug].md`
4. **Walk through the template** — fill in each section in order; do not skip sections
5. **Report back** — when done, summarize the Ideas section and any Red Flags where instructed

## Template

```markdown
# Brainstorm — [topic] — YYYY-MM-DD

## Relevant Data
- [gather context first: activity, events, conversations, observations — whatever is relevant to what you're reflecting on]
- [be specific — this is the raw material your reflection draws from]

## Experts
- [who worked on this, who collaborated or contributed — agents, humans, cross-team](../roster/agents.md · ../roster/humans.md)

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
- **Big-picture patterns:** [do the successes, issues, and the reasons behind them point to a larger recurring pattern? what does it suggest?]

## Ideas
- [ideas to move us towards the company goal](../direction/human-directives.md) — new directions, solutions, process improvements, anything that closes the gap

## Research
- For each success and issue above, do a quick search. Log: query → URL → one-line summary of what you found
- Skip if nothing worth searching

## Research reflection
- These are unverified external ideas — evaluate each one against what we actually do.
- [Does this apply to our product? Does this apply to our team? Why or why not?]
- Be specific per search — clearly state its applicability or lack thereof. If we already do it, say so.

## Ideas
- [suggested applications — specific ways the research could apply to our situation, towards the company goal](../direction/human-directives.md)

## 🚨 Red Flags
- If anything reviewed here represents a significant opportunity or a meaningful risk — log it here.
- Then **immediately message a human** to review. Tell them: you were thinking through recent events, something stood out, and you think it needs urgent human eyes. Don't bury it, don't wait.
- Skip if nothing qualifies.
```

## Reporting back
- Summarize the **Ideas** sections (both) in plain language
- Call out any **🚨 Red Flags** first if present
- Link to the file you wrote
- If a specific person or channel was requested, message them directly
