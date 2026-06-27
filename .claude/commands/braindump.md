---
name: braindump
description: Transform raw thoughts into structured knowledge with domain classification
allowed_tools: ["Read", "Write", "Edit"]
---

# Braindump

When the user gives you a raw dump of thoughts, notes, or ideas:

## Step 1 — Read context
Read `CRITICAL_FACTS.md` and `index.md` if not already loaded.

## Step 2 — Classify domains
Sort the input across these domains (use only what applies):
- **Strategy** — positioning, business model, competitive moves
- **Sales** — prospects, outreach, pipeline moves
- **Automation** — flow ideas, tool notes, client requirements
- **People** — contacts, relationships, observations
- **Learning** — frameworks, articles, ideas worth keeping
- **Operations** — process, admin, logistics

## Step 3 — Extract and file
For each classified item:
- Durable insight → create/update a note in `05-Knowledge/` or `04-Resources/`
- Action → add to the relevant project README in `02-Projects/`
- Person mention → update or create a profile in `05-Knowledge/People/`
- Idea → drop in `00-Inbox/` for later triage

Use the AI-First note format (see `CLAUDE.md`).

## Step 4 — Confirm
List what was created/updated and where. Ask if anything needs deeper development.
