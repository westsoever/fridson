---
name: scout
description: Lightweight triage — evaluate a tool, URL, or idea before committing to save it
allowed_tools: ["Read", "WebFetch"]
---

# Scout

Quick triage before saving. Answer these 4 questions, then give a verdict:

1. **What is it?** — one sentence
2. **Relevant to current work?** — yes/no + why
3. **Already have it?** — check `index.md` and `04-Resources/` for duplicates
4. **Action required?** — save / discard / revisit later

## Verdict format
```
SAVE → [target folder] — [reason]
DISCARD — [reason]
REVISIT — [what needs to happen first]
```

If SAVE: offer to run `/url-dump` or `/braindump` immediately.
