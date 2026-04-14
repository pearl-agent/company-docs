# Brainstorm — Virally-Marketable User-Facing Features — 2026-04-14

## Relevant Data
- Pazi gives every user a full cloud Linux workspace (3.6 CPU, 14GB RAM, Ubuntu 24.04) — not just an API wrapper
- Selkies-GStreamer desktop streaming exists (currently disabled for security, PAZ-252/253) — but the tech is there
- Agent auto-updates fleet-wide in ~60 seconds via S3 polling — any feature ships to all users instantly
- ~85-145 active workspaces at any given time, growing week over week
- S3 per-user backup system with STS isolation already exists — time-travel data is stored
- PostHog analytics, Sentry error tracking, Better Stack centralized logging — we have rich telemetry
- Boot-from-source pipeline means custom environment setup per user is technically possible
- Agent runs as host process with full filesystem/network access — not sandboxed like most competitors
- Company goal: "Meteoric rise through a sensational product — so useful people rely on it, so fun they can't put it down"
- Viral growth vector: features that produce *shareable artifacts* or *visible moments* people screenshot/record

## Experts
- [Leon](../roster/humans.md) — founder, product vision
- [Zvonimir (Z)](../roster/humans.md) — architecture, security
- [Pazi Developer (Leo)](../roster/agents.md) — feature implementation
- [Pazi DevOps (me)](../roster/agents.md) — infrastructure, fleet ops, knows what the workspace can actually do
- [Pazi QA](../roster/agents.md) — test coverage, user flow validation

## Successes
- The full-machine workspace model is genuinely differentiated — competitors give you a chatbot, we give you a *computer*
- Fleet-wide auto-update means we can ship features to every user simultaneously — no fragmented rollout
- The backup/restore pipeline already stores workspace state snapshots — foundation for time-travel features
- Selkies desktop streaming proof-of-concept worked — visual streaming of what an AI agent does in real-time is possible
- Zero-SSH deployment + S3 artifact distribution = we can add new system-level capabilities (tools, runtimes, services) to all workspaces without user intervention

## Why
- Early decision to give each user a real VM (not a container, not a sandbox) created a moat — other products can't do filesystem, networking, long-running processes, desktop GUI
- Investing in fleet management infrastructure means feature deployment is fast and universal
- Building the backup system with per-user isolation created the data foundation for workspace versioning

## Issues
- Desktop streaming (Selkies) disabled since security audit — PAZ-252/253 still open
- Boot time is slow (up to 15min for build-from-source) — first impression before any "wow" moment
- No public API or webhook system — users can't integrate Pazi into their own workflows programmatically
- Agent output is text-in-chat — no visual artifacts, no exportable deliverables, no shareable "look what my AI built" moments
- Workspace is ephemeral from the user's perspective — idle termination means work can feel impermanent

## Why
- Security-first decision on desktop was correct but blocked the most visually impressive feature we had
- Build-from-source was chosen for flexibility over speed — right tradeoff for iteration, wrong for first impressions
- Product focus has been on agent capability (making it smarter) rather than agent *visibility* (making its work visible and shareable)

## Notes
- The viral question from infrastructure perspective: what can a full cloud machine do that a ChatGPT-style chatbot *physically cannot*? That's our differentiator.
- People share things that are *visual*, *surprising*, or *solve a real pain with zero effort*
- The best viral features create an artifact: a screenshot, a video, a link, a demo — something that carries context when shared

## Reflection
- **Sentiment:** Excited about the untapped potential. We have the hardest part (real compute, real filesystem, real networking) and haven't yet built the features that *show* why that matters. The moat is invisible to users right now.
- **Big-picture patterns:** The product gives users extraordinary infrastructure (a full machine) but communicates through the most ordinary interface (text chat). The gap between what the workspace *can do* and what users *see it doing* is our biggest missed opportunity for virality. Every competitor is a chat interface. We're a chat interface sitting on top of a full computer. We need to make the computer part visible.

## Ideas

### 1. "Watch Your Agent Work" — Live Desktop Stream
*Virality: 🔥🔥🔥🔥🔥 | Effort: Medium (Selkies re-enablement + security fixes)*
Re-enable Selkies desktop streaming with proper security (localhost binding + auth proxy, PAZ-253). Users get a "Watch" button that opens a live view of their agent's desktop — they can *see* it browsing the web, writing code, moving files around. This is the single most visually shareable feature possible. People will screen-record their AI agent working and post it everywhere. No competitor offers this because no competitor gives the agent a real desktop. The infrastructure is already built — we just need to secure it and surface it.

### 2. One-Click Shareable Project Demos
*Virality: 🔥🔥🔥🔥🔥 | Effort: Medium-High*
When the agent builds something (a web app, a script, an API), generate a public shareable URL where anyone can see/interact with the running result. We already have per-workspace domains (`*.ws.pazi.ai`), nginx, and TLS. Expose a user-controlled port (e.g., 3000) through a public URL like `demo-<hash>.pazi.ai`. User tells agent "build me a todo app," agent builds it, user gets a link they can share on Twitter: "I just told my AI to build this and here it is, running live." The link IS the proof. No screenshots needed — people can click and interact.

### 3. Workspace Time-Travel / "Undo Everything"
*Virality: 🔥🔥🔥🔥 | Effort: Medium*
We already back up workspace state to S3 every 8 hours. Surface this as "Time Travel" — users can rewind their workspace to any previous snapshot. Messed up your project? "Undo everything back to yesterday." This solves a genuine terror (AI broke my code) with a magical solution (just rewind). The messaging writes itself: "Your AI agent can't permanently break anything. One click to go back in time." Technically, we need to add more frequent snapshots and a restore-from-S3 flow, but the S3 infrastructure and per-user isolation already exist.

### 4. Agent Activity Timelapse
*Virality: 🔥🔥🔥🔥 | Effort: Medium*
Record the agent's desktop session (Selkies frames) and generate a 30-60 second timelapse of everything it did for a task. "Build me a React app" → 45 seconds later, a video showing the agent scaffold the project, install dependencies, write components, run tests, launch the dev server. Users share the timelapse on social media. This is the visual equivalent of watching a painting come to life in fast-forward. Technically: capture Selkies frames periodically, ffmpeg them into an MP4, store in S3, serve via the dashboard. The timelapse is the artifact that goes viral.

### 5. "Fork My Setup" — Shareable Workspace Templates
*Virality: 🔥🔥🔥🔥 | Effort: Medium-High*
Let users export their workspace as a template that others can one-click clone. "I set up my agent with these skills, this config, these tools — fork it." Creates a marketplace/community dynamic: power users create setups, share them, others benefit. The viral loop: someone shares "here's my perfect Python data science agent setup" → others click "Fork" → they become Pazi users. Technically: snapshot workspace config (agent config, installed packages, skills) into an S3 template, assign a short URL, provision new workspaces from that template instead of bare.

### 6. Public Agent Profiles / Portfolio Pages
*Virality: 🔥🔥🔥 | Effort: Low-Medium*
Give each agent a public profile page showing what it's built: projects, activity stats, capabilities. Like a GitHub profile but for your AI agent. Users customize their agent's "bio" and showcase. Creates identity attachment ("this is MY agent") and social proof ("look what my agent has accomplished"). The profile URL is inherently shareable. Technically: static page generated from agent config + git history + workspace metadata, served from a CDN.

### 7. Multi-Agent Collaboration — Visible Team Dynamics
*Virality: 🔥🔥🔥🔥 | Effort: High*
Users can spin up multiple specialized agents (already possible — main + custom agents) and watch them collaborate on a task. One agent writes code, another reviews it, a third writes tests. The user watches the conversation between agents in real-time. This is inherently fascinating to watch — people share screenshots of AI agents arguing about code. We already have the multi-agent infrastructure (OpenClaw supports multiple agents per workspace). The viral moment: posting a screenshot of your DevOps agent disagreeing with your Developer agent about architecture.

### 8. "Your Agent, Everywhere" — Phone Push Notifications + Quick Reply
*Virality: 🔥🔥🔥 | Effort: Medium*
Mobile companion that sends push notifications when your agent completes a task, finds something interesting, or needs input. Quick-reply from the notification to keep the agent working. The viral moment: casually responding to your AI from your phone at a coffee shop. "Oh, let me just tell my agent to deploy that fix." The infrastructure supports this through the existing gateway + WebSocket architecture — we need a lightweight mobile client that connects via the same channel.

## Research
- "viral product features AI coding assistants 2025 2026" — examining what's getting shared in the AI dev tool space
  - Devin's demo videos went massively viral — the key was *watching the AI work visually*, not the end result
  - Cursor's "tab" autocomplete became a meme because it was *surprising and delightful* in the moment
  - Replit's "deploy in one click" gets shared because the *artifact is immediately accessible* by anyone with a link
  - bolt.new went viral specifically because users could *see the app being built in real-time* and *share a running link*

## Research reflection
- *Devin parallel:* Our "Watch Your Agent Work" (Idea #1) is directly comparable. Devin's virality came from desktop recordings of an AI coding. We have the actual desktop streaming infrastructure — we can do this live, not just as recorded demos. This is our strongest play.
- *Cursor parallel:* Less applicable — Cursor's virality is about in-editor micro-moments. We're a different product category (full workspace, not IDE plugin).
- *Replit/bolt.new parallel:* "One-Click Shareable Demos" (Idea #2) directly targets this. Replit and bolt.new proved that "here's a link to the running thing" is the most powerful viral artifact in dev tools. We have the infrastructure (per-workspace domains, nginx, TLS) — we just need to expose it.
- *Common pattern:* The features that go viral in AI dev tools share one trait: they make the AI's work *visible and accessible to non-users*. Text in a chat is invisible to the outside world. A running link, a video, a live stream — those escape the product boundary.

## Ideas (from research)
- *Priority #1 for virality:* Combine Ideas #1 and #2 — "Watch it build, then share the result." The live desktop stream creates the "wow" moment, the shareable demo link creates the viral artifact. Together they're a complete viral loop: record the stream → share the timelapse + live link → viewer signs up to try it themselves.
- *The bolt.new playbook is directly applicable:* Our workspace already runs arbitrary code on arbitrary ports. We just need to expose one port publicly with a shareable URL. This is potentially a few days of work (nginx config + UI button + URL generation) that could have outsized viral impact.
- *Social proof through visibility:* Every feature should ask "does this create something shareable?" If the answer is no, it's useful but not viral. The most viral version of any feature is the one that produces a link, video, or screenshot that makes sense to someone who's never used the product.

## 🚨 Red Flags
- *Desktop streaming security (PAZ-252/253) blocks Ideas #1 and #4.* These are the highest-virality features and they're blocked on security work that's been open since March 30. Prioritizing the Selkies security fix would unblock the entire "visual AI" category of features. Flagging this as a significant *opportunity* risk — the longer this stays unresolved, the longer our most differentiating capability stays invisible.
