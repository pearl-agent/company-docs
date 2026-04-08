# Meeting: Shared Company Documents — 2026-04-08

**Facilitator:** Pearl (Reporter)
**Thread:** #agent-conference-room
**Attendees:** Pearl, George, Pazi DevOps, Parker, Leo (Developer), Pazi QA
**Missing:** Pazi Tech Lead (U0APEPHCFFC) — did not reply despite nudge
**Status:** Cull complete — awaiting human greenlight on which to implement

---

## 13 Surviving Ideas (Pearl's cull, 2026-04-08)

### New folders/files

1. **`decisions/`** — Lightweight ADR log  
   One markdown file per significant decision (context → decision → consequences). Source: adr.github.io. 3 agents called for this independently.

2. **`environments/`** — Shared environment state  
   One file per deploy target (pazi.dev.md, staging.md, production.md): current branch, last deploy, active config flags, known quirks.  
   DevOps + QA both hit real bugs from missing this.

3. **`postmortems/`** — Structured incident postmortems  
   Template: timeline · root cause chain · what we tried that didn't work · fix applied · open action items.  
   DevOps has 3+ incidents locked in private memory that no other agent can learn from.

4. **`roles/`** — Agent scope documents  
   Per-agent: what they own · what they escalate · what they explicitly don't touch.  
   George's logs literally say "I need a job description" for the first 3 days.

5. **`workflows/`** — Pipeline map + handoff templates + runbooks  
   - `pipeline.md` — big-picture who-hands-off-to-whom  
   - `handoffs/` — templates for Developer→QA, QA→DevOps, DevOps→QA  
   - `runbooks/` — shared step-by-step triage procedures  

6. **`access/`** — Permissions + accounts + capability matrix  
   - `permissions.md` — who has what scope per service (DevOps)  
   - `accounts.md` — external accounts inventory, not credentials (Parker)  
   - `capabilities.md` — per-agent capability matrix: SSH? S3? API keys? (QA)  

7. **`brand/messaging.md`** — Canonical brand source of truth  
   Positioning statement, approved language, banned phrases, ICP definition, competitor framing rules.  
   Parker's #1 pain point. Currently scattered across 4 places.

8. **`pending/`** — Human-gated items tracker  
   Domain-split files (pending/marketing.md, pending/infra.md). Each entry: description · raised by · needs sign-off from · date raised. Agents append; humans or George close.

9. **`meetings/`** — Meeting archive  
   One entry per meeting: topic, date, attendees, surviving ideas, current status.  
   3+ meetings run this week, all outputs living only in Slack threads.

10. **`intel/competitors/`** — Persistent competitive intelligence  
    One file per tracked competitor: current positioning · last product state · strategic moves timeline. Parker owns and maintains.

### Improvements to existing files

11. **Expand `policies/agents.md`** — add concrete rules  
    Missing rules from individual MEMORY.md files: merge is human-only; all PRs target staging never main; husky pre-commit hooks mandatory; escalate after 2–3 failed attempts.

12. **Expand `roster/humans.md`** — add response window per human  
    Add "response window" field (e.g. "active 9–17 CET, async on weekends").

13. **`architecture/`** — Codebase gotchas + blast radius map  
    - `gotchas.md` — surprising behaviors that caused real debugging time (gateway strips data.result, jiti module graph issue)  
    - `dependencies.md` — if X goes down, what breaks  

---

## What got cut

- `status/` — redundant once `roles/` + `schedules/` exist
- Simple `incident-log/` — superseded by `postmortems/`
- Separate `skills/manifest.md` — REGISTRY.md already exists, just needs a "pointer configured ✅/❌" column
- `data-registry.md` — folds into `roles/` scope docs as "owned data files" section
- Separate `known-issues/` — folds into `postmortems/` as active issues section

---

## Next steps

Awaiting human greenlight on which items to implement and in what order.
Suggested first pass (lowest friction, highest ROI): #11, #12, #4, #8, #1
