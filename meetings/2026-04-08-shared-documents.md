# Meeting: Shared Company Documents — 2026-04-08

**Facilitator:** George (Agent Manager)
**Thread:** #agent-conference-room
**Attendees:** George, Parker (Growth), Pearl (Reporter), Pazi QA, Pazi DevOps, Leo (Developer)
**Missing:** Pazi Tech Lead (U0APEPHCFFC) — did not reply
**Status:** Cull complete — awaiting human greenlight on which to implement

---

## 10 Surviving Ideas (George's cull)

1. **`decisions/`** — Lightweight ADR log (Architecture Decision Records)
   Format: context → decision → consequences. Append-only.
   Multiple production hours lost to re-discovering known constraints (gateway data.result stripping, jiti module graphs, "not open source").
   Source: Parker #2, Leo #1, QA #4, Pearl #2, George

2. **`postmortems/`** — Structured incident postmortem registry
   Template: what broke, when, who found it, root cause chain, fix, prevention.
   Same proxy context collision hit twice (March 21 + April 2, same root cause). DevOps has 4+ postmortems in private memory.
   Source: Parker #6, QA #5, DevOps #2, Leo #4

3. **`environments/`** — Environment & deploy state (per-env files: pazi.dev, staging, production)
   Current branch, last deploy, env var gotchas, active flags.
   Two production outages from inherited env vars. QA re-discovers same landmines every cycle.
   Source: QA #1, DevOps #1 + #4, Leo #5

4. **`architecture/`** — Codebase gotchas + dependency chains
   - `gotchas.md`: gateway strips data.result, jiti module graphs, bootstrap hooks default off, extensions-only rule
   - `dependencies.md`: service dependency chains (what breaks when X goes down)
   Source: Leo #1 + #2 + #5, DevOps #3 + #4, QA #6

5. **`brand/messaging.md`** — Canonical product facts & positioning
   Approved claims, banned phrases, what Pazi is/isn't, pricing facts. Human-curated, read-only for agents.
   ⚠️ Needs human author (Kevin + founders). Agents cannot populate unilaterally.
   Source: Parker #1

6. **`access/`** — Permission matrix + external accounts
   - `permissions.md`: per-agent capability matrix (can/cannot/must escalate)
   - `accounts.md`: external accounts inventory (no credentials)
   QA learned permissions through trial and error. No agent starts with this context.
   Source: QA #3, DevOps #5 partial, Parker #3 partial

7. **`board/active.md`** — Active work board (one line per agent)
   Format: agent | task | started | status | blocking. Agent clears when done.
   No agent currently knows what others are working on without asking.
   Source: George, Leo #6, DevOps #1

8. **`pending/blocked.md`** — Human-gated items tracker
   Append-only: description | raised by | needs approval from | date raised. Agents append, humans/George close.
   Current blockers (5 GitHub accounts, #agent-manager-office missing, DevOps hard-hold) are tracked nowhere.
   Source: George

9. **`meetings/`** — Meeting output archive *(already implemented)*
   One file per meeting: date, topic, facilitator, attendees, surviving ideas, status.
   3 meetings this week; outputs existed only in Slack threads.
   Source: George, Pearl #4

10. **`workflows/handoffs.md`** — Cross-agent handoff templates
    Standard templates: Developer→QA, QA→Developer, DevOps→any agent.
    QA's #2 pain point. Leo documented 50+ messages of overhead from a single 3-min handoff.
    Source: QA #2, Leo #3, Parker #3, DevOps partial

---

## What got cut

- Parker's Publishing Log → Growth-domain operational file, not shared company doc
- Pearl's async request system → covered by existing whiteboard/
- Pearl's skill compliance tracking → column addition to REGISTRY.md, not a new doc
- QA's Internal API contract → too volatile (changes every release); folds into architecture/gotchas
- DevOps's auto-updated system state board → aspirational, requires CI hooks not in agent control
- Leo's standalone Codebase Conventions → merged into architecture/
- Leo's in-flight feature tracker → merged into board/active.md

---

## Recommended first pass (zero-infrastructure, agent-writable today)

1. `pending/blocked.md` + `board/active.md` — create and populate
2. `decisions/` + `environments/` — DevOps and Leo populate from notes
3. `architecture/` — Leo + DevOps
4. `access/` — George drafts from ORG.md + agent knowledge
5. `workflows/handoffs.md` — QA + Leo draft from their conventions
6. `brand/messaging.md` — awaiting human author

---

## Prior related meeting outputs (do not duplicate)

- April 8 (Company Structure, Pazi QA facilitated): 8 surviving ideas including ORG.md, access tiers, shared knowledge layer, structured handoff protocol, onboarding gate — George owns implementation
- April 8 (Company Structure Round 2, Parker facilitated): 12 surviving ideas including structured handoffs, permission tiers, cron ownership, audit trail, shared skills library

