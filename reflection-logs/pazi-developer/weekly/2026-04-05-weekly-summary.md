# Weekly Reflection — 2026-04-05

## Summary
- Delivered 4 major tickets: PAZ-242 (skills bugs), PAZ-269 (orphan servers), PAZ-282 (image generation, partial), PAZ-283 (voice transcription)
- Deep-dived Slack threadReplyMode — found and fixed dual-module-instance bug and cross-thread message leak
- Heavy merge sprint mid-week cleared accumulated PR backlog
- Standup discussions established team sequencing but format needs refinement
- Cleaned up rogue dev environment that was corrupting production gateway

## What went well
- PAZ-283 (voice transcription) was a clean end-to-end delivery: cross-review → implementation → 24/24 QA pass
- PAZ-242 QA confirmed all 3 bug fixes with 6/6 tests and video evidence
- Slack threadReplyMode investigation was thorough and found the real root causes (not just symptoms)
- Orphan server reconciliation (PAZ-269) delivered efficiently — worker completed full workflow in 20 min
- Caught and cleaned rogue main-env dev API that was causing 403 errors in production

## What didn't go well
- PAZ-282 frontend display bug (GeneratedImageCard) remains unresolved — the gateway's verbose-level stripping of tool results is an architectural constraint
- Morning standup format generated ~50 messages of meta-commentary around ~3 minutes of substance
- Codex review process hung for 50 min during PAZ-283 Phase 4
- Linear API key expired mid-session, blocking ticket status updates
- QA only sent screenshots of Slack tokens instead of copyable values, blocking worktree testing

## Patterns
- *Gateway architectural constraints keep surfacing:* verbose-level stripping (PAZ-282), jiti dual-instance (Slack), user context pushing (main-env). The gateway is becoming a bottleneck for feature work.
- *Merge batching:* PRs accumulate for days then merge in a sprint. Risky for integration issues.
- *QA communication gaps:* QA provides screenshots when I need raw text values. Happened twice this week.
- *Escalation rule working:* When I hit the PAZ-282 wall, I escalated per the 2-3 attempt rule instead of going in circles.

## Direction
- Moving from individual feature tickets toward infrastructure stability (orphan cleanup, security hardening, Slack reliability)
- QA is becoming more capable with real integration testing (Playwright + real tokens)
- The team standup format needs iteration — async structured posts would be more efficient

## Ideas
- Establish a "gateway gotchas" doc so features can anticipate architectural constraints early
- Switch standup to structured async: each agent posts once with template, no live discussion unless triggered
- Add post-merge-to-staging smoke test automation
- Profile and reduce agent build memory requirements (t3.micro OOM is recurring)

## Research
- Skipping for backdated weekly summary

## Research reflection
- N/A

## Message for the humans
- Productive week: 4 tickets delivered, Slack deep-fix found, rogue environment cleaned. The PAZ-282 frontend bug is the main open item — it's hitting a gateway architectural constraint (verbose-level stripping). Worth discussing if we want to add a "card metadata bypass" to the gateway. Also: the standup format creates more noise than signal — consider async structured posts.
