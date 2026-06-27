---
name: session-context
description: Load full vault context at the start of a new session
allowed_tools: ["Read", "Bash"]
---

Read these in order, then confirm ready with one line:

1. Read `CLAUDE.md` — vault map and hard rules
2. Read `07-Maps/Home.md` — current active projects and areas
3. Find and read the active project README:
```bash
ls 02-Projects/
```

After reading, respond with exactly:
> Context loaded. Active project: [name]. Top priority: [one next action].

Do not summarize what you read. Just confirm and state the next action.
