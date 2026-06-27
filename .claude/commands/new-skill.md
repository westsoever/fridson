---
name: new-skill
description: Create a new skill — write the command file and register it in SKILLS.md
allowed_tools: ["Read", "Write", "Edit", "Bash"]
---

Use this when you want to add a new repeatable workflow to the vault.

## Step 1 — Gather requirements
Ask the user (or infer from context):
1. **Name** — the `/command-name` (lowercase, hyphenated)
2. **Description** — one line, shown in SKILLS.md and the frontmatter
3. **Purpose** — what does this skill do? When should it be used?
4. **Steps** — what are the 3-6 steps the skill follows?
5. **Tools needed** — which of: `Read`, `Write`, `Edit`, `Bash`, `WebSearch`, `WebFetch`
6. **Category** — which section of SKILLS.md it belongs to:
   - Session Flow
   - Side Mission
   - Capture & Input
   - Daily Rituals
   - Knowledge Building
   - Thinking & Decisions
   - Vault Maintenance
   - *(or propose a new section)*

## Step 2 — Write the command file
Create `.claude/commands/<name>.md`:

```markdown
---
name: <name>
description: <description>
allowed_tools: [<tools>]
---

<Purpose paragraph — what this does and when to use it.>

## Step 1 — ...
[steps]
```

## Step 3 — Register in SKILLS.md
Read `.claude/SKILLS.md`. Add a row to the correct section table:
```
| `/<name>` | <description> | <when to use> |
```

If the category doesn't exist yet, add a new `## <Category>` section with a table header before appending the row.

## Step 4 — Confirm
Tell the user:
- File created: `.claude/commands/<name>.md`
- Registered in: `.claude/SKILLS.md` under `<Category>`
- Invoke with: `/<name>`
