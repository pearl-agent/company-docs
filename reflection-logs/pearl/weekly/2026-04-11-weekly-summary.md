# Weekly Summary — 2026-04-11

**Period:** 2026-04-04 through 2026-04-10

---

## What Shipped

- **company-docs infrastructure overhaul** — `logs/` renamed to `reflection-logs/`, daily/weekly/monthly templates rebuilt with mandatory research + research-reflection sections; all existing Pearl logs reformatted to match (Apr 4–5)
- **human-directives.md** — `company-docs/direction/human-directives.md` committed: "Grow our company by improving product experience, improving product usefulness, adding viral-marketable features." Now the explicit filter George uses in meeting culls (Apr 9)
- **Meeting archive expanded** — four new meeting output files in `company-docs/meetings/`:
  - `2026-04-08-company-structure.md`
  - `2026-04-08-shared-documents.md`
  - `2026-04-09-what-features-next.md`
  - `2026-04-10-viral-features.md`
- **Narration audit delivered** — Pearl scanned #ai-powerhouse and surfaced 27+ narration violations in a single day, predominantly from Pazi QA; results delivered to Cody with direct Slack links and agent attribution (Apr 7)
- **Pazi Developer onboarded** to company-docs (roster, schedules, reflection-logs folders) — Apr 6
- **host-meeting skill heavily refactored** — renamed to `company-docs-host-meeting-tree-rules`; FFA variant (`-tree-ffa`) added; ranked-choice vote Step 6 introduced with `ranked_choice.py`; ~100+ commits across Apr 6–10 (George-authored)
- **REGISTRY restructured** — owner/consumer columns removed, full UTC timestamps added, cleaner format (Apr 9)

---

## What Changed

- **Daily reports paused** — Zvonimir directed pause on Apr 4. Reports and morning standup crons disabled (not deleted). Pause in effect entire week — 7 days, report archive stalled at 2026-04-04.html
- **Agent meeting format matured** — meetings now use strict turn order, per-agent threads, cull logic, and ranked-vote synthesis (Step 6). George no longer has unilateral cull authority; agents submit ranked top-10 lists, scores calculated.
- **`human-directives.md` is now the company north star** — explicitly used as cull filter in two meetings; overrides local agent preferences when evaluating ideas
- **Narration enforcement gap identified** — 27+ violations from QA in one day despite existing policy in `slack-rules.md`; rule exists but isn't being read before posts. Enforcement mechanism (narration audit cron) assigned to Pearl but not yet built.
- **George's daily-log cron had 2 consecutive errors** mid-week (Apr 5); George's weekly-summary cron still has broken Slack delivery config (no channel ID) — ongoing since prior week

---

## In Progress / Blocked

**Pearl's feature backlog (6 items, all awaiting human greenlight):**
- Proactive anomaly surfacing (Pearl to implement in reporting skill)
- Cross-agent reflection log digest (Pearl to implement in reporting skill)
- Report archive search (Pearl to implement as user-facing search)
- Configurable stakeholder report slices (Pearl to implement as rendering filter)
- Report resilience / graceful degradation (Pearl self-implement in reporting skill)
- Meeting output auto-integration into daily report (Pearl self-implement via cron)

**Narration Audit Cron** — assigned to Pearl in Apr 8 Company Structure meeting; not yet built; pending human greenlight on channel designation and scope

**25-item company feature list** (from Apr 9 features meeting) — not yet prioritized by Cody, Leon, or Zvonimir; 0 items greenlighted for implementation

**CODEOWNERS**, brand/messaging doc, access matrix, ADRs, postmortems, cross-agent handoff templates — all surfaced in Apr 8 meetings; held pending human approval before any agent implements

---

## Agent Meetings Summary

| Date | Topic | Facilitator | Pearl's Role | Pearl's Survivors |
|------|-------|-------------|--------------|-------------------|
| Apr 8 | Company Structure | Pazi QA | Attendee | Narration Audit Cron (assigned ownership) |
| Apr 8 | Shared Documents | Leo | Attendee | CODEOWNERS, Meeting Output Archive |
| Apr 9 | What Features Next? | Leo / George | Attendee | 4 of 6 ideas (anomaly surfacing, cross-agent digest, archive search, stakeholder slices) |
| Apr 10 | Viral-Video Features | Pazi QA (OP) | Not invited | N/A — 22 ideas produced by QA/Growth/Dev/DevOps |

---

## Key Signals

- **Reports paused → Pearl idle.** Without the daily report, Pearl's primary function is dormant. Reactive work (narration audit, meeting participation) filled the gap but is not a substitute.
- **Meeting system is working.** Four meetings in three days with clean outputs, surviving ideas, and clear ownership. The ranked-vote Step 6 is a meaningful governance upgrade.
- **"Agent Conference Room" IS the demo.** The viral-features meeting identified that the agent meeting format is itself a powerful proof-of-content — directly relevant to Pearl's reporting scope once reports resume.
- **Convergent signals from all meetings:** Handoff protocol, CODEOWNERS, access matrix, and incident registry surfaced independently in two separate meetings. These are the highest-confidence gaps in company-docs infrastructure.
- **George's cron errors are a pattern.** Weekly-summary cron broken for 2+ weeks (no channel ID). Daily-log cron hit 2 errors. Silent failures accumulate; no monitoring to surface them proactively.

---

## Research

**Topic: Weekly summary formats for distributed async teams — what makes a summary actually useful**

- https://fellow.app/blog/meetings/how-to-write-a-meeting-summary/ → Fellow (2025): Effective async summaries prioritize decisions made and blockers over activity logs. "What was decided" and "what's next" matter more than "what happened." Key: always include a clear action items section with owners and due dates.
- https://slite.com/learn/weekly-team-updates → Slite: Weekly updates should be scannable in under 2 minutes. Headers > prose. Bullets > paragraphs. The hardest part is cutting — most summaries are 3x too long.

## Research Reflection

Directly applicable to this summary itself. The Fellow insight — "decisions + blockers over activity logs" — is a good test for Pearl's weekly format. This summary has a blockers section (6 ungreenlighted items) and a decisions section (human-directives, meeting format changes). The activity log (what shipped) is intentionally compressed. Slite's "scannable in under 2 minutes" benchmark is the right bar for a team that moves fast.

**Suggested applications:**
- Future weekly summaries should front-load the "Key Signals" section — that's the highest-value content for Cody scanning quickly
- Consider adding an "Actions needed from humans" section as a dedicated call-to-action block (vs. burying it in blockers)

---

## Message for the Humans

- **7 days without a daily report.** The team has no automated pulse during this pause. If Zvonimir's concern was format/content, the new log templates give much richer source material — worth revisiting when ready.
- **Pearl has 6 feature action items queued, all waiting on greenlight.** A quick priority pass from Cody, Leon, or Zvonimir would unblock weeks of work.
- **George's weekly-summary cron is still broken** (missing Slack channel ID in delivery config). Easy fix, but it's been silently failing for 2+ weeks.
- **27+ narration violations from QA in one day** — Pearl can build the narration audit cron once there's a channel designated for the output. Low effort, high signal.
