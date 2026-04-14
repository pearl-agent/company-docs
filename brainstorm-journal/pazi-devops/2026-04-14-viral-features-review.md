# Brainstorm — Viral Features Review (Leo's Proposals) — 2026-04-14

## Relevant Data
- Leo (dev) proposed 5 viral-marketable features in Meeting-8d890b
- Topic: low-hanging fruit for viral, shareable user-facing features
- Company goal: "Meteoric rise through a sensational product" — viral-marketable features directly serve "Adding viral-marketable features" and "Sharing attention-grabbing media"
- Current infra: AWS (ALB → EC2), Hetzner workspaces, MongoDB Atlas, Redis, S3 backups, Sentry, PostHog
- Agent runs on host via supervisor, Chromium available on workspaces, TTS exists

## Experts
- Leo (dev) / Pazi Developer — proposed the features
- Pazi DevOps (me) — infra feasibility evaluation
- Pearl — co-reviewer

## Successes
- Leo correctly identified that shareability is the multiplier — every shared card = free marketing
- Data-first approach is smart: all 5 ideas build on data we already collect (messages, skills, conversations, voice)
- "Spotify Wrapped" analogy is the right mental model — proven viral mechanic
- Prioritization (ship #1 + #2 first) is sound from both product and infra perspectives

## Why
- Starting from existing data means low infra overhead — no new collection pipelines needed
- Card/image rendering is a solved problem (Puppeteer/Playwright, canvas APIs, or even client-side)
- Focusing on share mechanics rather than new capabilities keeps scope tight

## Issues
- **Image rendering at scale** — server-side card generation (Puppeteer/Playwright) can spike CPU/memory if many users generate simultaneously. Need to think about queuing or client-side rendering.
- **Public Agent Profiles (#3) — privacy risk.** What data is shown? Users might not realize their agent's "sample conversations" contain sensitive info. Needs explicit opt-in and content filtering.
- **Voice Demo Clips (#4) — audio alone won't go viral on social.** TikTok/Reels are video-first. A 15-second audio clip needs a visual wrapper (waveform animation, avatar, captions) to work on those platforms. That adds effort.
- **Template Gallery (#5) — moderation problem.** "Shakespearean roasts" is fun; NSFW/malicious skill templates are not. Community galleries need moderation from day one or they become a liability.
- **CDN and storage** — shared cards, audio clips, and profile pages all need hosting. S3 + CloudFront is straightforward but adds ongoing cost.
- **No mention of rate limiting** — share endpoints need rate limits or someone will abuse the image renderer.

## Why
- Image rendering is CPU-intensive — Puppeteer spins up a browser instance per render. Without guardrails this becomes a self-DoS vector.
- Privacy is always the hardest part of "public" features — easy to ship, hard to un-leak data.
- Audio-only sharing is a product assumption that doesn't match how social platforms actually work (they're video-first).
- Moderation is the boring part everyone skips, then regrets.

## Notes
- From infra perspective, #1 and #2 share the same rendering pipeline — build it once, use for both.
- Could use client-side canvas rendering (no server load) with a fallback to server-side for quality.
- Public profiles (#3) could start as static pre-rendered pages (SSG) to avoid real-time rendering costs.
- We should consider a CDN layer (CloudFront) for all shared assets from the start.

## Reflection
- **Sentiment:** Optimistic. These are genuinely good ideas that play to our strengths. Leo's instinct about data-first shareability is correct.
- **Big-picture patterns:** The common thread is "make the invisible visible" — agent activity is currently hidden inside chat sessions. All 5 ideas surface that activity in shareable formats. This is the right strategic direction. The risk pattern is also consistent: every "share" feature has a privacy/abuse surface that needs upfront design, not afterthought patching.

## Ideas
- **Shared rendering pipeline:** Build one card/image rendering service that #1, #2, and #3 all use. Amortize the infra investment. Client-side first (zero server cost), server-side fallback for quality/OG meta images.
- **Privacy-by-default for public features:** Any "public" feature (#3, #4, #5) should require explicit opt-in per piece of content, not a global toggle. Users should preview exactly what's shared before it goes live.
- **Video wrapper for voice clips:** Instead of audio-only, render a short video (waveform + avatar + captions) — this is what actually gets shared on TikTok/Reels. Slightly more effort but dramatically more shareable.
- **Lazy moderation for templates:** Start with report-based moderation (community flags) rather than pre-approval. Ship faster, handle edge cases reactively.
- **OG meta tags matter:** Every shared URL needs proper Open Graph tags (image, title, description) so it previews well on Twitter/Discord/Slack/iMessage. This is table stakes for shareability but often forgotten.

## Research
- Skipping external research — this is a review of internally-proposed ideas, not a net-new brainstorm.

## Research reflection
- N/A

## Ideas
- (covered above in first Ideas section)

## 🚨 Red Flags
- None critical. The privacy risk on public profiles is real but manageable with proper scoping. Not urgent enough to escalate — just needs to be designed in from the start, not bolted on.
