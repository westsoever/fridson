---
name: sideplan
description: Side-mission planner — creates a focused plan file for a bounded task, works it, and removes it when done. Does not touch ACTIVE_PLAN.md.
allowed_tools: ["Read", "Bash", "Write", "Edit"]
---

A side mission is a bounded task that needs its own plan while the main project is still active. It lives in one file (`SIDEPLAN.md`) that is created on first use and deleted on completion.

## Step 1 — Find or create the side mission file

```bash
ls SIDEPLAN.md 2>/dev/null && echo "EXISTS" || echo "MISSING"
```

**If MISSING:** Ask the user: "What's the side mission? Give it a name and a one-line goal." Then create `SIDEPLAN.md` using this structure:

```markdown
# Side Mission: [Name]

**Goal:** [One sentence — what done looks like]
**Scope:** [What's in/out — 2-3 bullets]
**Done when:** [Specific, verifiable exit condition]

---

## Up Next
- [ ] [First task]
- [ ] [Second task]

## In Progress
*(move tasks here while working)*

## Done
*(move tasks here when complete)*

## Blockers
*(anything needing input or waiting on external)*

## Session Log
| Date | Summary |
|------|---------|
```

**If EXISTS:** Read `SIDEPLAN.md` — this is the source of truth for this session.

## Step 2 — Reconcile with reality
Check "In Progress" and "Up Next":
- Anything clearly done since last session → move to "Done"
- New blockers discovered → add to "Blockers"
- Scope creep crept in → move it out to `00-Inbox/` or `ACTIVE_PLAN.md`

## Step 3 — Pick the next task
Take the first unchecked item from "Up Next". Move it to "In Progress". Say which task you're starting.

## Step 4 — Execute
Work the task. Add discovered sub-tasks to "Up Next" immediately. When done, move from "In Progress" to "Done". Loop back to Step 3.

## Step 5 — After each task
Update `SIDEPLAN.md` and append to Session Log before moving on.

## Stopping (mission not yet complete)
Run `/sidewrap` to close the session cleanly.

## Completing the mission
When the "Done when" condition is met:
1. Confirm with the user: "Side mission complete — delete SIDEPLAN.md?"
2. If yes: `rm SIDEPLAN.md`
3. Capture anything worth keeping to the right PARA folder before deleting
4. Return to `/plan` for the main project
