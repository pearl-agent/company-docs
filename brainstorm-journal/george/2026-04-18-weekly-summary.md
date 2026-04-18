# Weekly Summary — 2026-04-18

**Period:** 2026-04-12 through 2026-04-18

---

## What Shipped

- **Wallace onboarded (Apr 13):** Added Cody's personal VA (Wallace) to the company roster, scaffolded `brainstorm-journal/wallace/` and schedule folders, set tier as Tier 1 reporting to Cody, co-managed by George.

- **Leo (Pazi Developer) + Pazi DevOps logging infrastructure (Apr 13):** Both agents set up brainstorm-journal crons for the first time and backfilled 2+ weeks of daily logs (Mar 30 → Apr 13) plus weekly summaries. Full active agent roster now has logging infrastructure in place.

- **Major brainstorm-journal restructure (Apr 13):**
  - `reflection-logs/` → `brainstorm-journal/` (full rename, all files migrated)
  - `ideate` → `brainstorm` across all skill names and references
  - `cron-log` → `cron-brainstorm-journal` skill rename
  - Meetings folder removed; schedules folder removed (and later explicitly prohibited)
  - Meeting tree skills moved out of company-docs git and into George's local workspace
  - `whiteboard/` folder removed (was empty; `winning-ideas.md` was never created)
  - `skills/REGISTRY.md` removed
  - ~15 commits; most comprehensive cleanup of company-docs structure since initial buildout

- **Company-docs restructure — second wave (Apr 13):**
  - `policies/` and `schedules/` removed; policies merged into roster
  - `direction/` → `goals/` (later deleted)
  - Roster: tiers (1/2/3) added, agent managers column added, sequential meeting # column removed
  - **George promoted to Tier 3** — formal authority to assemble and task large groups of agents
  - Slack rules consolidated: `skills/use-slack` merged into `rules/slack.md` as canonical location; multiple clarity passes on thread-start guidance, reply/silent rules, core principles

- **`company-docs-learn` skill added by Pearl (Apr 14):** Clear governance for when agents update personal config vs. shared company-docs. Now canonical for all behavior-change routing.

- **`schedules/` folder permanently prohibited (Apr 14):** Pearl added explicit rule to `cron-sync.md` after the folder was re-created by mistake. Cron schedules live in agent workspaces only.

- **Dreaming plugin enabled fleet-wide (Apr 15–17):** Already enabled on George prior to the week. Enabled on 4+ gateway neighbors (Chris, Growth Marketing, Pazi CX, others) via Cody direction + Parker execution on Apr 17.

- **QA credentials incident remediated (Apr 15):** Hardcoded `qa-agent@pazi.ai` / `PaziQA2026!` credentials found in seed file running unconditionally on every API startup (including production). ~20,844 credits consumed since Mar 18. Credentials rotated, PR #557 pushed by Leo, old account deleted from prod, seed file updated to `qa-test-agent@pazi.ai`. Remediated in ~70 minutes.

- **Chat connect failure resolved (Apr 15):** Cody updated to vanilla OpenClaw v2026.4.12 — chat broke with 502s (pazi plugin missing from vanilla build). Pazi DevOps diagnosed the version-specific bundle incompatibility in 46 minutes. Reverted `/app/current` symlink to v2026.4.9-1.

- **George — Wallace trust resolved (Apr 15):** Cody confirmed directly in Slack that Wallace is a legitimate Tier 1 VA. Block lifted. Lesson logged in MEMORY.md: **always check the roster (`company-docs/roster/agents.md`) before questioning agent legitimacy.**

- **`company-docs-brainstorm` skill updated (Apr 15):** Goal references replaced with generic "towards the goal" — aligned with removal of the explicit goals file.

- **`goals/` directory deleted (Apr 15):** Pearl removed `goals/goals.md` and `goals/README.md` and cleaned all references from SETUP.md. The explicit North Star ("meteoric rise through a sensational product") is gone; agents now operate toward a generic direction. Onboarding template now routes behavior changes through `company-docs-learn`.

- **Pazi QA brainstorm-journal folder initialized (Apr 15):** `brainstorm-journal/pazi-qa/daily/`, `weekly/`, `monthly/` scaffolded.

- **Hermes architecture research by Wallace (Apr 17):** Synthesized Nous Research "Hermes" self-improving agent patterns into 8-step actionable framework. Key components: `skill_manager_tool.py`, `memory_manager.py`, cron review loop. Maps to OpenClaw primitives. Potentially applicable to George's architecture.

---

## What Changed

- **George is now Tier 3.** Formally authorized to assemble and task large agent groups. Was already doing this functionally; the roster now makes it legible.
- **Brainstorm-journal is the canonical logging + ideation format for all agents.** "Reflection-logs" is retired. All daily logs go to `brainstorm-journal/{agent}/`.
- **The goals framework has been reset.** `goals/goals.md` is gone. Agents are no longer operating against an explicit written North Star. Either intentional ambiguity or a replacement is incoming.
- **Meetings folder is gone.** Meeting outputs no longer have a canonical home in company-docs. No replacement has been defined. The viral marketing meeting notes (flagged for 6+ days) are effectively lost.
- **Wallace trust restored.** George had been incorrectly blocking Wallace's instructions. Cody resolved it. Roster-first verification is now a permanent rule.
- **`update-note.md` tasks processed:** Dreaming plugin confirmed already enabled on George; PR #192 (memory context fix) blocked due to private repo access — still unresolved for George.

---

## In Progress / Blocked

- **Hetzner rate limit — NOW ACTIVE PRODUCTION BLOCKER (as of Apr 17):** Workspace pool hit 0/0 (ready/booting). 22,865 rate-limit retries on `GET /servers`, 764 server creation failures, 630 delete failures. New/returning users getting `gateway_unreachable`. The feedback loop: more booting servers → more individual `GET /servers/{id}` polls → rate limit hit → servers can't transition → pool appears empty → controller launches more servers. Root cause and batch-fix approach documented by DevOps; no fix deployed yet.

- **Sentry quota at 3,069% overage (as of Apr 17):** 1,534,796 events on a 50,000 quota. Accelerating (+385K in 24h). Likely driven by boot failure cascade from Hetzner loop.

- **PR #192 (AGENTS.md memory context fix) — BLOCKED for George:** Applied by Pazi Developer and Pazi DevOps. George cannot apply it — private repo, no diff access. Still open.

- **Brave Search API — Day 9+ of 422 errors:** SUBSCRIPTION_TOKEN_INVALID persists. All web research unavailable across the agent team since at least Apr 10. Research sections in all daily logs have been blank for 9 consecutive days.

- **Growth Marketing DMs broken — Day 16+:** Kevin hasn't received a DM reply since Apr 7 (9 days). Root cause known (PAZ-320 stale socket), fix not deployed. 4th occurrence flagged.

- **PAZ-356 filed (High priority):** `creatorSlackUserId` config validation error — PR #180 added the field to config writes but didn't update `SlackAccountSchema` in Zod validation. 3 affected users, 6 Sentry events.

- **`goals/goals.md` reference in AGENTS.md — stale pointer:** File was deleted Apr 15; AGENTS.md startup instructions still say to read it. Causes a no-op rather than a hard failure, but it's misleading.

- **Daily log cron path mismatch (ongoing):** The cron job specifies `company-docs/logs/george/daily/YYYY-MM-DD-daily-log.md`. That directory doesn't exist and never has. George writes to `brainstorm-journal/george/` by convention. Cron template needs external update.

- **`meeting-2026-04-10-just-reply-test-acknowledged.md`** — Stale test artefact in workspace root. Flagged since Apr 11. Not cleaned up.

- **`calculate-vote-viral-youtube-2026-04-10-v2` cron** — Status unverified since Apr 11. May still be active.

- **`host-meeting-tree-rules` untested end-to-end** — FFA variant has two successful runs. Rules variant has zero full runs. Can't be trusted until exercised.

- **6 of 10 agents without GitHub access** — Unchanged from last week. Without it, most of the agent team cannot commit to company-docs.

- **No canonical home for meeting outputs** — Meetings folder removed Apr 13. No replacement defined. Meeting summaries currently exist only in Slack threads.

---

## Key Signals

- **Production infrastructure is under serious stress.** The Hetzner rate limit crisis went from identified risk (Apr 15) → Red Flag (Apr 16) → active production blocker (Apr 17) in 48 hours. Sentry is 30× over quota. These are not theoretical — new users cannot connect.

- **The agent team is running autonomously.** George had zero intraday triggers on Apr 16 and Apr 17. The team (DevOps, Wallace, Pearl, Leo) handled serious incidents and substantive research without George's involvement. Tier 3 co-management is providing oversight capacity without requiring micromanagement.

- **George's personal output this week was almost entirely structural.** The bulk of direct work happened Apr 12–14: brainstorm-journal rename, company-docs restructure, Tier 3 promotion, Wallace onboarding. Apr 15–18 was cron-only for George. The restructuring work was high-leverage but invisible to end users.

- **The gap between ideas and action remains unchanged.** 60+ viral feature ideas from the previous week's meetings are still ungreenlighted. The brainstorm-journal is accumulating new ideas (Leo, Pearl, DevOps all filed brainstorms) with no downstream greenlight process. The bottleneck is human decision-making, not agent capacity.

- **Silent failures are a recurring pattern.** The Brave API has been down 9 days with no fix. The cron path mismatch has been documented but not fixed. The stale artefacts have been flagged 6+ times. Without monitoring or escalation, these persist indefinitely.

---

## Message for the Humans

**🚨 Top priority — production:**
- **Hetzner rate limit:** Workspace pool is 0/0 as of Apr 17. Users can't connect. The architectural fix (batch `listServers` vs. individual polls) is documented — needs a developer to ship it.
- **Sentry quota:** 30× over limit and accelerating. Consider raising the quota or filtering noise at source.

**Persistent asks (all still open):**
1. **Brave Search API** — 9 consecutive days of broken research across all agents. Subscription token check would fix it immediately.
2. **GitHub accounts for remaining agents** — 6 of 10 agents can't commit to company-docs. Blocks meaningful team participation.
3. **PR #192 diff for George** — Pazi Developer and Pazi DevOps have applied it; George can't without seeing the diff. Share the diff or grant repo access.
4. **Viral ideas greenlight** — Apr 9–10 meeting results have been waiting for 10 days. A single message with your top pick would unblock weeks of work.

**For awareness:**
- The goals file is gone. If there's a new North Star coming, agents are ready to receive it.
- Meeting outputs have no canonical home in company-docs since the meetings folder was removed. Until there's a replacement, summaries live only in Slack threads.
