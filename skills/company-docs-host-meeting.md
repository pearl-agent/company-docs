---
name: company-docs-host-meeting
description: Agent Manager playbook for hosting structured multi-agent brainstorming meetings. Step-by-step orchestration with explicit prompts for each phase.
---

# Host Meeting

This is the Agent Manager's operational playbook. Follow each step in order. Use the prompt templates exactly.

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

- `#agent-conference-room` — Working channel. All threads happen here.
- `#agent-manager-office` — Output channel. Only final results posted here.

---

## Step 0: Setup

1. Validate attendees exist in roster (`company-docs/roster/agents.md`) and have "Can Attend Meeting" marked as eligible
2. Get current date: `date -u '+%Y-%m-%d'`
3. Create scratch file: `company-docs/whiteboard/meeting-{date}-{topic-slug}.md`
4. Set **meeting-completion** timer

---

## Step 1: Start Threads

Post a **top-level message** in `#agent-conference-room`:

> **Meeting: {topic} — {date}**

Then immediately post the following as the **first reply** in that message's thread, tagging all attendees:

### Prompt — Kickoff (thread reply)

> Attendees: @Agent1 @Agent2 @Agent3
>
> **Topic: {topic}**
> {If the requester provided additional context or asked you to expand on the topic, include a brief expansion here. Otherwise just restate the topic clearly.}
>
> Each of you: post a **new top-level message** in this channel now.
>
> **Your message must:**
> 1. Title: `{topic} — {your name}'s thread — {date}`
> 2. Share your big-picture, unique takes on this topic: **{topic}**. Research what you feel is relevant — your chat history, your reflection logs, external web searches, etc.
> 3. Tag the other attendees and ask them to each reply ONCE in your thread with their own big-picture, unique takes on **{topic}** after checking their own relevant sources (chat history, reflection logs, external searches, etc). They must tag you when done and end their reply with: **"This is my final message in this thread. Stopping now."**
>
> **Rules:**
> - One top-level message per attendee
> - Do NOT reply in your own thread until all tagged agents have replied
> - When all tagged agents have replied, follow the Cull & Summarize instructions below
>
> **After all replies are in — Cull & Summarize:**
> 1. Review every suggestion in your thread. Treat each one as if it came from a beginner. Remove anything that wouldn't actually work, is a duplicate, is too vague to act on, or doesn't hold up under scrutiny.
> 2. For each surviving idea — do a quick internal check (reflection logs, company-docs) then external check (web search). Every surviving idea must be at least plausible with some supporting reasoning or evidence.
> 3. Post your final summary as the last reply in your thread: numbered list of surviving ideas, each with what to do, why it matters, and source citation. Tag @{Manager} at the end of this same message to signal you're done.
>
> If no ideas survived — say so and tag @{Manager} anyway.

Set **thread-reply-timeout** timer.

---

## Step 2: Handle Stragglers

The original poster in each thread is responsible for tracking replies — they wait until all tagged agents have responded before proceeding with cull & summarize.

### If thread-reply-timeout fires and a thread has missing replies:

#### Prompt — Nudge non-responder

> @NonResponder — reminder to reply in @OriginalPoster's thread on {topic}. One reply with your takes, tag @OriginalPoster when done, end with "This is my final message in this thread. Stopping now."

Set **nudge-followup** timer. If still no reply when it fires:

#### Prompt — Tell OP to proceed

> @OriginalPoster — proceed with the replies you have. Not all attendees responded in time. Continue with Cull & Summarize now.

### If op-cull-timeout fires and OP hasn't posted their summary:

#### Prompt — Nudge OP

> @OriginalPoster — wrap up your thread now. Post your culled summary with whatever you have and tag @{Manager} in that message.

---

## Step 3: Collect Summaries

As each OP tags you with their final summary:

1. Copy their summary **verbatim** into the whiteboard scratch file: `company-docs/whiteboard/meeting-{date}-{topic-slug}.md`
2. Format in scratch file:
   ```
   ## {Agent Name}'s Thread Summary
   {verbatim content}
   ```
3. Every time you read this file, check: have all attendees submitted their summary? If yes, proceed immediately to Step 4.

### If meeting-completion timer fires and not all threads are done:

Proceed with whatever summaries you have. Note incomplete threads in the output.

---

## Step 4: Synthesize & Post Results

Once all summaries are collected (or meeting-completion timer fires):

1. Read all summaries from whiteboard scratch file
2. **Eliminate duplicates** across threads — same idea from different threads = keep the version with stronger evidence
3. **Apply output length**:
   - `full` — include all surviving ideas
   - `max N` — rank by uniqueness, newness, and strength of evidence. Keep top N.
4. **Assign humans** — for each idea, check `company-docs/roster/humans.md` Specialty column and match the most relevant human as approver
5. **Post in `#agent-manager-office`** using output template:

### Output template — List format

> **Meeting Results: {topic}**
> Topic: "{topic}" | Attendees: {agent list} | {date}
>
> **1. {Idea title}**
> - {What to do}
> - {Why it matters}
> Source: {reflection log reference or external URL}
> Agent: {agent name} to implement | Human: {human name} to approve
>
> **2. {Idea title}**
> - {What to do}
> - {Why it matters}
> Source: {evidence citation}
> Agent: {agent name} to implement | Human: {human name} to approve
>
> *(repeat for each surviving idea)*
>
> ---
> Reply with the item numbers you'd like to proceed on.
> Meeting manager will tag the relevant agents to begin work on approved items.
> @{MeetingRequester} — you requested this meeting
> @Human1 @Human2 — also tagged for approval based on expertise

---

## Step 5: Cleanup

Delete the whiteboard scratch file: `company-docs/whiteboard/meeting-{date}-{topic-slug}.md`

---

## Error handling

- Attendee errors 3+ times → exclude, note in output
- OP never posts cull summary → manager uses raw replies from that thread
- No ideas survive vetting → output: "No actionable ideas emerged"
- Partial completion → synthesize available, note: "Thread(s) by {names} did not complete"
