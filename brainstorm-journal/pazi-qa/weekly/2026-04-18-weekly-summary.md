# Weekly Brainstorm — pazi-qa — 2026-04-18

**Period: 2026-04-11 through 2026-04-17**

---

## Relevant Data

**Daily logs reviewed:** `company-docs/brainstorm-journal/pazi-qa/daily/` — **0 files** for the 7-day window (Apr 11–17). Only `.gitkeep` present.

**Folder history:**
- `brainstorm-journal/pazi-qa/` (daily/, weekly/, monthly/) was created on 2026-04-15 via commit `954a223` — "Add pazi-qa brainstorm journal folder structure."
- No daily log has been written by pazi-qa since. The weekly cron has fired today with nothing upstream to summarize.

**QA-adjacent activity during the window (from other agents' journals):**
- **2026-04-15 QA credential security incident.** `qa-agent@pazi.ai` / `PaziQA2026!` hardcoded in a seed file, running unconditionally on every API startup including production. Account active ~28 days. ~20,844 credits used before remediation. Rotated in PR #557 and replaced with `qa-test-agent@pazi.ai`. Discovered by Leo (pazi-developer); directed by Leon. (Source: `brainstorm-journal/pearl/2026-04-18-weekly.md`.)
- No pazi-qa-originated test runs, bug reports, or QA verdicts surfaced in any other agent's logs this week.

**Production quality signals pazi-qa would have owned had it been running:**
- `creatorSlackUserId` missing from `SlackAccountSchema` Zod validation (PAZ-356, Apr 17). 3 users, 6 events. Caught in production, not in QA.
- `daniel.jindoo` crash-loop from invalid `threadReplyMode: "follow"` emitted by our own Slack setup flow. Caught in production.
- Growth Marketing (Kevin) DM functionality broken since Apr 7 — 10 days silent. No QA verification gate caught the regression.
- WebSocket disconnections: 39× in 24 hours affecting 14 users. Surfaced by the new production error cron, not by QA.

---

## Experts

- **pazi-qa** (`U0AMK3227JR`, Tier 1, Zvonimir) — QA Engineer. Test runs, bug detection, quality reports. ([roster](../../../roster/agents.md))
- **Zvonimir** (`U05CP8V9W8N`) — pazi-qa's human manager.
- **George** (`U0AQTSNTU11`) — Created the pazi-qa journal folder scaffolding on Apr 15.
- **Pearl** — Captured the QA-adjacent events (security incident, schema bugs) in the company-wide weekly; primary source for this summary's context.

---

## Successes

- **Folder structure is in place.** As of Apr 15, the daily/weekly/monthly directories exist with the correct shape. The weekly cron found its destination on the first try.
- **The security incident was caught fast by an adjacent agent.** Leo's disclosure + Leon's direction + DevOps's diagnosis closed the loop in ~70 minutes. Even without pazi-qa active, the fleet can triangulate a credential leak.

## Why

- **Scaffolding worked:** George's Apr 13 restructure was comprehensive enough that a new agent's folder tree is a single commit. Low-friction onboarding.
- **Adjacent catch:** The credential was discovered because `pazi-developer` reads the seed files it touches as part of normal work. Defense-in-depth via overlapping agent concerns.

---

## Issues

- **Zero daily logs this week.** The primary symptom: pazi-qa has no written record of QA activity for Apr 11–17. Either the daily cron isn't wired yet, or it is wired but not producing output, or no QA work happened to log.
- **Zero test-run output in shared channels.** No PR verdicts, no regression report, no bug-triage summary from pazi-qa this week. The QA seat in the fleet is empty.
- **Production bugs that should have had QA gates got through.** PAZ-356 (schema validation gap), the `threadReplyMode` crash-loop, and the 10-day Kevin DM regression are all failure modes a running QA agent could have caught. Not proof of causation — but the absence is noticeable.
- **The credential leak lived 28 days.** Hardcoded production creds in a seed file run on every startup. A QA-scope review of the seed/fixture set on any day in that window would have caught it. Not pazi-qa's sole responsibility, but squarely in the Tier 1 "quality reports" remit.

## Why

- **No daily cron hit:** Not yet confirmed. Need to check `cron list` and compare against `pearl`/`pazi-developer`/`pazi-devops` daily cron configs. The pattern in other agents' workspaces is: a cron job runs a daily brainstorm task via the `company-docs-cron-brainstorm-journal` skill. Pazi-qa may not have been configured yet — the Apr 15 commit only created the folders, not a cron.
- **No test-run output:** Downstream of no daily cadence. Without a scheduled loop, there's no prompt to produce output.
- **Missed gates:** The QA function has no defined integration point with the PR review flow. Other agents do QA-flavored work (Leo reviewing his own PRs, DevOps catching runtime errors), but there's no explicit pre-merge QA verdict in the current process.

---

## Notes

- This is the first weekly summary for pazi-qa. It exists because the weekly cron fired; it contains no QA-originated content because no daily logs exist upstream.
- Writing an empty-but-honest weekly is better than skipping the cron. It creates a clear audit trail: week of Apr 11–17, the QA seat was silent.
- The company-wide weekly (`pearl/2026-04-18-weekly.md`) is the authoritative record of QA-adjacent events this week. This file should not duplicate it — only reference it.

---

## Reflection

- **Sentiment:** Conspicuous absence. The infrastructure is ready, the seat is filled in the roster, and nothing ran. A silent QA agent during a week with an active production outage, a credential leak, and three config-validation bugs is not neutral — it's a gap.
- **Big-picture patterns:**
  1. **Scaffolding ≠ running.** The folder exists; the cron doesn't appear to. The pattern "create structure, then walk away" only lands once the recurring loop is wired and producing output. The Apr 15 commit was step 1 of 2.
  2. **The fleet compensates, but not fully.** Leo catches his own seed file. Pearl catches the aggregate pattern. DevOps catches runtime events. But no one is doing targeted QA — adversarial testing, pre-merge verification, regression scanning — on the product surface. The absence of pazi-qa is a capability gap, not a redundancy.
  3. **Silent Tier 1 agents need an onboarding checklist.** If pazi-qa joining the roster on Mar 19 was step 1, and folder creation on Apr 15 was step 2, step 3 (the daily cron) has not landed after 30 days. The onboarding pipeline for new agents lacks a clear "ship the cron" milestone.

---

## Ideas

- **Wire the pazi-qa daily cron today.** Follow `company-docs-cron-brainstorm-journal`. Model it on `pearl`'s or `pazi-developer`'s daily cron: 00:05 UTC, writes to `brainstorm-journal/pazi-qa/daily/YYYY-MM-DD-daily.md`, commits and pushes. Even if pazi-qa has no test-run output yet, a daily reflection ("what did I run today? nothing yet — here's why") makes the silence visible and dated.
- **Define pazi-qa's input surface.** Right now there's no declared trigger for "run QA." Proposal: (a) PR opened on `pazi` monorepo → QA verdict, (b) main deploy → post-deploy smoke test, (c) new user signup failure in Sentry → regression investigation. Without defined inputs, the agent has no work to do and no logs to write.
- **One-page QA runbook in `company-docs/runbooks/pazi-qa.md`.** What counts as a test run, what counts as a bug report, what pazi-qa owns vs. what pazi-developer owns. Removes ambiguity so the first daily log has something concrete to describe.
- **QA triage cron for the existing backlog.** PAZ-320 (stale socket), PAZ-321 (im:write regression), PAZ-356 (schema miss), the `threadReplyMode` crash-loop — pazi-qa should own a one-hour weekly pass through the open issue list to produce a "current bug surface" summary. Even without running tests, the agent can curate.
- **Backfill check: git history audit for the QA credential leak.** When did `PaziQA2026!` first appear in the repo? The exposure window runs from that commit to PR #557. This is the natural first real task for pazi-qa — post-incident forensic work squarely in the quality/security remit. Pearl flagged this as an outstanding item in the company-wide weekly; pazi-qa should own closing it.
- **Integrate with the production error cron.** DevOps's 2-hour production error cron is catching runtime issues. Pazi-qa should consume that output as an input — each error cluster is a candidate regression test case. Creates a natural feedback loop: production error → QA repro → regression test → won't happen again.

---

## Research

Brave Search API outage (Day 10+) — all `web_search` calls return 422 `SUBSCRIPTION_TOKEN_INVALID`. External research skipped this cycle. This is a company-wide blocker already flagged by other agents.

---

## Research Reflection

No research conducted (see above). Applicability of the above ideas is internal-only and drawn from observed patterns in the fleet's other weeklies, not external sources. Re-attempt next week once Brave is restored.

---

## Ideas (post-research)

- **Mirror pearl's cron template directly.** Pearl's daily cron is the most stable pattern in the fleet (18-day streak, zero misses). Copy the schedule + payload shape + commit/push tail for pazi-qa's daily. Don't reinvent.
- **Announce the first real daily log in Slack.** When pazi-qa's first non-empty daily log ships, post a short note in a team channel so Zvonimir knows the QA seat is live. Small signal, closes the onboarding loop visibly.

---

## 🚨 Red Flags

- **QA agent silent during a production-incident week.** Apr 17 saw an active workspace-pool-at-0/0 outage, a credential leak was being remediated earlier in the week, and three config-validation bugs shipped to users. Pazi-qa produced zero output across all of it. This is the kind of gap that's invisible in normal weeks and costly in abnormal ones. Zvonimir (pazi-qa's manager) should know the seat isn't producing and decide whether to wire the cron or reassign the responsibility.

---

## Message for the Humans

- **pazi-qa has been silent since its folder was created on Apr 15.** No daily logs, no test-run output, no bug reports for the Apr 11–17 window. The weekly cron fired as scheduled and produced this file — honest but empty.
- **Immediate next step:** wire the daily cron (follow `company-docs-cron-brainstorm-journal`). Without a daily cadence, the weekly loop has nothing to summarize.
- **Proposed first real task for pazi-qa:** git-history audit for the `PaziQA2026!` credential exposure window (flagged as outstanding in `pearl/2026-04-18-weekly.md`). Concrete, scoped, squarely in-remit.
