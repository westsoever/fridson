---
name: new-note
description: Create a well-linked permanent note in the correct PARA folder
allowed_tools: ["Read", "Write", "Edit"]
---

When the user asks to create a new note:

## Step 1 — Classify
Ask (or infer from context):
- **Project note** → goes in `02-Projects/[project-name]/`
- **Area note** → goes in `03-Areas/[area]/`
- **Resource/reference** → goes in `04-Resources/[topic]/`
- **Inbox capture** → goes in `00-Inbox/`

## Step 2 — Create the note
Use this template:
```markdown
# [Title]

[1-paragraph summary of the core idea]

## Details
[Body content]

## Related
- [[link to relevant Map]]
- [[link to related notes]]
```

## Step 3 — Link it
- Add a link from the relevant Map in `07-Maps/` to the new note
- If it belongs to a project, link from the project README

## Step 4 — Confirm
Tell the user the file path and which Map was updated.
