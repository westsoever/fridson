---
name: plan
description: Load the active project, reconcile with reality, pick next task and execute. Creates the project on first use.
allowed_tools: ["Read", "Bash", "Write", "Edit"]
---

## Step 1 — Find or create the active project

```bash
ls 02-Projects/ 2>/dev/null
```

**If no projects exist (or user is starting a new one):** Ask:
1. "What's the project name?" (used as the folder name, e.g. `client-onboarding`)
2. "What's the goal in one sentence?"
3. "What's the deadline or timeframe?"

Then create `02-Projects/<name>/` and `02-Projects/<name>/ACTIVE_PLAN.md` using this structure:

```markdown
# [Project Name]

**Goal:** [One sentence — what done looks like]
**Deadline:** [Date or timeframe]
**Owner:** [You]

---

## Session Protocol
- 🤖 Claude can do autonomously
- 🤝 Claude drafts, human reviews
- 🧑 Human-only action required
- Never skip a GATE — these are explicit checkpoints requiring sign-off

## Human-Action Queue
*(tasks Claude can't do — needs you)*

---

## Phase 1 — [Phase name]
- [ ] 🤖 ▶ NEXT [First task]
- [ ] 🤖 [Second task]
- [ ] 🧑 GATE: [Checkpoint description]

## Phase 2 — [Phase name]
- [ ] 🤖 [Task]

---

## Blockers
*(anything waiting on input, credentials, or external events)*

## Status Log
| Date | Summary |
|------|---------|
| [today] | Project created |
```

Also create `02-Projects/<name>/README.md` with the project name and a link to `ACTIVE_PLAN.md`.

Update `index.md` to add the new project to the Active Projects table.

**If one project exists:** Read its `ACTIVE_PLAN.md` directly.

**If multiple projects exist:** Ask which one to work on.

---

## Step 2 — Reconcile with reality
Check `## Blockers` first — anything resolved? Then verify:
```bash
ls 02-Projects/<active-project>/
```

Cross-reference against ACTIVE_PLAN.md checkboxes:
- Items clearly done → tick them off
- New blockers → add to `## Blockers`
- Order still optimal? → reorder if needed, never skip a GATE

## Step 3 — Pick the next task
Go to the `▶ NEXT` marker. If the task is 🧑, prepare everything Claude can, add it to the Human-Action Queue, and move `▶ NEXT` to the next non-blocked task. Say which task you're starting.

## Step 4 — Execute
Work the task. Add discovered sub-tasks to ACTIVE_PLAN.md immediately. When done, tick the checkbox and move `▶ NEXT`.

## Step 5 — After each task
Append to `## Status Log` (date + one line). Loop to Step 3 until stopping.

## Completing the project
When the project goal is met:
1. Confirm with the user: "Project complete — archive it?"
2. If yes: move `02-Projects/<name>/` to `08-Archive/<name>/`
3. Remove it from `index.md` Active Projects table
4. Return: "Project archived. Run `/plan` to start a new one."

## Stopping (project not yet complete)
Run `/wrap-up` before ending.
