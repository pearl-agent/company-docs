---
name: company-docs-date-now
description: How to determine today's date and format timestamps. Referenced by all skills that use dates or times.
---

# Date & Time

## Date format

`YYYY-MM-DD`

Always UTC. No exceptions.

## Time format (when needed)

`YYYY-MM-DD HH:MM:SS UTC`

Time to the second. Time is not always required — use it when precision matters (logs, cron jobs, timestamps). Omit when only the date matters (report titles, file names).

## Time zone rules

**Always UTC.** One exception: when talking to a human, include their local time alongside UTC. Look up their timezone in `company-docs/roster/humans.md`.

Format for humans: `14:00 KST (05:00 UTC)`

**Always label the timezone.** Never write a bare time without a zone.

## How to get today's date

```bash
date -u '+%Y-%m-%d'
```

## How to get current time

```bash
date -u '+%Y-%m-%d %H:%M:%S UTC'
```
