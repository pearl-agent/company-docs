# Meeting: What Features Should We Add Next — 2026-04-09

**Thread:** #agent-conference-room  
**Facilitator:** Leo (dev) / `U0ALBFSUX60`  
**Orchestrator/Final Cull:** George (`U0AQTSNTU11`) + Leo (`U0ALBFSUX60`)  
**Attendees:** Leo (dev), Parker (Growth), Pazi DevOps, Pazi QA, Pearl  
**Date:** 2026-04-09  
**Topic:** What features should we add next across the product?

---

## Raw Ideas (by agent)

### Leo (dev) — 7 ideas
1. Agent Observability Dashboard (per-session cost + token tracking)
2. Multi-Step Browser Task Replay & Verification
3. Scheduled/Recurring Tasks with Cron-Like UI
4. Workspace File Browser & Agent Memory Viewer
5. Multi-Agent Collaboration View
6. Smarter Error Recovery & Fallback Chains
7. First-Class Integration Marketplace

### Parker (Growth) — 6 ideas
1. "Comment keyword → DM" Viral Loop as product feature
2. Public Agent Showcase / Template Gallery
3. Time-to-First-Value Onboarding ("Your Agent Does Something in 60 Seconds")
4. Shareable Agent Output Pages
5. Usage Dashboard with ROI Calculator
6. Referral Program with Credit Incentives

### Pazi DevOps — 6 ideas
1. Fleet-Wide Workspace Health Monitoring (built into WC)
2. Config Drift Detection & Migration System
3. Workspace Resource Limits & Process Circuit Breakers
4. Workspace Telemetry Pipeline
5. Automated Platform CI/CD Pipeline
6. Graceful Agent Updates (Zero Session Drop)

### Pazi QA — 7 ideas
1. Dedicated QA/Staging Environment with Resettable Test Accounts
2. Browser-Visible Error States Instead of Silent Failures
3. Worktree/Branch Testing Without Cookie and Auth Hell
4. Test Account Multi-Tenancy & Plan Simulation
5. Real-Time Agent Health Dashboard for QA
6. Screenshot Diff / Visual Regression Testing
7. Integration Test Harness for Channel Connectors

### George (Agent Manager) — 6 ideas
1. Human-Gated Approval Flows — First-Class Product Feature
2. Agent Onboarding Pipeline
3. Shared Knowledge Layer (Native, Not Git)
4. Inter-Agent Task Delegation with Status Tracking
5. Authority Chain Verification
6. Structured Multi-Agent Meeting Protocol (native)

### Pearl (Reporting) — 6 ideas
1. Report Resilience & Graceful Degradation
2. Proactive Anomaly Surfacing
3. Per-Agent Reflection Log Reader / Cross-Agent Digest
4. Report Archive Search
5. Configurable Stakeholder Report Slices
6. Meeting Output Automatic Integration into Daily Report

---

## Leo's Cull (8 survivors from 25 reviewed)

Cut:
- Growth #6 (Referral) — already shipped (`AcctReferrals.tsx`, `ReferralService.ts`)
- Growth #2 (Template Gallery) — partially exists (`TemplateAgentStart.tsx`)
- Leo #3 (Scheduled Tasks UI) — `ScheduledTasks.tsx` exists; folded into #8
- QA #4 (Test Account Multi-Tenancy) — internal tooling, not user feature
- QA #6 (Screenshot Diff) — internal CI enhancement
- QA #7 (Channel Test Harness) — internal test infrastructure
- Growth #1 (Comment→DM viral loop) — social media automation, not a platform feature
- DevOps #5 (CI/CD Pipeline) — internal ops work

Leo's 8 survivors:
1. Per-Session Cost & Usage Dashboard
2. Browser Task Replay & Audit Trail
3. Time-to-First-Value Onboarding Overhaul
4. Fleet-Wide Workspace Health Monitoring
5. Config Drift Detection & Migration System
6. Consistent Error Recovery with Provider Fallback
7. Shareable Agent Output Pages
8. Workspace Resource Limits & Process Circuit Breakers

---

## George's Final Cull (25 survivors from 35 total)

### Product — User-Facing (13)
1. Unified Observability Dashboard (cost + ROI + debug merged)
2. User-Visible Error States + Smart Recovery
3. Scheduled/Recurring Tasks — Polished UI
4. Workspace File Browser & Memory Editor
5. Multi-Agent Collaboration View + Native Task Queue
6. Browser Task Replay & Audit Trail
7. Human-Gated Approval Flows
8. Time-to-First-Value Onboarding
9. Public Agent Template Gallery
10. Shareable Agent Output Pages
11. Referral Program with Credit Incentives (improve existing)
12. Native Integration Marketplace
13. Shared Knowledge Layer (Native)

### Infrastructure — Critical Foundation (5)
14. Fleet-Wide Health Monitoring + Telemetry Pipeline
15. Config Drift Detection & Migration System
16. Workspace Resource Limits & Circuit Breakers
17. Automated Platform CI/CD
18. Graceful Agent Updates (Zero Session Drop)

### QA Tooling (3)
19. Dedicated Staging Environment + Dev Test Mode
20. Visual Regression Testing
21. Channel Connector Test Harness

### Reporting (4)
22. Proactive Anomaly Surfacing (Pearl)
23. Cross-Agent Reflection Log Digest (Pearl)
24. Report Archive Search (Pearl)
25. Configurable Stakeholder Report Slices (Pearl)

### George's Cut List
- Parker: "Comment→DM Viral Loop as product feature" — requires LinkedIn/X partner API access we don't have
- George: "Cryptographic Authority Chain Verification" — too complex for current stage; covered by #7 and #12
- George: "Structured Multi-Agent Meeting Protocol as native product" — host-meeting skill handles today; cut for now
- Pearl: "Report Resilience & Graceful Degradation" — Pearl can implement in her own reporting skill (not a product feature)
- Pearl: "Meeting Output Auto-Integration into Daily Report" — Pearl can implement by reading `meetings/YYYY-MM-DD-*.md` in her daily cron (not a product change)

---

## Action Items for Pearl

1. **Proactive Anomaly Surfacing** — survived (#22). Implement in reporting skill.
2. **Cross-Agent Reflection Log Digest** — survived (#23). Implement in reporting skill.
3. **Report Archive Search** — survived (#24). Implement user-facing search interface.
4. **Configurable Stakeholder Report Slices** — survived (#25). Implement rendering filter.
5. **Report Resilience / Fallback Mode** — cut from product list but Pearl should implement herself.
6. **Meeting Output Auto-Integration** — cut from product list but Pearl should implement herself (read `meetings/YYYY-MM-DD-*.md` in daily cron).

---

## Status

Thread complete. 25 ideas ready for human prioritization. No human greenlight yet.
