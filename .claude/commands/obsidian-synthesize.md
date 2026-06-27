---
name: obsidian-synthesize
description: Auto-discover cross-note patterns and generate a synthesis page
allowed_tools: ["Read", "Bash", "Write"]
---

# Obsidian Synthesize

Finds connections across notes that haven't been explicitly linked.

## Step 1 — Define scope
Ask the user (or infer from context): what topic, time range, or folder to synthesize?

## Step 2 — Gather notes
```bash
find . -name "*.md" -not -path '*/.obsidian/*' -not -path '*/.claude/*' | xargs grep -l "[topic]" 2>/dev/null
```

Read each matching note.

## Step 3 — Find patterns
Look for:
- Recurring themes across unconnected notes
- Contradictions between notes (especially across time)
- Gaps — things implied but never stated
- Convergence — 3+ notes pointing at the same underlying idea

## Step 4 — Write synthesis
Create `06-Wiki/concepts/[slug].md`:
```markdown
---
synthesized: YYYY-MM-DD
sources: [[note1]], [[note2]], [[note3]]
---

# [Pattern Name]

## For future Claude
[What this synthesis is, what question it answers]

## The Pattern
[Core insight in 2-3 sentences]

## Evidence
- [[note1]] — [what it contributes]
- [[note2]] — [what it contributes]

## Contradictions
[Where sources disagreed — keep them, don't flatten them]

## What this implies
[Actionable takeaway or next question]
```

## Step 5 — Link
Add to relevant Map in `07-Maps/`. Update `index.md`.
