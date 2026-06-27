---
name: knowledge-consolidation
description: Build a reusable framework or reference from scattered braindumps, notes, and insights
allowed_tools: ["Read", "Bash", "Write"]
---

# Knowledge Consolidation

Use when you have enough scattered notes on a topic to warrant a proper synthesis.

## Step 1 — Gather source notes
Identify all relevant notes on the target topic:
```bash
grep -rl "[topic keyword]" 00-Inbox/ 04-Resources/ 06-Wiki/ 05-Knowledge/ 2>/dev/null
```

Read each source note.

## Step 2 — Extract claims
Pull out every distinct claim, observation, or pattern. Flag:
- Contradictions between notes
- Claims with low confidence
- Gaps — what's missing to make this complete?

## Step 3 — Build the framework
Synthesize into a structured reference note:
```markdown
---
consolidated: YYYY-MM-DD
sources: [[note1]], [[note2]]
confidence: high|medium|low
---

# [Framework / Topic Name]

## For future Claude
[What this framework is and when to use it]

## Core Pattern
[The central insight in 2-3 sentences]

## Components
[Structured breakdown]

## Contradictions & Caveats
[Where sources disagreed, with citations]

## Open Questions
[What's still unknown]
```

## Step 4 — File and link
Save to `05-Knowledge/` or `04-Resources/` depending on type. Link from the relevant Map.

## Step 5 — Prune
Offer to archive the source scraps in `08-Archive/` now that they're consolidated.
