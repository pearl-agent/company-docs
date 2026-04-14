# Brainstorm — Low-Hanging-Fruit Features to Improve Functionality — 2026-04-14

## Relevant Data
- Just shipped PAZ-330 (Tech Team Template): agent templates with sequential creation, partial failure recovery, template-based onboarding
- Just shipped PAZ-325 (Goals): goal creation via agent + UI, scheduled tasks integration, GoalCreatedCard
- PAZ-297 (Slack connection flow): overhauled Slack setup from Socket Mode to webhooks, removed friction
- Agent roster: 11 agents, 3 tiers — multi-agent coordination is core product architecture
- Product vision: "So useful people rely on it, so fun they can't put it down"
- Key growth axes: functional usefulness, fun usability, viral-marketable features, polished UX
- Frontend has stubs for skills.delete and skills.create but no gateway-side implementation yet
- Recent QA patterns: lots of infrastructure blockers (OOM on t3.micro, API overwritten by deployments, session expiry)
- Husky/precommit was silently skipped in worktrees — caught and fixed, but shows "silent failures" pattern
- Goals feature went through 3 rework cycles based on Zvonimir's UX feedback — confirmation cards → direct creation
- Slack setup had a 3-day root cause hunt for a single manifest field (`app_home.messages_tab_enabled`)

## Experts
- Leon (Founder) — product direction, infrastructure
- Zvonimir (CEO) — product UX, quality bar, feature vision
- Alan (Tech Lead agent) — ticket management, QA coordination
- Pazi QA — testing, E2E verification
- Me (Leo, Developer) — implementation, PR delivery

## Successes
- Tech Team Template shipped cleanly — multi-agent creation with progress indicators and partial failure recovery
- Goals feature iteratively improved through tight feedback loops with Zvonimir
- Slack connection overhaul reduced setup friction dramatically
- Agent tool integration pattern (agent calls tool → UI card renders → user interacts) is proven and extensible
- Cross-review workflow (Codex vs Claude Code) consistently produces solid implementation plans

## Why
- Short feedback loops: Zvonimir tests on pazi.dev, gives immediate feedback, we iterate same day
- Strong QA process catches real bugs before merge
- Template pattern allows rapid agent bootstrapping
- The "agent tool → card" pattern is modular — once the pattern exists, new tools are relatively cheap to add

## Issues
- Goals feature required 3 rework cycles because initial UX assumptions didn't match Zvonimir's vision
- Slack setup debugging took 3 days for a single manifest field — diagnostic tooling gap
- QA infrastructure blockers (OOM, deployment conflicts) slow testing cycles
- Skills management is half-built (frontend stubs exist, gateway RPCs missing delete/create)
- No user-facing feedback loop — users can't easily tell us what's broken or what they want
- Agent onboarding is template-based but there's no "what do you want to do?" discovery flow
- No activity feed or timeline — users can't see what their agents have been doing

## Why
- UX rework cycles: building before validating assumptions → could use lightweight mockups or spec confirmation
- Slack debugging gap: no structured diagnostic tool for integration setup → errors are silent and opaque
- Infrastructure contention: single staging environment shared across all features → deployment conflicts
- Skills gap: skills were built for internal agent use, not yet for user-facing CRUD
- No feedback channel: product is internally driven right now — users have no structured way to surface needs
- No discovery flow: users land with an agent but no guided path to their first useful interaction
- No activity feed: agents do work but users can't passively see it — have to actively ask

## Notes
- The "agent tool → UI card" pattern is the most extensible part of the architecture — each new card is a new feature
- Tech team template proves multi-agent creation works — could extend to other "team recipes"
- Goals integration proves agents can drive persistent state changes — opens door for habits, reminders, trackers
- Most of these ideas require minimal backend changes — they're about connecting existing pieces better

## Reflection
- **Sentiment:** Optimistic. The core architecture is solid and extensible. Most low-hanging fruit is about *connecting* things that already exist, not building from scratch.
- **Big-picture patterns:** The product has strong infrastructure (agents, tools, cards, templates) but weak "glue" — discovery, visibility, and feedback loops. Users can do powerful things but might not know how, and can't see what's happening unless they ask. The wins will come from making existing power visible and accessible.

## Ideas
1. *Agent Activity Feed / Timeline* — A sidebar or dashboard view showing what agents have done recently (tasks completed, goals updated, messages sent). Low effort: agents already log events; this is a UI layer. High impact: makes the product feel alive and useful even when the user isn't actively chatting.

2. *Quick Actions / Suggested Prompts on Agent Cards* — When viewing an agent, show 3-5 contextual suggested actions ("Set a goal", "Check my calendar", "Connect Slack"). Reduces the blank-chat-box problem. Could be template-driven — each agent type defines its suggestions.

3. *Integration Health Dashboard* — A simple status page showing connected integrations (Slack ✅, GitHub ✅, Calendar ❌) with one-click setup. We already have the connection flows; this surfaces them. Makes the product feel complete vs "I don't know what's connected."

4. *Skill Gallery with One-Click Install* — Frontend has skills.create stubs. Building the gateway RPCs + a simple gallery UI would let users browse and add skills to their agents. Transforms agents from static templates to customizable assistants. Viral angle: "I taught my agent to do X."

5. *"What Can You Do?" Command* — A universal agent command that returns a formatted card with the agent's capabilities, connected integrations, and active scheduled tasks. Zero backend — agent introspects its own config and skills. Immediately useful for onboarding.

6. *Notification Digest* — Instead of real-time notifications for every agent action, offer a daily/weekly digest email or in-app summary. Already have goals, scheduled tasks, and agent events — just need aggregation. Makes agents feel like proactive assistants, not noisy bots.

7. *Agent Personality Customization* — Let users tweak their agent's tone (formal/casual/funny) and interests via a settings panel. Trivial to implement: it's a system prompt modifier. But the UX impact is huge — "my agent feels like mine." Fun + viral: people share funny agent responses.

8. *Onboarding Wizard with Intent Detection* — After template creation, run a short 3-question chat flow: "What do you mainly want help with?" → route to relevant skill setup. Converts the generic "hi, I'm your agent" into an immediately useful first interaction.

9. *Goal Templates / Presets* — "Learn a new skill", "Ship a feature by Friday", "Exercise 3x/week" — pre-built goal structures users can pick from. Goals feature already exists; this adds discoverability and reduces friction.

10. *Agent-to-Agent Handoff Visibility* — When agents collaborate (like our tech team flow), show the user a visual trace: "Developer created PR → QA testing → Tech Lead reviewing." Users see the team working. Builds trust and feels magical.

## Research
- "AI agent onboarding UX 2026" → https://www.vezadigital.com/post/ai-ux-ui-design-trends — Trend toward adaptive, personalized onboarding with multimodal interactions. Dynamic visual systems and accessibility-first design.
- "AI agent retention engagement" → https://a16z.com/state-of-consumer-ai-2025-product-hits-misses-and-whats-next/ — ChatGPT paid retention at 68% by month 12. Key: habitual use patterns, not just initial wow factor. Retention comes from solving real recurring problems.
- "AI agent platform quick wins" → https://www.lindy.ai/blog/best-ai-agents — Lindy highlights step-by-step onboarding lessons. Market trend: platforms compete on onboarding speed and "time to first value."
- "AI agent activity feed dashboard" → general industry trend — Products like Notion AI, Linear, and Zapier all added activity feeds in 2025. Users expect to see what automated systems did without asking.

## Research reflection
- *Adaptive onboarding:* Directly applicable. Our template system is step 1; adding intent-based routing after creation would be step 2. We already have the agent tools — we just need a guided flow that triggers them.
- *Retention through habitual use:* Critical. Our Goals feature is heading this direction (recurring scheduled tasks), but we need more "daily touchpoint" features — digest emails, activity feeds, proactive agent messages. The a16z data says retention comes from solving recurring problems, not one-off tasks.
- *Time to first value:* Our current flow is: sign up → create agent → blank chat. The gap between "blank chat" and "first useful thing" is where we lose people. Quick actions, suggested prompts, and onboarding wizards all close this gap.
- *Activity feeds as industry standard:* We should have this. Our agents already emit events — this is purely a UI/aggregation feature. Not having it makes us look behind competitors.

## Ideas
1. *First-value accelerator:* Combine onboarding wizard (#8) + quick actions (#2) + "What can you do?" (#5) into a cohesive "first 5 minutes" experience. This alone could significantly improve conversion from signup to retained user.

2. *Daily touchpoint system:* Notification digest (#6) + agent activity feed (#1) create passive engagement. User opens the app, sees what their agent did overnight. This is the habit loop — and it's mostly aggregation of existing events.

3. *Customization as viral feature:* Agent personality (#7) + skill gallery (#4) let users make agents "theirs." Combined with sharing — "Check out what my agent can do" — this becomes organic marketing.

4. *Multi-agent visibility:* Agent handoff trace (#10) is uniquely ours — competitors don't have multi-agent teams. Showcasing this visually is both a feature and a marketing asset. Demo clips of "watch my dev team work" could be sensational.

## 🚨 Red Flags
None — these are all additive features with no risk to existing functionality. The closest thing to a flag: the skills gateway gap (frontend stubs without backend) should be resolved before shipping a skill gallery, or it'll be a frustrating dead end for users.
