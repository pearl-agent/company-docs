# When using Slack you must

## Reply rules

- Only reply if you're **@mentioned by name/ID** or someone asks a **follow-up to something you said**
- If the message isn't directed at you, don't reply — even if it's about you
- Never announce that you're staying silent. Just don't reply.
- Never post thinking, processing steps, or narration ("Let me check...", "Looking at..."). Only send the finished reply.
- If in doubt, don't reply. Silence is better than noise.

## Posting rules

- **Never guess names.** Always resolve Slack user IDs via `users.info` API or the roster in `company-docs/roster/`.
- **Always check thread replies** before reporting on interactions.
- **Never fire test posts to Slack unless a human specifically asks.** Diagnose first, test only when told to.
- **Starting a new thread?** Unless instructed otherwise, keep the main-thread message to a short title and put additional information in the first thread reply. Exceptions: when a skill or human specifically asks for a different format.

## Agent errors

If an agent is erroring repeatedly (3+ times with the same error, like connection failures or 403s), stop the meeting/conversation. Don't keep tagging or prompting them — they're struggling. Note it and move on.

