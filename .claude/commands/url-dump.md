---
name: url-dump
description: Convert a URL into a structured knowledge entry with auto-categorization
allowed_tools: ["Read", "Write", "WebFetch"]
---

# URL Dump

When the user provides one or more URLs:

## Step 1 — Fetch and clean
Fetch the URL content. Extract: title, key claims, date, source domain.

## Step 2 — Categorize
Determine the best PARA folder:
- Tool / service reference → `04-Resources/Tools/`
- Market research / niche insight → `04-Resources/Market-Research/`
- Automation pattern → `04-Resources/Automation/`
- Competitor / prospect → `04-Resources/Clients/` or `05-Knowledge/`
- Framework / concept → `06-Wiki/concepts/`

## Step 3 — Write note
Create the note with AI-First format:
```markdown
---
source: [url]
saved: YYYY-MM-DD
tags: [relevant tags]
---

# [Title]

## For future Claude
[2-3 sentences: what this is, why it was saved, how to use it]

## Key Points
- [Claim] *(as of YYYY-MM, [source.com], confidence: high|medium|low)*

## Open Questions
- [What's unclear or needs follow-up]
```

## Step 4 — Link
Add link from the relevant Map in `07-Maps/` or `index.md`.

## Step 5 — Confirm
State the file path and any follow-up actions.
