# Brainstorm — Viral-Marketable User-Facing Features — 2026-04-14

## Relevant Data

- **Company North Star:** "Meteoric rise through a sensational product — so useful people rely on it, so fun they can't put it down."
- **Goals explicitly include:** Viral-marketable features, fun usability that sparks curiosity, polished UX people screenshot and share, cutting-edge positioning.
- **Current state:** Pazi is an AI assistant platform. Team is in pre-launch/fast iteration phase. Agent infrastructure is maturing (Pearl, George, Wallace, DevOps, QA, Developer, CX, Growth, Tech Lead, Onboarding Manager).
- **Recent signals:** 31+ feature ideas voted on in Apr 8–9 meetings, none yet greenlighted. Daily reports paused. Team is building agent infrastructure and multi-agent coordination systems.
- **My vantage point:** I read every deploy, PR, Linear issue, and Slack update. What I consistently notice is that the things that *look impressive from the outside* rarely match what the team thinks is impressive internally. Engineers celebrate correctness; users celebrate magic.

## Experts

- **Cody** (`U098CNKQ2JV`) — Founder. Sets direction. Wants viral + fun.
- **George** (`U0AQTSNTU11`) — Agent Manager. Designs agent coordination systems.
- **Pearl** — Reporter. Sees the full picture of what ships and what gets talked about.
- **Pazi Growth agent** — Social media and marketing focus.

## Successes

- Multi-agent coordination infrastructure is operational (standup, meetings, reports, discussion rounds)
- Agent onboarding is fast and reliable (Wallace went from zero to crons in one session)
- Daily log streak: 14 consecutive days of perfect uptime on automated cron

## Why

- The infrastructure is reliable because it's simple — one cron, one task, low surface area
- The coordination features (meeting engine, discussion rounds) are impressive because they're observable: you can watch agents interact in real time

## Issues

- 31+ voted ideas sitting idle — the gap between "great idea" and "shipped feature" is too wide
- Primary user-facing output (daily reports) has been paused 10 days — no visible product activity to showcase
- Brave Search API down — reduces research capability for all agents
- Nothing shipped recently that a user could screenshot and share

## Why

- The pause is top-down (policy hold), not capability failure
- The gap between idea and shipped feature reflects lack of authority handoff — no human greenlight = no action
- "Impressive to engineers" ≠ "impressive to users" — the team has built plumbing that users never see

## Notes

- The virality pattern in AI products in 2024–2026 follows a consistent formula: **show the agent doing something unexpected, in real-time, that feels like magic**. Text → action → visible result = shareable moment.
- The products that went viral (Perplexity, Character.AI, Rabbit, Claude Artifacts) all had one thing in common: a single "holy sh*t" moment that was trivially easy to demo in 60 seconds.
- Pazi's current architecture (multi-agent, real-time coordination) is *already the kind of thing that could be that moment* — it just hasn't been packaged for an audience yet.

## Reflection

- **Sentiment:** There's a real gap between what we've built and what's visible. The infrastructure is genuinely impressive. The user experience of that infrastructure is invisible.
- **Big-picture patterns:** Pazi's virality bottleneck isn't ideas — we have 31+. It's packaging. The features that go viral are the ones that are easy to demo, easy to understand, and easy to share in 30 seconds. Everything else is a blog post nobody reads.

---

## Ideas

From what I observe across every report, PR, and team interaction:

1. **Agent Live Feed** — A public-facing "Pazi Mission Control" view: real-time stream of what your agents are doing, in plain English. "George just reviewed 14 Linear issues." "Pearl just filed a report." Users love watching AI work. Observable AI = shareable AI.

2. **"Watch Me Work" Screen** — When a user asks an agent to do something complex, a split-panel view shows the agent's reasoning steps in plain language alongside the output. Like watching someone think. Makes the invisible visible. Trivially screenshot-able.

3. **Agent Highlight Reel** — Daily or weekly auto-generated short video/GIF of the most interesting agent moments ("your agents did 47 things today — here's the best one"). Shareable on social, zero user effort required.

4. **Personality Skins / Personas** — Let users configure their agent's personality: "corporate", "hype man", "stoic", "roast me". Same capability, different voice. Wildly shareable when people post funny outputs.

5. **Agent-to-Agent Debates** — Surface the multi-agent meeting system as a product feature. Users pose a question; two agents argue both sides; user gets a structured pros/cons answer. The disagreement is the product. People share debates.

6. **"Caught It" Notifications** — Agent proactively surfaces a thing it found before you asked. "Pearl noticed you have a meeting conflict tomorrow." "Your agent flagged a risky deploy." Push notification for the unexpected catch. Trust-building and shareable ("my AI is smarter than I thought").

7. **Public Agent Profiles** — Let users share a public URL for their agent: what it does, what it's good at, recent wins. Like a portfolio page, but for your AI. Social proof engine built-in.

8. **Zero-Setup Agent Templates** — One-click agent configurations for common personas: "my personal reporter", "my dev assistant", "my growth advisor". Named, opinionated, and immediately usable. Reduces onboarding friction to near zero — and each template is a piece of shareable marketing content.

9. **Agent Memory Replay** — "Here's what your agent remembers about you." A beautifully-formatted summary of what the agent has learned. Surprising, personal, and slightly eerie in the best way. People screenshot this.

10. **Cross-Team Challenge Mode** — Two teams configure their agents against the same task; results compared. Like a live coding challenge but for AI setups. Leaderboard optional. Competitive feature = social feature.

---

## Research

Web search unavailable (Brave Search API token invalid, day 4+ outage). Research section skipped.

## Research Reflection

No external research available this cycle. Ideas above are drawn from pattern observation across Pazi activity logs and known AI product viral moments (Perplexity, Character.AI, Claude Artifacts, Rabbit r1 launch).

## Ideas

_(Research-driven section skipped — no search capability)_

---

## 🚨 Red Flags

- **31+ voted features ungreenlighted for 5+ days.** Every day without action is a day the team's momentum stalls. Not a crisis yet — but if another week passes with no greenlight on any of those items, we're in drift territory. Worth human eyes sooner than later.
- **No shareable product moment exists yet.** If Pazi went to Product Hunt tomorrow, what would the hero demo be? I can't answer that confidently. That's a gap.
