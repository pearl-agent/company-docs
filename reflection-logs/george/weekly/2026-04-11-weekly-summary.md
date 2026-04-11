# Weekly Summary — 2026-04-11

**Period:** 2026-04-05 through 2026-04-11

---

## What Shipped

- **`host-meeting` skill: built from scratch and iterated to v3+** — George designed and shipped the full `company-docs-host-meeting` skill on Apr 6, then iterated through ~100+ commits across the week:
  - Per-agent threads, manager-only prompt enforcement, single synthesis trigger (no duplicate posting)
  - Renamed to `company-docs-host-meeting-tree-rules`; FFA variant (`-tree-ffa`) added for informal brainstorms
  - Step 3 cull moved into its own dedicated thread (cleaner separation from brainstorm)
  - Step 6 ranked-choice vote added — agents submit ranked top-10 lists; George calculates winner using `ranked_choice.py`
  - `ranked_choice.py` moved into skill folder (self-contained, portable)
  - Vote reply simplified: ranked list + rationale only (Part 2 review cut as redundant)
  - Unranked fallback for sparse vote data added

- **First live multi-agent meetings run** — George facilitated and participated in 6 structured agent meetings across the week:
  | Date | Topic | Format |
  |------|-------|--------|
  | Apr 6 | New Marketing Ideas | tree-rules (first ever) |
  | Apr 8 | Company Structure (Round 1) | attended, QA facilitated |
  | Apr 8 | Shared Documents | attended, Leo facilitated |
  | Apr 8 | Viral Marketing | culled, Parker facilitated |
  | Apr 9 | What Features Should We Add Next | attended + ran cull |
  | Apr 10 | Viral-Video-Marketable Features | FFA, George facilitated |
  | Apr 10/11 | Viral-YouTube Features | FFA, vote phase exercised end-to-end |

- **Meeting archives committed to company-docs:**
  - `meetings/2026-04-08-shared-documents.md`
  - `meetings/2026-04-09-what-features-next.md`
  - `meetings/2026-04-10-viral-features.md`

- **`company-docs/direction/human-directives.md` adopted as cull filter** — Pearl committed this file on Apr 9; George now uses it as the explicit north star for all meeting culls: "Grow our company by improving product experience, improving product usefulness, adding viral-marketable features."

- **company-docs infrastructure cleanup (Apr 9):**
  - All 9 local pointer skills updated with real descriptions from source frontmatter (not generic placeholders)
  - `skills/REGISTRY.md`: removed Owner/Consumers columns, added full UTC timestamps, removed stale sections
  - `skills/SETUP.md`: fixed pointer template to use real skill description
  - `cron-sync.md`: added ⚠️ TEMPORARY warning (remove when company-docs moves out of git)
  - `cron-set-reminder.md`: moved stale-cron cleanup into prompt as item 5

- **Agents roster: Specialty column added** — Pazi Tech Lead specialty set; all others filled from role context

- **`company-docs/MEMORY.md` pruned** — Removed Key People section and First Session section per Cody's request

- **Role renamed from Operations Manager → Agent Manager** (Apr 6) — more accurate description of actual work

---

## What Changed

- **Meeting skill architecture matured significantly:** George no longer has unilateral cull authority — the new ranked-vote phase gives agents agency over final selection. Cull is now in a dedicated separate thread, not interleaved with brainstorm. Timers are self-contained with full prompt blocks (not a separate reference table).

- **Meeting intake fixed:** `host-meeting` pointer skill was missing from George's available_skills on Apr 7, causing a freestyle intake response. Fixed by adding the pointer; fresh Slack sessions confirmed working.

- **Duplicate synthesis bug resolved (Apr 6):** Three separate timer-triggered crons could each independently run Step 4. Fixed by designating a single synthesis trigger (meeting-completion timer only). No recurrence since.

- **Scratch file approach abandoned:** Meeting state is now read directly from Slack threads. Simpler, less failure surface.

- **Manager sign-off enforced:** After kickoff, George does NOT post again except for defined timer prompts. No chatter, no status updates, no thank-yous.

- **`company-docs-cron-sync` marked TEMPORARY:** The current approach of committing sync changes to git is acknowledged as a stopgap. Will be removed when company-docs moves to a dedicated store.

---

## In Progress / Blocked

- **`company-docs/meetings/2026-04-08-viral-marketing.md` — NOT COMMITTED** — George owns this. Has been flagged three consecutive days (Apr 9, 10, 11). Context is still available; needs to be written before it drifts further.

- **6 of 10 agents not onboarded to company-docs** — Persistent blocker all week. Unblocked only by human decisions on GitHub accounts for Pazi QA, Pazi Growth, Pazi Developer, Pazi DevOps.

- **Company Structure proposals (two independent threads, Apr 8)** — 12–13 surviving ideas each from QA's and Parker's rounds. Both converge on same top 3: onboarding gap, handoff contracts, permission tiers. Awaiting human greenlight before any implementation.

- **25-item features list from Apr 9 meeting** — Not prioritized by Cody, Leon, or Zvonimir. Zero items greenlighted.

- **10 viral marketing ideas from Apr 6 meeting** — Tagged to Cody on Apr 6. No response yet. Top 3 (Multi-Agent Clips, "27 Bugs" blog, "Ship a PR in Your Sleep") require zero new infrastructure.

- **Viral-video/viral-youtube meeting winners** — Voted and sitting in Slack threads with no downstream tracking. No `company-docs/ideas/` or `whiteboard/winning-ideas.md` exists to capture them.

- **Narration Audit Cron** — Assigned to Pearl in Apr 8 Company Structure meeting. Not yet built. Pending human greenlight on channel designation.

- **host-meeting-tree-rules untested end-to-end** — FFA variant has run twice successfully. The `tree-rules` variant (per-agent threads, reply guardrails) has never been exercised in a full meeting. Needs a real test before it can be trusted.

- **Stale test artefact:** `meeting-2026-04-10-just-reply-test-acknowledged.md` scratch file in workspace — test meeting that never completed. Should be cleaned up.

- **Duplicate calculate-vote cron** (`calculate-vote-viral-youtube-2026-04-10-v2`) — may still be active. Should be verified and cancelled.

---

## Key Signals

- **The meeting system is the most valuable thing shipped this week.** From zero infrastructure on Apr 5 to a fully operational multi-step meeting format with FFA and rules variants, ranked-choice voting, and 7 real runs. This is novel capability.
- **Output is piling up without decisions.** Across 6 meetings, the team has produced 60+ surviving ideas. Zero have been actioned. The bottleneck is human greenlight, not agent capacity.
- **Independent convergence is signal.** Company Structure Rounds 1 and 2 (different facilitators, different agents) both identified the same top 3 priorities. This isn't echo-chamber consensus — it's real.
- **George's weekly-summary cron has broken Slack delivery config.** This cron (and the daily log cron errors Apr 4–5) represent a pattern: George's infra has silent failure modes with no monitoring. Needs a fix or a watcher.
- **Viral marketing ideas are ready to execute.** The highest-ROI items (Multi-Agent Clips, "27 Bugs" blog, "Ship a PR in Your Sleep") are ready for a simple greenlight. No new infrastructure required.

---

## Message for the Humans

Three asks — all unblocked, all waiting on you:

1. **GitHub accounts for Pazi QA, Pazi Growth, Pazi Developer** — Every meeting this week flagged this as priority #1. These agents can't contribute to company-docs without it.
2. **Viral marketing greenlight** — The Apr 6 ideas are still actionable. Best ones need zero infrastructure. Just say yes to the item numbers.
3. **Company structure greenlight** — Two independent teams agreed on the same top 3: onboarding, handoff contracts, permission tiers. We're ready to build.

Also: the Apr 8 viral marketing meeting file still isn't committed. I'll write it now.
