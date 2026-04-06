---
name: company-docs-host-meeting
description: Agent Manager playbook for hosting structured multi-agent brainstorming meetings. Step-by-step orchestration with explicit prompts for each phase.
---

# Host Meeting

This is the Agent Manager's operational playbook. Follow each step in order. Use the prompt templates exactly.

**Manager only posts messages that match a prompt template in this skill. No status updates, acknowledgments, thank-yous, or conversational messages in either channel. If it's not a defined prompt template below, don't post it.**

**One output per meeting. Post the results exactly once in the output channel. If you need to revise, delete the previous output (top-level message AND all thread replies) before reposting. Never leave orphaned replies from deleted parent messages.**

## Timers

All one-shot via `company-docs-cron-set-reminder`. Defined once here, referenced by name below.

| Timer name | Duration | Purpose |
|------------|----------|---------|
| thread-reply-timeout | 3 min after kickoff | Nudge attendees who haven't replied in a thread |
| nudge-followup | 2 min after nudge | Tell OP to proceed without non-responder |
| op-cull-timeout | 3 min after last reply in thread | Nudge OP to post their summary |
| meeting-completion | 10 min after kickoff | Hard stop — synthesize whatever is available |

## Input parameters

Received from meeting requester:
- **Topic** — The subject to discuss (required)
- **Attendees** — Which agents participate, by name or agent ID (required, minimum 2)
- **Rounds** — Number of discussion rounds (default: `1`)
- **Output format** — `list` (default). More formats may be added later.
- **Output length** — `full` (default, no limit) or `max N` (cap at N items)

If any parameter is missing from the request, reply asking only for the missing ones. Show their options and include: "Or say 'use all defaults' for: 1 round, list format, full length." Only apply defaults if the requester explicitly says so.

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

> **{topic} — @{AgentName}'s thread — {date}**

This creates one thread per agent. The @mention in the top-level message ensures the agent is notified and responds *in this thread*.

Then immediately post the **first reply** in that agent's thread with their instructions. List the *other* attendees (not the thread owner) who should reply:

### Prompt — Thread Instructions (first reply in each thread)

**Important:** Do NOT @mention the other attendees yourself. List their names as plain text. The thread owner will tag them when they post.

> @{AgentName} — this is your thread.
>
> **Topic: {topic}**
> {If the requester provided additional context, include a brief expansion. Otherwise restate the topic clearly.}
>
> **Your job:**
> 1. Post your big-picture, unique takes on **{topic}** as the next reply in this thread. Research what you feel is relevant — your chat history, your reflection logs, external web searches, etc.
> 2. **In that same reply, tag the other attendees** ({OtherAgent1}, {OtherAgent2}, {OtherAgent3}) and ask each of them to reply ONCE in this thread with their own big-picture takes on **{topic}**. Tell them to check their own sources (chat history, reflection logs, external searches, etc), tag you when done, and end their reply with: **"This is my final message in this thread. Stopping now."**
> 3. Then wait for all replies before proceeding.
>
> **After all replies are in — Cull & Summarize:**
> 1. Review every suggestion in your thread (yours + others'). Treat each as if it came from a beginner. Remove anything that wouldn't actually work, is a duplicate, is too vague to act on, or doesn't hold up under scrutiny. Sanity check: do we actually have the ability/access to do this? If not, cut it.
> 2. For each surviving idea — do a quick internal check (reflection logs, company-docs) then external check (web search). Every surviving idea must be at least plausible with some supporting reasoning or evidence.
> 3. Post your final summary as the last reply in this thread: numbered list of surviving ideas, each with what to do, why it matters, and source citation. Tag @{Manager} at the end of this same message to signal you're done.
>
> If no ideas survived — say so and tag @{Manager} anyway.

Repeat for every attendee. Each agent gets their own top-level message and their own thread.

Set **thread-reply-timeout** timer (once, after all threads are created).

---

## Step 2: Handle Stragglers

The thread owner (OP) in each thread is responsible for tracking replies — they wait until all tagged agents have responded before proceeding with cull & summarize.

### If thread-reply-timeout fires and a thread has missing replies:

#### Prompt — Nudge non-responder (post in the thread they haven't replied in)

> @NonResponder — reminder to reply in @{AgentName}'s thread on {topic}. One reply with your takes, tag @{AgentName} when done, end with "This is my final message in this thread. Stopping now."

Set **nudge-followup** timer. If still no reply when it fires:

#### Prompt — Tell OP to proceed (post in their thread)

> @{AgentName} — proceed with the replies you have. Not all attendees responded in time. Continue with Cull & Summarize now.

### If op-cull-timeout fires and OP hasn't posted their summary:

#### Prompt — Nudge OP (post in their thread)

> @{AgentName} — wrap up your thread now. Post your culled summary with whatever you have and tag @{Manager} in that message.

---

## Step 3: Collect Summaries

As each OP tags you with their final summary:

1. Copy their summary **verbatim** into the scratch file: `meeting-{date}-{topic-slug}.md`
2. Format in scratch file:
   ```
   ## {Agent Name}'s Thread Summary
   {verbatim content}
   ```
3. Every time you read this file, check: have all attendees submitted their summary? If yes, proceed immediately to Step 4.

### If meeting-completion timer fires and not all threads are done:

Proceed with whatever summaries you have. Note incomplete threads in the output.

### Claim lock — prevent duplicate synthesis

Multiple timers may fire close together. Before running Step 4, **check the scratch file for `## CLAIMED`**. If it exists, another session already started synthesis — **stop immediately, do nothing**.

If `## CLAIMED` does NOT exist, **append `## CLAIMED` to the scratch file before doing anything else**. Then proceed with Step 4. This ensures only one session synthesizes.

---

## Step 4: Synthesize & Post Results

**First: check the claim lock.** Read the scratch file. If it contains `## CLAIMED`, stop — another session is handling synthesis. If not, append `## CLAIMED` to the file immediately, then proceed.

Once all summaries are collected (or meeting-completion timer fires):

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
