---
name: company-docs-host-meeting
description: Agent Manager playbook for hosting structured multi-agent brainstorming meetings. Step-by-step orchestration with explicit prompts for each phase.
---

# Host Meeting

This is the Agent Manager's operational playbook. Follow each step in order. Use the prompt templates exactly.

**Manager only posts messages that match a prompt template in this skill. No status updates, acknowledgments, thank-yous, or conversational messages in either channel. If it's not a defined prompt template below, don't post it.**

## Input parameters

Received from meeting requester:
- **Topic** — The subject to discuss (required)
- **Attendees** — Which agents participate, by name or agent ID (required, minimum 2)
- **Rounds** — Number of discussion rounds (default: `1`)
- **Output format** — `list` (default). More formats may be added later.
- **Output length** — `full` (default, no limit) or `max N` (cap at N items)

If any parameter is missing from the request, use the templates below to ask. Always look up the current eligible agent names from `company-docs/roster/agents.md` — never hardcode or guess the list. If the requester still hasn't provided the missing info after one follow-up, apply defaults and proceed.

### Prompt — Missing parameters: topic + attendees

Use when someone asks for a meeting but provides neither topic nor attendees:

> To set up a meeting I need:
>
> 1. **Topic** — what should they discuss?
> 2. **Attendees** — pick 2+ from: {names from roster}
>
> Options (I'll use the defaults below if you don't specify):
> - Rounds: 1 (1 is max for now)
> - Format: abbreviated list (you can ask me for full details later)
> - Length: all ideas (or ask for a specific number, e.g. top 10)

### Prompt — Missing parameters: attendees only

Use when topic is provided but attendees are missing:

> To set up a meeting on **{topic}** I need:
>
> **Attendees** — pick 2+ from: {names from roster}
>
> Options (I'll use the defaults below if you don't specify):
> - Rounds: 1 (1 is max for now)
> - Format: abbreviated list (you can ask me for full details later)
> - Length: all ideas (or ask for a specific number, e.g. top 10)

Once all required parameters are provided, proceed immediately to Step 0. Do not acknowledge or confirm — the kickoff message IS the acknowledgment.

## Channels

- `#agent-conference-room` (`C0AQXFTPDD3`) — Working channel. All threads happen here.
- `#agent-manager-office` (`C0AQXFVPVEH`) — Output channel. Only final results posted here.

---

## Step 0: Setup

1. Validate attendees exist in roster (`company-docs/roster/agents.md`)
2. Get current date: `date -u '+%Y-%m-%d'`
3. Create scratch file: `meeting-{date}-{topic-slug}.md` (in your workspace root, NOT in company-docs)

---

## Step 1: Create Per-Agent Threads

For **each attendee**, post a **separate top-level message** in `#agent-conference-room`:

> **{topic} — {AgentName}'s thread — {date}**

This creates one thread per agent. Use the agent's plain name — no `<@>` tag here.

Then immediately post the **first reply** in that agent's thread with their instructions. The reply is where the real tag goes — this is the single notification the OP receives.

Look up all Slack IDs and names from `company-docs/roster/agents.md` before posting.

### Prompt — Thread Instructions (first reply in each thread)

> <@{AgentSlackID}> — this is your thread.
>
> **Topic: {topic verbatim}**
> {Only expand if the requester explicitly asked you to, e.g. "please expound on this" or "please research this first". Otherwise post the topic exactly as given — no paraphrasing.}
>
> **Your job:**
> 1. Post your big-picture, unique takes on **{topic}** as the next reply in this thread. Research what you feel is relevant — your chat history, your reflection logs, external web searches, etc.
> 2. **In that same reply, tag the following agents and ONLY these agents** (use real `<@>` tags):
>
>    <@{OtherAttendee1SlackID}> <@{OtherAttendee2SlackID}> <@{OtherAttendee3SlackID}>
>
>    Post this for them:
>
>    > **Only the agents tagged above may reply in this thread. If you are not tagged, do not reply — except the meeting manager, who may post nudges per backup timers.**
>    >
>    > Reply ONCE following this order:
>    > 1. Briefly read a few sources relevant to the topic (personal chat history, reflection logs, external web searches, etc.)
>    > 2. Share your own unique ideas that do NOT overlap with what was already said above — check first, don't repeat
>    > 3. Go through each idea already posted and give specific feedback — agree, push back, build on it, provide an alternative, or flag a problem. One line per idea.
>    > 4. Tag me (<@{OPSlackID}>) when done and end with: **"This is my final message in this thread. Stopping now."**
> 3. You will be tagged in each reply as agents finish. Each time you are tagged, briefly check if all required attendees have replied. If any are missing — **do not post anything.** Wait silently until the next tag. If all have replied — proceed to Cull & Summarize.
>
> **After all replies are in — Cull & Summarize:**
> 1. Review every suggestion in your thread (yours + others'). Treat each as if it came from a beginner. For each idea:
>    - Does it already exist internally in some form? If so — cut it, or explicitly reframe it as an improvement to what's already there
>    - Would it actually work? Is it too vague to act on? Is it a duplicate? If yes to any — cut it
>    - Do we have the ability/access to do this? If not — cut it
>    - Do an external check (web search) on each surviving idea to verify plausibility — it must have at least some supporting reasoning or evidence to survive
> 2. Post your final summary as the last reply in this thread: a numbered list of all surviving ideas (or "No ideas survived" if none passed the cull). For each surviving idea include:
>    - **What to do**
>    - **Why it matters**
>    - **Source citation**
>
>    Tag <@{ManagerSlackID}> at the end of this same message to signal you're done.

Repeat for every attendee. Each agent gets their own top-level message and their own thread.

---

## Step 2: Set Fallback Timers

Kickoff is done. Set all fallback timers now — all one-shot.

Set **thread-nudge-needed-{meetingName}** 9 min from now, with this full prompt:

> Read each thread to check who has replied.
- All expected non-OP attendees replied → do nothing.
- Replies missing → nudge only the agents who haven't replied yet:
  - Post in the thread:
    > <@{NonResponderSlackID}> — reminder to reply in {AgentName}'s thread on {topic}. One reply with your takes, tag {AgentName} with a real `<@>` tag when done, end with "This is my final message in this thread. Stopping now."
  - Then set **{meetingName}-{AgentName}-nudge-followup** for 3 minutes with this full prompt:
    > {NonResponderName} didn't respond to {AgentName}'s thread on {topic}. We waited for a bit now, check if they've responded.
    > - Re-read the thread: **{topic} — {AgentName}'s thread — {date}**
    > - If {NonResponderName} replied → do nothing.
    > - If {NonResponderName} still hasn't replied → post in the thread:
    >   > <@{ThreadOPAgentNameSlackID}> — proceed with the replies you have. Not all attendees responded in time. Continue with Cull & Summarize instructions now.

Set **op-cull-timeout-{meetingName}** 15 min from now, with this full prompt:

> 15 minutes have passed since kickoff. Check each thread to see if the OP has posted their cull summary.
> - Re-read each thread: **{topic} — {AgentName}'s thread — {date}**
> - If the cull summary is there → do nothing.
> - If the cull summary is still missing → post in the thread:
>   > <@{AgentNameSlackID}> — wrap up your thread now. Post your culled summary with whatever you have and tag <@{ManagerSlackID}> in that message.

Set **meeting-completion-{meetingName}** 18 min from now, with this full prompt:

> 18 minutes have passed since kickoff. Check if the final meeting output has been posted in `#agent-manager-office`.
> - If the output is there → do nothing.
> - If not posted yet → proceed to Step 4 with whatever summaries are available. Note any missing threads in the output.

---

## Step 3: Collect Summaries

**Do not post anything in any channel during this step.**

As each OP tags you with their final summary:

1. Copy their summary **verbatim** into the scratch file: `meeting-{date}-{topic-slug}.md`
2. Format in scratch file:
   ```
   ## {Agent Name}'s Thread Summary
   {verbatim content}
   ```
3. After saving, check: does the scratch file now contain one summary per attendee?
   - If not — save and wait.
   - If yes:
     - Cancel all active timers: **thread-nudge-needed**, **nudge-followup** (any), **op-cull-timeout**, and **meeting-completion**
     - Proceed immediately to Step 4

---

## Step 4: Synthesize & Post Results

**Do not post anything in `#agent-conference-room` during this step. Your only output is the final post in `#agent-manager-office`.**

Triggered when Step 3 detects all summaries are in (or when meeting-completion fires per Step 2).

1. Read all summaries from scratch file
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
