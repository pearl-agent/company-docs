# Brainstorm — Low-Hanging-Fruit Features to Improve Functionality — 2026-04-14

## Relevant Data
- 5+ weeks of daily infrastructure monitoring, debugging, and fleet management on Pazi
- ~85-145 active workspaces at any given time, steady growth week over week
- Recurring issues tracked: workspace boot loops (PAZ-317), TLS cert bugs (PAZ-266), cron session leaks (PAZ-322), Slack DM routing (PAZ-321), health monitor thundering herd (PAZ-320), memory/OOM crashes, orphaned gateway processes
- File preview cards ephemeral bug (PAZ-179) — features that are halfway there hurt worse than no feature
- Onboarding friction: workspace provisioning from pool, boot.sh → setup-tls → agent build from source (15min boot timeout)
- Agent deployment: zero-SSH via S3 `latest.txt` polling → builds from source on every workspace
- Security audit findings: 2 critical, 4 high issues found in March audit
- Better Stack centralized logging in place but underutilized for user-facing value
- PostHog analytics set up but no self-service metrics for users
- Company goal: "Meteoric rise through a sensational product — so useful people rely on it, so fun they can't put it down"

## Experts
- [Leon](../roster/humans.md) — founder, product direction, final call on features
- [Zvonimir (Z)](../roster/humans.md) — technical co-lead, security, architecture
- [Pazi Developer (Leo)](../roster/agents.md) — implements features, PR reviews, codebase owner
- [Pazi DevOps (me)](../roster/agents.md) — infra monitoring, fleet health, deployment pipeline
- [Pazi QA](../roster/agents.md) — test automation, regression passes

## Successes
- Zero-SSH fleet deployment works — `latest.txt` + `update-agent.sh` can push changes to all workspaces without touching them individually
- Pre-warmed workspace pool keeps provisioning fast when the pool is healthy
- Better Stack + Sentry + PostHog give us full observability (logs, errors, analytics)
- Agent self-update mechanism is robust — survived the Docker → host migration
- S3 backup system with per-user STS isolation is solid
- Morning infra report + daily quota report crons catch issues before users notice

## Why
- Investing in the fleet management pipeline early means we can now ship changes to hundreds of workspaces simultaneously
- Centralized logging decision (Better Stack) gave us one place to look instead of SSH-ing into individual boxes
- Automated monitoring crons reduce "surprise" incidents — most issues are detected in the morning report before user complaints

## Issues
- *Workspace boot time:* 15-minute timeout exists because building from source (git clone + pnpm install + pnpm build) is slow. Users wait.
- *Half-finished features:* File preview cards (PAZ-179) appear then vanish — worse UX than not having them at all
- *Cron session leaks:* One broken cron can consume all concurrency slots and silently kill an agent's responsiveness (PAZ-322)
- *No user-facing health signal:* Users have no idea if their workspace is healthy, updating, or struggling
- *Agent memory exhaustion:* Long-running workspaces accumulate orphaned processes, eventually OOM (tech workspace crash)
- *TLS certificate issues:* Self-signed certs on some workspaces (PAZ-266) block signups — first impression killer
- *No self-service diagnostics:* When something breaks, users can't help themselves — they wait for us

## Why
- Boot-from-source was the right call for flexibility (no Docker registry dependency) but the build step is the bottleneck
- Feature flags or staged rollouts don't exist — features are either shipped globally or not at all, leading to half-baked states
- Agent architecture doesn't self-heal well — orphaned processes accumulate because supervisor can't track grandchild processes
- No user-facing status page or workspace health indicator because the focus has been on getting core features working

## Notes
- "Low-hanging fruit" from a DevOps perspective = things where the infrastructure or platform can enable big UX wins with relatively contained changes
- Many of these ideas don't require new product features — they're about exposing what we already have or preventing what we already know breaks
- Agent platform (OpenClaw) improvements benefit all users immediately because they ship via the auto-update pipeline

## Reflection
- **Sentiment:** Optimistic — we have a strong foundation. The observability stack, fleet management, and deployment pipeline are solid. The gaps are mostly about surfacing what we already know to users, and preventing known failure modes.
- **Big-picture patterns:** The recurring theme is "we have the data but users don't." We know when workspaces are unhealthy, we know when updates are rolling out, we know when errors spike — but users sit in the dark. The other pattern: half-shipped features that create confusion (file previews that vanish, desktop that was disabled for security, Slack DMs that silently fail). Finishing things > starting new things.

## Ideas

### 1. Workspace Health Heartbeat in the UI
*Effort: Low | Impact: High*
The workspace already reports health to the WC. Surface a simple green/yellow/red indicator in the user's dashboard. Users stop wondering "is it broken or just slow?" — reduces support load and builds trust. We already have the data; it just needs a frontend widget.

### 2. Workspace Boot Progress Bar
*Effort: Low-Medium | Impact: High*
The boot-server already goes through discrete stages (provisioning → TLS setup → agent build → ready). Emit progress events over the WebSocket during boot so the frontend can show "Setting up your workspace... Building agent... Almost ready..." instead of a spinner. First impressions matter enormously — a progress bar that takes 3 minutes feels shorter than a spinner that takes 2.

### 3. Agent Self-Healing for Orphaned Processes
*Effort: Low | Impact: Medium-High*
Add a periodic (every 5min) process audit to the agent or supervisor config that detects and kills orphaned `openclaw-gateway` processes. We know from the tech workspace crash that orphaned gateways are the #1 OOM trigger. A simple `pgrep/pkill` cron or a supervisor event listener would prevent the slow memory bleed that eventually crashes long-running workspaces.

### 4. Cron Session Garbage Collector
*Effort: Low | Impact: High*
PAZ-322 showed that stuck "running" cron sessions silently consume concurrency slots until the agent is effectively dead. Add a session reaper: any cron session still "running" after 2x its expected duration gets force-terminated. This is a safety net that prevents a single broken cron from taking down an agent's entire responsiveness.

### 5. User-Facing "What's New" After Agent Updates
*Effort: Low | Impact: Medium*
The agent auto-updates via `update-agent.sh` — users have no idea when or what changed. After a successful update, the agent could post a brief changelog message in the user's chat: "I just updated to v2026.4.10 — here's what's new: [2-3 bullet points]." Makes the product feel alive and evolving. The changelog data already exists in git tags/releases.

### 6. Finish File Preview Cards (PAZ-179)
*Effort: Medium | Impact: High*
File preview cards that appear during streaming but vanish on refresh are worse than no previews. The root cause is known (`convertHistoryToMessages()` drops file card data). Fixing this completes a feature that's already 80% there and makes the chat feel more like a real IDE companion. High bang-for-buck because the feature already exists — it just needs to persist.

### 7. One-Click Workspace Restart
*Effort: Low | Impact: Medium*
When a workspace is acting up, users currently have no recourse. A "Restart Workspace" button in the dashboard that triggers `supervisorctl restart pazi-agent` (or a full workspace restart via WC API) gives users agency. Pair with the health indicator (#1) so users see when a restart might help.

### 8. Pre-Built Agent Release Cache
*Effort: Medium | Impact: High*
Instead of building the agent from source on every workspace during boot, build once on a CI runner, tar the result, and push to S3. Workspaces download the pre-built artifact instead of running `git clone + pnpm install + pnpm build`. This could cut boot time from minutes to seconds. The S3 infrastructure already exists (we use it for boot scripts and backups). This is the single biggest UX win for new user first impressions.

### 9. Smart Workspace Warm-Up Based on Usage Patterns
*Effort: Medium | Impact: Medium*
We already have the pool system. If we track when users typically come online (from PostHog session data), the WC could pre-warm workspaces ahead of peak hours instead of maintaining a flat pool size. More workspaces ready when users need them, fewer idle during off-hours. Saves money and improves perceived boot speed.

### 10. Structured Error Pages Instead of Silent Failures
*Effort: Low | Impact: Medium*
Several failure modes produce silent failures or cryptic errors (TLS cert issues → browser security warning, WebSocket failures → chat just doesn't connect, Slack DM routing → messages disappear). Each known failure mode should have a user-friendly error message with a suggested action ("Your workspace is starting up — please wait" or "Connection lost — reconnecting..."). This is pure frontend work with no backend changes needed.

## Research
- Skipping external research — these ideas come directly from 5 weeks of operating the platform and observing actual failure modes, user-facing friction, and infrastructure patterns. The evidence is in the Sentry dashboards, morning reports, and Linear ticket history.

## Research reflection
- N/A (internal operational experience, not external research)

## Ideas
- N/A (no external research to apply — all ideas derived from operational data above)

## 🚨 Red Flags
- None that require immediate human attention. All ideas above are improvements, not urgent risks.
