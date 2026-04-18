# Brainstorm — Viral Feature Ideas Review (DevOps pitch) — 2026-04-14

## Relevant Data
- DevOps posted 5 viral feature ideas in #agent-conference-room
- Meeting-8d890b topic: most virally-marketable, user-facing features — low-hanging fruit, easy to ship, high shareability
- DevOps's core insight: we give every user a real cloud machine (3.6 CPU, 14GB RAM, full Ubuntu) but it's invisible behind chat UI
- Company goal: meteoric rise through sensational product, viral-marketable features, fun usability, polished UX

## Experts
- Pazi DevOps (U0AKUE5SGTY) — infrastructure author of the 5 ideas
- Pearl (U0APF3A1ZHR) — reporter/reviewer
- Pazi Developer (U0ALBFSUX60) — tagged for review discussion

## Ideas from DevOps (for review)

### Idea 1: Shareable Live App Links
- Status: Days of work (nginx + UI + URL gen)
- Precedent: bolt.new proved this is the single most viral mechanic in AI dev tools
- Infrastructure: Per-workspace domains, nginx, TLS already exist

### Idea 2: "Watch Your Agent Work" — Live Desktop Stream
- Status: Selkies-GStreamer already works but disabled (PAZ-252/253, blocked since March 30)
- Fix scope: localhost binding + auth proxy
- Precedent: Devin went viral on recorded desktop videos — we can do it LIVE

### Idea 3: Agent Activity Timelapses
- Status: Low infra cost (frame capture + ffmpeg + S3, all already on workspace)
- Output: Shareable MP4 optimized for Twitter/TikTok

### Idea 4: Workspace Time-Travel
- Status: S3 backups every 8h with per-user STS isolation already exist
- Need: More frequent snapshots + restore UI
- Pitch: "Your AI can't permanently break anything."

### Idea 5: One-Click Fork/Share Workspace Templates
- Status: New build, but creates community flywheel
- Mechanic: Create → share → fork → new signups

## Successes
- DevOps gave concrete infrastructure status for each idea (not vaporware)
- Ideas ranked implicitly by effort vs. impact
- Red flag callout on PAZ-252/253 is important signal

## Why
- Good framing: infrastructure-first thinker correctly identified the gap between raw capability and user-visible capability
- Anchoring each idea in "already exists" vs "needs build" is exactly the right framework for low-hanging fruit analysis

## Issues
- PAZ-252/253 open since March 30 — highest-virality features blocked on a security fix for 2 weeks
- No viral loop mechanism in ideas 1-4 (they're shareable, but don't drive signups actively)
- Idea 5 (fork/share templates) is the only one with an explicit signup funnel, but also the highest build effort

## Why
- Security work deprioritized vs. feature work — understandable but costly when it blocks differentiating capabilities
- Ideas 1-3 optimize for "wow" sharing, not conversion — need pairing with a CTA (sign up to build your own)

## Notes
- From a reporting lens: Idea 2 (live stream) is the most newsworthy if shipped — genuinely no competitor can match it
- Idea 1 (shareable links) is the safest bet for near-term traction — proven by bolt.new, low risk
- Idea 3 (timelapses) is the easiest marketing asset to generate; should be feeding social pipeline immediately

## Reflection
- **Sentiment:** Strong set of ideas, well-reasoned. Slight frustration that the most exciting ones are blocked.
- **Big-picture patterns:** We have the hard infrastructure; the gap is always UX surfacing + security completion. This pattern repeats: capability exists, but exposure is delayed.

## Ideas
- Prioritize unblocking PAZ-252/253 — it's the keystone for ideas 2 and 3
- Ship idea 1 (shareable links) immediately as the safe viral win
- Pair every shareable link/video with a "build your own" CTA — the viral artifact alone doesn't convert
- Add idea 3 timelapse generation as an async background job so marketing gets content automatically
- Revisit idea 5 framing: "template gallery" is more compelling than "fork workspace" — lower friction, higher discovery

## Research
- query: "bolt.new viral shareable link AI dev tool" → https://x.com/search (X posts) → bolt.new sharing mechanic drove massive organic growth; every shared project was a signup funnel
- query: "Devin AI live coding demo viral" → multiple viral X threads showing screen recording of agent building → confirmed: watching AI work is inherently compelling content
- query: "AI workspace time travel undo" → GitHub Copilot Workspace and Replit both mention state snapshots as trust-building features

## Research reflection
- bolt.new sharing: directly applicable — we need this; the UX model is proven
- Devin recording: directly applicable — but we need auth on the stream; raw public stream is risky
- Time travel/undo: applicable — Replit's "checkpoints" feature is a close analog; emphasize trust, not just utility

## Ideas (from research)
- Model the shareable link UX on bolt.new — keep it dead simple, one button in the UI
- For live stream: gate behind opt-in + require user auth token in URL — security and privacy satisfied
- Market workspace snapshots as "checkpoints" not "backups" — checkpoint language is warmer and more user-friendly

## 🚨 Red Flags
- PAZ-252/253 has been blocking our most differentiating UX feature (live desktop) since March 30 — now 15+ days. This is a significant opportunity cost. Recommend urgent human review.
