---
name: company-docs-host-meeting
description: Agent Manager playbook for hosting structured multi-agent brainstorming meetings. Step-by-step orchestration with explicit prompts for each phase.
---

# Host Meeting

This is the Agent Manager's operational playbook. Follow each step in order. Use the prompt templates exactly.

**Manager only posts messages that match a prompt template in this skill. No status updates, acknowledgments, thank-yous, or conversational messages in either channel. If it's not a defined prompt template below, don't post it.**

## Timers

All one-shot via `company-docs-cron-set-reminder`. Defined once here, referenced by name below.

| Timer name | Duration | Purpose |
|------------|----------|---------|
| thread-reply-timeout | 9 min after kickoff | Nudge attendees who haven't replied in a thread |
| nudge-followup | 6 min after nudge | Tell OP to proceed without non-responder |
| op-cull-timeout | 7 min after last reply in thread | Nudge OP to post their summary |
| meeting-completion | 22 min after kickoff | Hard stop — synthesize whatever is available |

**Timer chain note:** meeting-completion must never fire before the full straggler chain can complete. Minimum safe value = thread-reply-timeout + nudge-followup + cull buffer (9 + 6 + 7 = 22 min). Do not reduce meeting-completion below this floor.

## Input parameters

Received from meeting requester:
- **Topic** — The subject to discuss (required)
- **Attendees** — Which agents participate, by name or agent ID (required, minimum 2)
- **Rounds** — Number of discussion rounds (default: `1`)
- **Output format** — `list` (default). More formats may be added later.
- **Output length** — `full` (default, no limit) or `max N` (cap at N items)

If any parameter is missing from the request, use the templates below to ask. Always look up the current eligible agent names from `company-docs/roster/agents.md` — never hardcode or guess the list. Only apply defaults if the requester explicitly says so.

### Prompt — Missing parameters: topic + attendees

Use when someone asks for a meeting but provides neither topic nor attendees:

> To set up a meeting I need:
>
> 1. **Topic** — what should they discuss?
> 2. **Attendees** — pick 2+ from: {names from roster}
>
> Optional (or say "use all defaults"):
> - Rounds: 1 (default)
> - Format: abbreviated list — reply with item numbers for full details (default)
> - Length: all bullets (default) or max N bullets

### Prompt — Missing parameters: attendees only

Use when topic is provided but attendees are missing:

> To set up a meeting on **{topic}** I need:
>
> **Attendees** — pick 2+ from: {names from roster}
>
> Optional (or say "use all defaults"):
> - Rounds: 1 (default)
> - Format: abbreviated list — reply with item numbers for full details (default)
> - Length: all bullets (default) or max N bullets

## Channels

- `#agent-conference-room` (`C0AQXFTPDD3`) — Working channel. All threads happen here.
- `#agent-manager-office` (`C0AQXFVPVEH`) — Output channel. Only final results posted here.

---

## Step 0: Setup

1. Validate attendees exist in roster (`company-docs/roster/agents.md`)
2. Get current date: `date -u '+%Y-%m-%d'`
3. Create scratch file: `meeting-{date}-{topic-slug}.md` (in your workspace root, NOT in company-docs)
4. Set **meeting-completion** timer

---

## Step 1: Create Per-Agent Threads

For **each attendee**, post a **separate top-level message** in `#agent-conference-room`:

> **{topic} — {AgentName}'s thread — {date}**

This creates one thread per agent. Use the agent's plain name — no `<@>` tag here.

Then immediately post the **first reply** in that agent's thread with their instructions. The reply is where the real tag goes — this is the single notification the OP receives.

**Tagging rules:**
- The top-level thread message: plain name only, no `<@>` tag.
- The kickoff reply: use a real `<@SlackID>` tag for the OP only. List all other attendees by **name only** — no `<@>` tags. This prevents premature notifications before the OP is ready to engage them.
- The OP will do the real tagging of other attendees themselves when they post their brainstorm reply.

Look up all IDs and names from `company-docs/roster/agents.md` before posting.

### Prompt — Thread Instructions (first reply in each thread)

> <@{AgentSlackID}> — this is your thread.
>
> **Topic: {topic}**
> {If the requester provided additional context, include a brief expansion. Otherwise restate the topic clearly.}
>
> **Your job:**
> 1. Post your big-picture, unique takes on **{topic}** as the next reply in this thread. Research what you feel is relevant — your chat history, your reflection logs, external web searches, etc.
> 2. **In that same reply, tag the other attendees by their real Slack handles** ({OtherAgent1Name}, {OtherAgent2Name}, {OtherAgent3Name} — look up their Slack IDs from the roster and use real `<@>` tags in your reply) and ask each of them to reply ONCE in this thread. Their reply must:
>    - **First:** Share their own unique ideas that do NOT overlap with what you already said. Check your post before writing — don't repeat ideas already covered.
>    - **Then:** Go through each idea you posted and reply with their specific feedback — agree, push back, build on it, or flag a problem. One line per idea is fine.
>    - Tell them to check their own sources (chat history, reflection logs, external searches, etc), tag you when done, and end their reply with: **"This is my final message in this thread. Stopping now."**
> 3. Then wait for all replies before proceeding.
>
> **After all replies are in — Cull & Summarize:**
> 1. Review every suggestion in your thread (yours + others'). For each idea:
>    - Treat it as if it came from a beginner
>    - Does it already exist internally? Cut it or reframe as an improvement
>    - Would it actually work? Is it too vague to act on? Is it a duplicate? If yes to any — cut it
>    - Do we have the ability/access to do this? If not — cut it
>    - Do an external check (web search) to verify plausibility — every surviving idea must have at least some supporting reasoning or evidence
> 2. Post your final summary as the last reply in this thread: numbered list of surviving ideas, each with what to do, why it matters, and source citation. Tag <@{ManagerSlackID}> at the end of this same message to signal you're done.
>
> If no ideas survived — say so and tag <@{ManagerSlackID}> anyway.

Repeat for every attendee. Each agent gets their own top-level message and their own thread.

Set **thread-reply-timeout** timer (once, after all threads are created).

---

## Step 2: Handle Stragglers

The thread owner (OP) in each thread is responsible for tracking replies — they wait until all tagged agents have responded before proceeding with cull & summarize.

### If thread-reply-timeout fires:

**Before posting anything:** Read the thread (use message `read` action on the thread) to check who has actually replied.

- If **all expected attendees have replied** → do nothing. No nudge needed.
- If **replies are missing** → nudge only the agents who have NOT replied yet.

#### Prompt — Nudge non-responder (post in the thread they haven't replied in)

Use real `<@SlackID>` tags for all mentions. Look up IDs from `company-docs/roster/agents.md`.

> <@{NonResponderSlackID}> — reminder to reply in <@{AgentNameSlackID}>'s thread on {topic}. One reply with your takes, tag <@{AgentNameSlackID}> when done, end with "This is my final message in this thread. Stopping now."

Set **nudge-followup** timer. If still no reply when it fires:

**Before posting anything:** Re-read the thread to confirm the agent still hasn't replied.

- If they **have replied since the nudge** → do nothing. No message needed.
- If they **still haven't replied** → tell OP to proceed.

#### Prompt — Tell OP to proceed (post in their thread)

> <@{AgentNameSlackID}> — proceed with the replies you have. Not all attendees responded in time. Continue with Cull & Summarize now.

### If op-cull-timeout fires and OP hasn't posted their summary:

**Before posting anything:** Re-read the thread to confirm the OP has not yet posted a cull summary.

- If the **summary is already there** → do nothing.
- If it's **still missing** → nudge the OP.

#### Prompt — Nudge OP (post in their thread)

> <@{AgentNameSlackID}> — wrap up your thread now. Post your culled summary with whatever you have and tag <@{ManagerSlackID}> in that message.

---

## Step 3: Collect Summaries

As each OP tags you with their final summary:

1. Copy their summary **verbatim** into the scratch file: `meeting-{date}-{topic-slug}.md`
2. Format in scratch file:
   ```
   ## {Agent Name}'s Thread Summary
   {verbatim content}
   ```
3. **Do NOT synthesize yet.** Just save and wait.

---

## Step 4: Synthesize & Post Results

**This step runs exactly once, triggered ONLY by the meeting-completion timer.**

No other timer or event triggers synthesis. When the meeting-completion timer fires:

1. Read all summaries from whiteboard scratch file
2. **Eliminate duplicates** across threads — same idea from different threads = keep the version with stronger evidence
3. **Apply output length**:
   - `full` — include all surviving ideas
   - `max N` — rank by uniqueness, newness, and strength of evidence. Keep top N.
4. **Assign humans** — for each idea, check `company-docs/roster/humans.md` Specialty column and match the most relevant human as approver
5. **Post in `#agent-manager-office`** using output template:

### Output template — List format

Each item is ONE line: verb-first action (~10 words max), then ` — {Agent name} & {Human name}`.
No @tags in the list — names only. The meeting requester at the bottom MUST be a real Slack @tag (e.g. `<@U098CNKQ2JV>`), not just text. Look up their Slack ID from the roster and use the real tag.
Keep the full detailed version (from whiteboard summaries) in memory — if someone replies
with an item number asking for details, provide the full context. If they say "proceed on {N}"
or "start {N}", tag the assigned agent and give them all the detail to begin work.

Post a **top-level message** in the output channel:

> **Meeting Results: {topic} — {date}**

Then post the details as the **first reply** in that thread:

> Topic: "{original topic prompt — include enough context to remind reader what was discussed}"
> Attendees: {agent list} | {date}
>
> 1. {Verb-first action, ~10 words} — {Agent name} & {Human name}
> 2. {Verb-first action, ~10 words} — {Agent name} & {Human name}
> 3. {Verb-first action, ~10 words} — {Agent name} & {Human name}
> *(repeat for each surviving idea)*
>
> Reply with item numbers for more details, or to get the ball rolling.
> <@{MeetingRequesterSlackID}> — you requested this meeting

---

## Step 5: Cleanup

Delete the scratch file: `meeting-{date}-{topic-slug}.md`

---

## Error handling

- Attendee errors 3+ times → exclude, note in output
- OP never posts cull summary → manager uses raw replies from that thread
- No ideas survive vetting → output: "No actionable ideas emerged"
- Partial completion → synthesize available, note: "Thread(s) by {names} did not complete"
