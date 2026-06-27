# Skills Quick Reference

All skills in `.claude/commands/`. Invoke with `/skillname`.

---

## Session Flow
| Skill | Purpose | When |
|-------|---------|------|
| `/session-context` | Load vault state + active project | Start of every session |
| `/plan` | Create or continue the active project; pick next task and execute | Daily work |
| `/wrap-up` | Reconcile state, process Inbox, log session | End of session |

---

## Side Mission
| Skill | Purpose | When |
|-------|---------|------|
| `/sideplan` | Create or continue a bounded side mission; separate from the main project | When a task needs its own plan without derailing the main project |
| `/sidewrap` | End a side mission session — update SIDEPLAN.md, log, queue next | End of a side mission session |

---

## Capture & Input
| Skill | Purpose | When |
|-------|---------|------|
| `/obsidian-capture` | Zero-friction idea drop into Inbox — no filing required | Any time — fastest capture |
| `/braindump` | Raw thoughts → classified, filed notes | After calls, thinking sessions |
| `/url-dump` | URL → structured knowledge entry with auto-categorization | Saving articles, tools, research |
| `/scout` | Lightweight triage — evaluate a tool, URL, or idea before committing to save | Before committing to save |
| `/obsidian-save` | Extract decisions, tasks, people, and ideas from the current conversation | After significant sessions |

---

## Daily Rituals
| Skill | Purpose | When |
|-------|---------|------|
| `/daily-brief` | Priorities, open loops, one key action → saved to `01-Daily/` | Morning |

---

## Knowledge Building
| Skill | Purpose | When |
|-------|---------|------|
| `/new-note` | Create a well-linked permanent note in the right PARA folder | Capturing a single piece of knowledge |
| `/knowledge-consolidation` | Build a reusable framework from scattered notes | When a topic has 3+ loose notes |
| `/obsidian-synthesize` | Auto-discover cross-note patterns, generate a synthesis page | When looking for hidden connections |

---

## Thinking & Decisions
| Skill | Purpose | When |
|-------|---------|------|
| `/obsidian-panel` | 3-4 perspectives argue a decision independently, then synthesize | Stuck on a decision |

---

## Vault Maintenance
| Skill | Purpose | When |
|-------|---------|------|
| `/obsidian-health` | Audit: orphans, stale notes, broken links, contradictions | Weekly or before major work |
| `/new-skill` | Create a new skill — write the command file and register it here | Adding a new repeatable workflow |

---

## Typical Flows

**Morning:** `/daily-brief` → `/plan`

**Mid-session capture:** `/obsidian-capture` (fast) or `/braindump` (structured)

**End of session:** `/obsidian-save` → `/wrap-up`

**Side mission:** `/sideplan` → work → `/sidewrap` → repeat → `/sideplan` (to close)

**Stuck on a decision:** `/obsidian-panel`

**Saved 3+ notes on same topic:** `/knowledge-consolidation`
