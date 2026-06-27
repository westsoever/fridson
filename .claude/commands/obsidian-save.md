---
name: obsidian-save
description: Extract decisions, tasks, people, and ideas from the current conversation and file them in the vault
allowed_tools: ["Read", "Write", "Edit"]
---

# Obsidian Save

Run after any significant conversation. Scans the conversation and extracts:

## What to extract

| Signal | Destination |
|--------|------------|
| Decision made | `06-Wiki/decisions/[YYYY-MM-DD]-[slug].md` |
| Task or commitment | Active project README checklist |
| Person mentioned (new) | `05-Knowledge/People/[name].md` |
| Insight or learning | `05-Knowledge/` or `04-Resources/` |
| Idea (not ready to act on) | `00-Inbox/idea-[slug].md` |

## Note format for decisions
```markdown
---
date: YYYY-MM-DD
status: decided|reversed|pending
---

# Decision: [Title]

## Context
[Why this decision came up]

## Decision
[What was decided]

## Rationale
[Why this over alternatives]

## For future Claude
[How this affects future work in this vault]
```

## After extracting
- Update `log.md` with a one-line entry
- Update `index.md` if a new significant file was created
- Ask if anything needs deeper development via `/braindump` or `/knowledge-consolidation`
