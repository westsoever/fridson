---
name: obsidian-capture
description: Zero-friction idea capture — drop something into Inbox immediately, no filing required
allowed_tools: ["Write"]
---

# Obsidian Capture

Fastest capture in the vault. No classification, no linking.

## What to do
Take whatever the user says and dump it into a timestamped Inbox file:

File: `00-Inbox/[YYYY-MM-DD]-[slug].md`

```markdown
---
captured: YYYY-MM-DD
---

# [Slug / Title]

[Raw content as given — do not interpret, restructure, or summarize]

---
*Process with `/braindump`, `/url-dump`, or `/new-note` when ready*
```

Confirm with: `Captured → 00-Inbox/[filename]`

That's it. Do not file further unless explicitly asked.
