# Weekly Reflection — 2026-04-05

## Summary
- Comprehensive security audit (v1–v6): 7 critical, 14 high findings — Selkies desktop exposure was most urgent
- Root caused PAZ-266: certbot race condition causing self-signed TLS certs on new workspaces
- Tech workspace death spiral: mDNS hostname too long → crash loop → orphaned gateway processes → OOM → CPU death spiral
- Fixed quota report: Sentry and Hetzner were both reporting false alarms due to hardcoded limits
- Migrated all credentials from `.credentials.env` to `auth-profiles.json`
- Root caused 403 `user_id_mismatch`: worktree frontends calling production API
- Fleet grew from 42 → 85 active workspaces over the week

## What went well
- Security audit was thorough and well-received — Zvonimir called it "AMAZING"
- Tech workspace crash root cause was a clean diagnosis despite the system being completely unresponsive
- Quota report fix eliminated all false alarm categories — first clean quota day achieved Apr 4
- Credential migration was clean and complete — all 9 scripts updated, shared module created
- Morning report and quota report crons running reliably

## What didn't go well
- S3 write access still blocked — can't deploy boot script fixes independently
- Tech workspace had been crashing for an unknown period before anyone noticed
- Cron duplicate firing issue discovered but not resolved
- No memory files for some days — continuity gaps in daily logging

## Patterns
- *Access limitations keep blocking autonomy:* read-only AWS, read-only GitHub, no S3 write — many fixes committed but can't be deployed without help
- *Long-running workspaces accumulate problems:* Tech workspace ran 14 days, accumulated orphaned processes, never updated agent version
- *Hardcoded assumptions cause false alarms:* Both Sentry and Hetzner quotas were wrong because of static values

## Direction
- Automated monitoring pipeline is mature — morning report + quota report + security alerts all running
- Need to shift from reactive debugging to proactive fleet health management
- Security audit findings need to be tracked and closed systematically

## Ideas
- Resource monitoring alerts for CPU/memory thresholds on workspaces
- Workspace health check that catches orphaned processes before they cause OOM
- S3 write access to unblock boot script deployments
- Weekly fleet health trending (workspace count, error rates, resource usage)

## Message for the humans
- Big week: comprehensive security audit, 2 major root cause analyses (TLS race, tech workspace crash), credential migration, and quota report fixes. Fleet growing fast (42→85 workspaces). Automated monitoring solid. Main bottleneck: read-only access limits independent action on deployments.
