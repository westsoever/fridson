---
name: daily-brief
description: Generate a focused daily brief — priorities, open loops, and one key action
allowed_tools: ["Read", "Bash"]
---

# Daily Brief

## Step 1 — Load state
Read:
- `CRITICAL_FACTS.md`
- Active project README (find it first: `ls 02-Projects/`)
- Yesterday's entry in `log.md` (last row)
- `00-Inbox/` file list

```bash
ls 00-Inbox/
```

## Step 2 — Surface open loops
Identify:
- Unchecked items in the current project phase
- Anything in Inbox not yet filed
- Blockers flagged in the project README

## Step 3 — Generate brief
Output format:
```
## Daily Brief — [date]

**Focus today:** [one sentence — the single thing that moves the needle]

**Open loops:**
- [item] → [where it lives]

**Inbox to process:** [count] items

**Blockers:** [any, or "none"]

**One key action:** [specific, doable today]
```

## Step 4 — Save to vault
Create `01-Daily/[YYYY-MM-DD].md` with the brief content.
