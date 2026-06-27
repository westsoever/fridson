# [Project Name] — Knowledge OS

Personal knowledge base built on PARA + Maps of Content, with AI-first note conventions. Uses Claude Code skills for daily workflow.

---

## Setup

1. Clone this repo and rename the folder to your project name
2. Fill in `SOUL.md` — who you are, values, constraints
3. Fill in `CRITICAL_FACTS.md` — name, company, role, tools, goal
4. Update `CLAUDE.md` title and description
5. Create your first project under `02-Projects/<project-name>/`
6. Update `07-Maps/Home.md` as your entry point

---

## Folder Map

| Folder | What goes here |
|--------|---------------|
| `00-Inbox/` | Raw captures — process weekly, nothing lives here permanently |
| `01-Daily/` | Daily briefs and weekly check-ins |
| `02-Projects/` | Active work with a goal and deadline |
| `03-Areas/` | Ongoing responsibilities — no deadline |
| `04-Resources/` | Reference by topic |
| `05-Knowledge/` | Consolidated frameworks + People CRM |
| `06-Wiki/` | Entities, concepts, decisions |
| `07-Maps/` | Entry points that link everything together |
| `08-Archive/` | Completed or paused — archive, never delete |
| `09-agents/` | Agent configs and automation scripts |

**Start here:** `07-Maps/Home.md`

---

## Skills — All `/commands`

### Session Flow
| Command | What it does |
|---------|-------------|
| `/session-context` | Load vault state at session start |
| `/plan` | Create or continue the active project; pick next task and execute |
| `/wrap-up` | Reconcile state, process Inbox, log session |

### Side Mission
| Command | What it does |
|---------|-------------|
| `/sideplan` | Create or continue a bounded side mission — separate from the main project |
| `/sidewrap` | End a side mission session cleanly |

### Capture
| Command | What it does |
|---------|-------------|
| `/obsidian-capture` | Instant drop to Inbox — no filing, fastest path |
| `/braindump` | Raw thoughts → classified, filed notes |
| `/url-dump` | URL → structured knowledge entry with categorization |
| `/scout` | Triage: save / discard / revisit? |
| `/obsidian-save` | Extract decisions, tasks, people from current conversation |
| `/new-note` | Create a linked permanent note in the right PARA folder |

### Daily Rituals
| Command | What it does |
|---------|-------------|
| `/daily-brief` | Morning priorities + one key action → saved to `01-Daily/` |

### Synthesis & Thinking
| Command | What it does |
|---------|-------------|
| `/knowledge-consolidation` | Merge 3+ loose notes into a reusable framework |
| `/obsidian-synthesize` | Find hidden cross-note patterns, create synthesis page |
| `/obsidian-panel` | 3-4 perspectives debate a decision → synthesized verdict |

### Maintenance
| Command | What it does |
|---------|-------------|
| `/obsidian-health` | Audit: orphans, stale notes, broken links, contradictions |
| `/new-skill` | Create a new skill — write the command file and register it in SKILLS.md |

---

## Key Identity Files

| File | Purpose |
|------|---------|
| `SOUL.md` | Who I am, values, constraints — Claude reads for context |
| `CRITICAL_FACTS.md` | Always-loaded key facts: name, company, tools, goals |
| `index.md` | Vault page catalog — what exists and where |
| `log.md` | Append-only session timeline |

---

## Note Conventions (AI-First)

Every note intended for Claude to reason from uses:
- `## For future Claude` — 2-3 sentences: what this is, why it was saved, when to use it
- Claims stamped: `*(as of YYYY-MM, source.com, confidence: high|medium|low)*`
- `[[wikilinks]]` for internal links · `[text](url)` for external only

Template: `04-Resources/Templates/ai-first-note.md`

---

## Typical Session

```
Morning:   /daily-brief → /plan
Working:   /obsidian-capture  (fast drop)
           /braindump         (after calls or thinking)
           /url-dump          (saving a link)
End:       /obsidian-save → /wrap-up
Side job:  /sideplan → work → /sidewrap → repeat → /sideplan (to close)
Quarterly: /obsidian-health
```

---

## Source Patterns

| Concept | Source |
|---------|--------|
| PARA folder system, Maps of Content | PARA Method (Tiago Forte) + Obsidian community |
| Skills: `/braindump`, `/url-dump`, `/scout`, `/daily-brief`, `/knowledge-consolidation` | [COG Second Brain](https://github.com/huytieu/COG-second-brain) |
| Skills: `/obsidian-save`, `/obsidian-capture`, `/obsidian-health`, `/obsidian-synthesize`, `/obsidian-panel` · AI-first note conventions · `SOUL.md` · `CRITICAL_FACTS.md` | [obsidian-second-brain](https://github.com/eugeniughelbur/obsidian-second-brain) |
| Obsidian Flavored Markdown syntax (wikilinks, embeds, callouts, properties) | [kepano/obsidian-skills](https://github.com/kepano/obsidian-skills) |
