---
name: wrap-up
description: End-of-session update — reconcile project state, capture blockers, log the session
allowed_tools: ["Read", "Bash", "Edit", "Write"]
---

Run at end of every session. Takes 2 minutes.

## Step 1 — Audit
```bash
ls 00-Inbox/
ls 02-Projects/
```

For every in-progress item in the active project README:
- Done → tick the checkbox
- Partially done → add a progress note inline
- No longer relevant → move note to `08-Archive/`

## Step 2 — Capture blockers
Add to the project README under a "Blockers" section:
- Needs credential, URL, or decision from user
- Waiting on external event
- Format: `- [ ] 🔑/🌐/❓ **Label** — what's needed`

## Step 3 — Process Inbox
```bash
ls 00-Inbox/
```
For each file in Inbox: file it into the right PARA folder or discard.

## Step 4 — Update Home
Update `07-Maps/Home.md` if any new projects/areas/resources were created this session.

## Step 5 — Session log
Append to `log.md`:
```
| [date] | [2-sentence summary: what moved, what's next] |
```

## Step 6 — Confirm
Print the next 3 unchecked tasks so the user sees what's queued.
