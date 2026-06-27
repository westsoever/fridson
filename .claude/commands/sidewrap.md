---
name: sidewrap
description: End-of-session update for the active side mission — reconcile SIDEPLAN.md, log what happened, set up next session. Sibling of /wrap-up.
allowed_tools: ["Read", "Bash", "Edit", "Write"]
---

Closes a side mission session. Operates on `SIDEPLAN.md` only — never touches `ACTIVE_PLAN.md`.

## Step 1 — Audit completed work
Read `SIDEPLAN.md`. For every item in "In Progress":
- Done → move to "Done"
- Partially done → keep in "In Progress", add a note on what's left
- No longer in scope → remove, park in `00-Inbox/` or `ACTIVE_PLAN.md`

## Step 2 — Capture blockers
Add anything to "Blockers" that:
- Requires a credential, URL, or decision from the user
- Is waiting on an external event
- Could not be completed without human action

Format: `- [ ] 🔑/🌐/❓ **Short label** — what exactly is needed`

## Step 3 — Sharpen the plan
Look at "Up Next" with fresh eyes:
- Reorder by what unblocks the mission fastest
- Add tasks discovered this session
- Remove tasks that are no longer needed
- Anything that's scope creep → move it out

## Step 4 — Add session log entry
Append to the Session Log table in `SIDEPLAN.md`:
```
| [date] | [2-sentence summary: what was done, what's next] |
```

## Step 5 — Check for completion
Does the current "Done" list satisfy the "Done when" condition?
- **Yes** → tell the user the mission is complete and suggest running `/sideplan` to finalize and delete `SIDEPLAN.md`
- **No** → print the "Up Next" list so the next session starts instantly
