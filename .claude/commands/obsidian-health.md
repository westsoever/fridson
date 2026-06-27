---
name: obsidian-health
description: Vault audit — find contradictions, orphaned notes, stale claims, and gaps
allowed_tools: ["Read", "Bash"]
---

# Vault Health

Full audit. Takes 2-3 minutes. Run weekly or before major decisions.

## Step 1 — Orphaned notes
```bash
find . -name "*.md" -not -path '*/.obsidian/*' -not -path '*/.claude/*' | sort
```
Flag any notes not linked from any Map or index.

## Step 2 — Inbox age
```bash
ls -lt 00-Inbox/
```
Flag anything older than 7 days still in Inbox.

## Step 3 — Stale project status
Read each project README in `02-Projects/`. Flag:
- Projects with no update in >14 days
- Projects with all tasks checked but not archived

## Step 4 — Contradiction scan
Read `CRITICAL_FACTS.md` and `SOUL.md`. Cross-check against notes in `03-Areas/Company/` and `06-Wiki/decisions/`. Flag any conflicts.

## Step 5 — Gap analysis
Check `07-Maps/` — are all linked notes actually created? List any `[[broken links]]`.

## Step 6 — Report
Output:
```
## Health Report — [date]

**Orphaned notes:** [list or "none"]
**Inbox backlog:** [count] items, oldest: [date]
**Stale projects:** [list or "none"]
**Contradictions:** [list or "none"]
**Broken links:** [list or "none"]

**Action queue:**
- [ ] [specific fix needed]
```
