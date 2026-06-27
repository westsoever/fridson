# Fridson AI Issue Reporting + Desktop HMI Analysis

Date: 2026-06-27  
Scope: analysis of what makes a good error/issue reporting interface with AI integration, with specific recommendations for Fridson’s desktop HMI.

## Executive summary

Fridson should not be designed as “a ticket list with an AI panel.” The stronger product pattern is: **low-friction capture for reporters, AI-enriched triage for operators, and a calm desktop command center for facility managers.**

The current draft already has a promising three-column direction: a report list, a main issue workspace, and an “Agent brief” panel. But in its current visible state it feels non-intuitive because the interface starts from an empty “select an issue” state, groups reports by severity, shows repeated/duplicate-looking reports as separate items, and uses the AI area as an empty future promise rather than as an immediate decision aid.

The biggest recommended changes are:

1. **Reframe the desktop screen as a triage inbox / mission control, not a generic report list.** Linear’s Triage model is a strong benchmark: incoming issues land in an inbox where users accept, mark duplicate, decline, snooze, assign, or route before they enter the working backlog[^1](https://linear.app/docs/triage).
2. **Separate three users and workflows:** occupant/reporter, facility manager/operator, technician/vendor. Do not make all users use the same interface.
3. **Make AI a visible co-pilot inside the workflow.** Best-in-class AI products place AI in the workspace context panel, reply editor, triage pane, or issue detail view, not as a separate chat-only destination[^2](https://support.zendesk.com/hc/en-us/articles/5524125586330-About-Zendesk-Copilot)[^3](https://www.intercom.com/blog/announcing-fin-ai-copilot/)[^4](https://support.freshdesk.com/support/solutions/articles/50000010359-overview-of-freddy-ai-for-ticketing)[^5](https://linear.app/docs/triage-intelligence).
4. **Make duplicate detection first-class.** Fridson’s visible list already shows repeated “Pump room · Basement / Leak visible” and repeated printer/out-of-paper reports. These should be clustered into one operational incident with multiple reports, not presented as separate equal tickets.
5. **Use a 3-level consequence-based urgency system.** HSE alarm guidance recommends roughly three priority levels based on consequence if no response occurs, with a target distribution around 5% high, 15% medium, and 80% low[^6](https://www.hse.gov.uk/pubns/chis6.pdf).
6. **Use QR codes as physical context keys.** A QR scan should prefill building, floor, room, asset, default categories, and routing rules. NN/g recommends QR codes have clear context labels and deep-link to relevant actions, not generic homepages[^7](https://www.nngroup.com/articles/qr-code-guidelines/).
7. **Design desktop around decisions:** What needs attention now? Is this duplicate? Who should handle it? What is the evidence? What is the next action?

## What good issue-reporting interfaces do

### 1. They reduce reporting friction without destroying structure

The best systems do not ask users to “write a ticket.” They guide people through a small number of meaningful questions, while mapping answers into structured fields. Linear issue templates, GitHub issue forms, Jira Service Management forms, and Freshdesk ticket forms all use fields, dropdowns, required inputs, placeholders, tooltips, and direct mapping into labels, assignees, priorities, request types, and workflow fields[^8](https://linear.app/docs/issue-templates)[^9](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)[^10](https://support.atlassian.com/jira-service-management-cloud/docs/use-forms-in-jira-service-management/)[^11](https://support.freshdesk.com/support/solutions/articles/50000010095-understand-and-use-ticket-forms).

For Fridson, the reporter flow should be closer to:

1. Scan QR.
2. Location is already known.
3. Add photo.
4. Choose or type what is wrong.
5. Answer one safety question: “Is anyone in danger or is damage spreading?”
6. Submit.

The facility manager can later see the structured fields: category, asset, urgency, duplicate match, assignee, SLA, vendor, and status.

### 2. They use a triage buffer before work enters the main backlog

A common mistake is making every report immediately equal to a task. Linear explicitly uses Triage as an inbox/holding area for issues from integrations, outside team members, or forms; users can accept, mark duplicate, decline, or snooze before the issue becomes normal backlog work[^1](https://linear.app/docs/triage). Sentry similarly separates issue states such as For Review, Unresolved, Resolved, Archived, Escalating, and Regressed to focus attention[^12](https://docs.sentry.io/product/issues/states-triage/).

Fridson should adopt a desktop default of **“Needs decision”** rather than **“All reports.”**

Recommended triage queue states:

- New / unacknowledged
- Possible duplicate
- Needs information
- Accepted / routed
- In progress
- Waiting vendor
- Scheduled
- Snoozed
- Resolved
- Declined / not actionable

### 3. They capture evidence at the moment of reporting

Facility issues are often visual. Best-in-class bug and field-maintenance tools capture evidence automatically or visually: Marker.io captures screenshots and technical context; Usersnap captures screenshots, recordings, console logs, and metadata; MaintainX supports photos and annotations on work orders; Snapfix supports photo, video, voice, and QR-based issue creation[^13](https://help.marker.io/en/articles/5546520-how-to-integrate-marker-io-into-your-web-app)[^14](https://help.usersnap.com/docs/copy-of-usersnap-for-product-managers)[^15](https://www.getmaintainx.com/use-cases/work-order-management)[^16](https://snapfix.com/fix).

For Fridson, the issue photo should be central in the desktop detail view, not buried as an attachment.

### 4. They prevent duplicates and cluster repeated reports

Duplicate defense is a major quality-of-life feature. Linear lets triagers mark duplicates and move attachments/customer requests to the canonical issue[^1](https://linear.app/docs/triage). Sentry groups repeated events into issues using fingerprints, stack traces, exceptions, and messages[^17](https://docs.sentry.io/concepts/data-management/event-grouping/). MaintainX’s QR maintenance flow can show existing open work orders after a scan before a user creates another one[^18](https://www.getmaintainx.com/blog/using-qr-codes-in-maintenance).

Fridson should show:

- “Same asset/location, same issue category, same day”
- “Multiple reports attached to this incident”
- “Open issue already exists”
- “Create new / link / merge / mark related”

### 5. They close the loop with the reporter

Good reporting interfaces do not make the reporter wonder if anything happened. Marker.io supports two-way sync and status communication with issue trackers; UpKeep supports free requesters who can submit and track work requests; Snapfix supports QR task tracking links for monitoring status[^13](https://help.marker.io/en/articles/5546520-how-to-integrate-marker-io-into-your-web-app)[^19](https://upkeep.com/qr-codes/)[^20](https://support.snapfix.com/knowledge/how-can-i-use-qr-codes-in-snapfix).

For Fridson, after submission:

- Show issue ID.
- Show expected next step.
- Offer optional email/SMS/magic-link updates.
- Let the reporter add one missing detail later without logging in.

## What good AI integration looks like

### 1. AI should be in context, not a separate destination

Zendesk Copilot appears inside the agent workspace and editor with ticket summaries, sentiment, intent, suggested replies, merge suggestions, and review-and-approve flows[^2](https://support.zendesk.com/hc/en-us/articles/5524125586330-About-Zendesk-Copilot). Intercom Fin Copilot sits inside the inbox and shows source links so agents can validate generated answers[^3](https://www.intercom.com/blog/announcing-fin-ai-copilot/). Freshdesk Freddy appears across the ticket list, ticket detail, and reply editor with summaries, writing assistance, sentiment, auto triage, and similar-ticket suggestions[^4](https://support.freshdesk.com/support/solutions/articles/50000010359-overview-of-freddy-ai-for-ticketing). Linear puts Triage Intelligence directly under the issue title with suggested labels, assignees, teams, estimates, and duplicates[^5](https://linear.app/docs/triage-intelligence).

For Fridson, the “Agent brief” panel should become an **AI Decision Panel**. It should not be empty until the user does something. When no issue is selected, it should explain what AI will do and show queue-level insights, such as duplicate clusters and urgent items.

### 2. AI should suggest, explain, and prefill — humans approve important actions

Strong AI interfaces preserve user control. Linear gives explicit triage actions: accept, duplicate, decline, snooze[^1](https://linear.app/docs/triage). Freshdesk supports manual and automatic triage modes and treats overwritten suggestions as feedback[^21](https://support.freshdesk.com/en/support/solutions/articles/50000002117). ServiceNow Now Assist generates incident summaries and resolution notes, but agents review and submit the notes[^22](https://www.servicenow.com/content/dam/servicenow-assets/public/en-us/doc-type/resource-center/data-sheet/ds-now-assist-for-itsm.pdf). Sentry Seer separates diagnosis from higher-risk actions such as PR generation and allows organization/project/repository toggles[^23](https://docs.sentry.io/product/ai-in-sentry/seer/).

Fridson AI states should be explicit:

- Suggested
- Applied by user
- Auto-applied by rule
- Rejected / overridden

### 3. AI needs transparency: reason, evidence, confidence, and source

Intercom Fin Copilot shows source links and previews in the inbox[^3](https://www.intercom.com/blog/announcing-fin-ai-copilot/). Linear Triage Intelligence provides reasoning/details for suggestions[^5](https://linear.app/docs/triage-intelligence). Freshdesk Similar Tickets shows confidence score, agent/group/date, CSAT, and a link to historical tickets[^24](https://crmsupport.freshworks.com/support/solutions/articles/50000011659-similar-tickets-in-freshdesk). Sentry Seer can show reasoning/evidence during investigation[^23](https://docs.sentry.io/product/ai-in-sentry/seer/).

Fridson should avoid black-box labels like “High severity.” Use reasoning:

> Urgency 3 because: active leak + basement mechanical room + previous open report within 1 hour + photo shows water on floor.

### 4. AI should support structured summaries for each stage

Freshdesk summaries are structured into Issue, Steps Taken, and Outcome[^25](https://support.freshdesk.com/support/solutions/articles/50000006257-summarize-automate-ticket-summaries-for-efficient-collaboration). ServiceNow’s Now Assist summary UI uses Issue and Actions Taken bullets and can share content into work notes[^22](https://www.servicenow.com/content/dam/servicenow-assets/public/en-us/doc-type/resource-center/data-sheet/ds-now-assist-for-itsm.pdf). Jira summaries are on-demand, private, and transient when summarizing issue comments[^26](https://support.atlassian.com/jira-service-management-cloud/docs/summarize-an-issues-comments-using-atlassian-intelligence/).

Fridson should use different AI summaries for different moments:

- **Pre-submit:** What I understood, missing details, suggested route.
- **Triage:** Issue, evidence, impact, duplicate risk, recommended action.
- **Handoff:** Technician/vendor-ready work order.
- **Resolution:** Cause, fix performed, outcome, prevention suggestion.

## Current Fridson draft: what feels difficult

Based on the visible draft snapshot, Fridson currently shows:

- Header: “Fridson · Issue workspace” with “13 reports · live.”
- Top navigation to Assets and QR Stickers.
- Left sidebar grouped by Severity, with High, Medium, Low, and Unscored.
- Repeated reports such as “Pump room · Basement / Leak visible” and multiple printer/out-of-paper issues.
- Empty center panel: “Select an issue.”
- Empty right panel: “Agent brief.”

### Main issues

#### 1. The default screen does not answer “what should I do now?”

Grouping by severity is useful, but the operator’s real first question is usually: **Which items need a human decision right now?**

Severity grouping mixes status and work stage. For example, a high-severity issue marked “failed” may need different action than a high-severity issue that is new and unacknowledged. A medium issue marked “done” should not compete with new medium issues.

Better default grouping:

1. New unacknowledged
2. Urgency 3 / immediate
3. Possible duplicates
4. Needs info
5. SLA risk / due soon
6. Waiting vendor
7. Done / closed

#### 2. Duplicate-looking items are not clustered

The left list shows repeated issues by same location and category. This creates cognitive load and makes the user manually infer what the system should know.

Fridson should show:

- “Pump room leak visible — 2 reports — first seen 16:29 — latest 17:20 — high urgency”
- Open canonical issue with attached reporter events underneath.

#### 3. The AI panel is not doing visible work

An empty “Agent brief” panel tells the user AI exists, but it does not reduce workload. The AI panel should immediately explain:

- What it can do.
- What it has already detected.
- What action is recommended next.

Empty state idea:

> AI has found 3 possible duplicate clusters, 2 reports needing location confirmation, and 1 high-urgency issue not yet acknowledged.

#### 4. The interface lacks a visible workflow model

The badges “Failed,” “Done,” and “Awaiting” are ambiguous. Failed what? Failed AI refinement? Failed resolution? Failed reporter submission? Failed work order?

Use separate concepts:

- **Report intake status:** New, Needs info, Accepted, Declined.
- **Work status:** Assigned, In progress, Waiting vendor, Scheduled, Resolved.
- **Automation status:** AI suggested, AI failed, AI applied, AI skipped.
- **Reporter status:** Notified, awaiting reply, no contact.

#### 5. The center panel should not be empty real estate

When no issue is selected, the center should show a mission-control dashboard or focused queue summary. Empty states are useful only when they teach the next action.

## Recommended desktop HMI architecture

### Mode 1: Mission Control Dashboard

Purpose: facility manager overview.

Should answer:

1. What needs attention now?
2. What is unacknowledged?
3. What is about to breach SLA?
4. What is repeating?
5. What is blocked?

Recommended layout:

- Top KPI strip: Urgency 3 open, New unacknowledged, SLA breach/due today, Duplicate clusters, Waiting vendor.
- Main queue: decision-first work list.
- Right insight rail: AI-detected clusters, risky assets, suggested follow-ups.
- Drilldown: site → building → floor/area → asset → issue.

HMI support: Rockwell’s Process HMI Style Guide recommends progressive disclosure, display hierarchy, matching user goals/tasks/mental models, avoiding clutter, and reserving bright colors for alarms[^27](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

### Mode 2: Triage Inbox

Purpose: process incoming reports quickly.

Columns / row fields:

- Urgency
- Report summary
- Location / asset
- AI category
- Reporter / source
- Created age
- SLA
- Assigned team/vendor
- Status
- Duplicate count

Actions:

- Acknowledge
- Accept
- Merge
- Link related
- Route
- Ask for info
- Snooze
- Resolve
- Decline

Power-user features:

- Keyboard shortcuts.
- Bulk actions.
- Saved views.
- Filters by site, category, assignee, SLA, status.
- “Only needs decision” toggle.

### Mode 3: Issue Decision Panel

Purpose: select one report/incident and decide what happens.

Three-column detail view:

**Left: original evidence**
- Reporter quote.
- Photos/videos.
- QR tag, location, asset.
- Reporter/contact/channel.

**Center: work order / decision form**
- Editable issue title.
- Category/trade.
- Urgency.
- Assignee/vendor.
- SLA/due date.
- Status.
- Comments.

**Right: AI Decision Panel**
- AI interpretation.
- Reasoning.
- Duplicate/related issues.
- Similar history.
- Suggested next action.
- Missing info prompt.
- Rule/AI/audit trail.

### Mode 4: Asset / Location History

Purpose: see recurrence and prevent repeat failures.

Should include:

- All issues tied to asset/location.
- Recurring categories.
- Vendor history.
- Mean time to resolution.
- Previous fixes.
- QR tag metadata.
- Preventive maintenance suggestions.

### Mode 5: QR Sticker Management

Purpose: manage physical-to-digital context.

Each QR tag should map to:

- Site
- Building
- Floor
- Area/room
- Asset
- Default issue categories
- Default routing/vendor rules
- Label text
- Fallback URL/code
- Status: active/replaced/retired

NN/g notes QR codes need clear information scent and should link to context-specific destinations rather than generic pages[^7](https://www.nngroup.com/articles/qr-code-guidelines/). Fiix describes QR codes as a bridge from physical assets/spaces into CMMS maintenance pages, reducing phone/email/sticky-note transcription[^28](https://fiixsoftware.com/blog/why-you-should-be-using-qr-codes-for-facility-management/).

## Recommended AI feature set

### 1. AI interpretation card

Shows:

- “What happened” summary.
- Category/trade.
- Impact.
- Evidence used.
- Missing details.
- Confidence.

Actions:

- Apply summary.
- Edit.
- Regenerate.
- Mark incorrect.

### 2. Severity/routing card

Shows:

- Suggested urgency 1/2/3.
- Rule vs AI source.
- Reasoning bullets.
- Suggested owner/vendor.
- SLA implication.

Actions:

- Apply urgency.
- Override with reason.
- Route.
- Escalate.

### 3. Duplicate cluster card

Shows:

- Existing issue match.
- Similarity/confidence.
- Matching reason.
- Existing status/owner/age.
- Number of linked reports.

Actions:

- Merge.
- Link as related.
- Keep separate.
- Ignore suggestion.

### 4. Missing information card

Shows:

- “Need photo?”
- “Need exact room?”
- “Need access instructions?”
- “Need permission to enter?”

Actions:

- Ask reporter one-click.
- Use template question.
- Mark not needed.

### 5. Resolution note card

At close, AI drafts:

- Cause.
- Action taken.
- Vendor/technician.
- Parts/time.
- Outcome.
- Prevention suggestion.

Human reviews before saving or notifying reporter, following ServiceNow’s review-and-submit pattern for generated resolution notes[^22](https://www.servicenow.com/content/dam/servicenow-assets/public/en-us/doc-type/resource-center/data-sheet/ds-now-assist-for-itsm.pdf).

## Urgency model for Fridson

Use three internal levels, not many ambiguous severities.

### Urgency 3: Immediate

Criteria:

- Safety/security risk.
- Active water leak or spreading damage.
- Electrical/fire/regulatory issue.
- Locked/access blocked where critical.
- Multiple reports in short window.
- Critical asset down.

Default actions:

- Require acknowledgement.
- Notify responsible person/vendor.
- Start SLA timer.
- Show in top dashboard.

### Urgency 2: Soon

Criteria:

- Comfort/service degradation.
- Broken appliance/equipment with operational impact.
- Issue likely to worsen.
- Repeated but not dangerous issue.

Default actions:

- Assign/schedule.
- Track SLA.
- Batch updates where possible.

### Urgency 1: Routine

Criteria:

- Cosmetic issue.
- Cleaning/restock if not urgent.
- Minor inconvenience.
- Improvement request.

Default actions:

- Queue for planned work.
- Digest notifications.
- No alarm-style alert.

HSE’s alarm guidance supports consequence-based prioritization and roughly three levels, rather than overusing high-priority alerts[^6](https://www.hse.gov.uk/pubns/chis6.pdf).

## Form and reporting UX recommendations

### Reporter / QR form

Do:

- One job per screen.
- Large buttons.
- Location prefilled.
- Photo-first option.
- Simple category chips.
- Optional text.
- Safety gate.
- Confirmation page.

Avoid:

- Asking user to choose building/floor/asset if QR knows it.
- Asking user to estimate technical severity.
- Login walls for guests or non-technical staff.
- Long multi-field admin forms.

GOV.UK advises teams to know why each question is being asked and ask only for information really needed[^29](https://design-system.service.gov.uk/patterns/question-pages/). NN/g recommends logical grouping, familiar UI patterns, reduced clutter, transparency, and support to reduce cognitive load[^30](https://www.nngroup.com/articles/4-principles-reduce-cognitive-load/).

### Desktop operator form

Do:

- Use compact panels for trained users.
- Show structured fields with AI suggestions.
- Keep evidence visible while editing.
- Preserve queue context when opening issue detail.
- Provide keyboard shortcuts and bulk actions.

Avoid:

- Full-page modal forms that hide the queue.
- Separate AI chat that loses issue context.
- Hiding reasoning behind badges.
- Mixing intake, work, and automation statuses into one label.

### Error/validation handling

Validation should tell users what went wrong and how to fix it, preserve entered data, show an error summary, and place inline errors next to fields[^31](https://design-system.service.gov.uk/patterns/validation/).

For Fridson:

- “Choose a room/area so we can route this correctly.”
- “Add a photo or confirm no photo is available.”
- “This looks like a duplicate. Choose merge, link, or create new.”

## Visual design and HMI principles

### Color discipline

Do not make everything colorful. Use calm neutrals for normal state and reserve red/orange for abnormal conditions requiring action. Rockwell’s HMI guide recommends muted non-data pixels and bright/intense colors only for alarms, with color paired with shape/icon/text rather than being the only signal[^27](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

### Progressive disclosure

Adopt four levels:

1. Overview / mission control.
2. Operating queue / triage inbox.
3. Issue decision detail.
4. Asset/location diagnostics.

Rockwell describes HMI hierarchy using overview, operating, detail, and support levels to support progressive disclosure[^27](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

### Response feedback

Show immediate feedback for every action:

- Acknowledged.
- Assigned.
- Routed.
- Reporter asked.
- Merged.
- Resolved.

Rockwell gives HMI response-time expectations: Level 2/3 displays under 2 seconds, Level 1/4 under 5 seconds, and user entry feedback within 0.5–2 seconds[^27](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

## Specific changes to make now

### High-impact UX fixes

1. Replace default “Severity” grouping with “Needs decision” or “Triage inbox.”
2. Add duplicate clustering for repeated location/category/time-window reports.
3. Rename ambiguous statuses:
   - “Failed” → specify failed what: “AI failed,” “Work failed,” “Resolution failed,” etc.
   - “Awaiting” → “Awaiting assignment,” “Awaiting vendor,” or “Awaiting reporter.”
4. Make the empty center panel useful: show mission-control summary when no issue is selected.
5. Make the AI panel useful when no issue is selected: show queue insights and next recommended action.
6. Add acknowledgement state for high-urgency unacknowledged reports.
7. Add “merge/link/create new” controls for suspected duplicates.
8. Use urgency 1/2/3 with visible reasoning instead of broad severity groups alone.
9. Add SLA/age indicators to the list.
10. Show photo/evidence thumbnail in each row if available.

### Desktop layout change

Recommended default desktop layout:

- **Left rail:** queue categories and saved views.
- **Center list:** actionable triage queue.
- **Right detail:** selected issue with AI decision panel.

Alternative if keeping current three columns:

- Left column: queue filters and grouped report list.
- Center column: selected issue evidence + editable work fields.
- Right column: AI decision panel + actions.

### Copy changes

Current: “Pick a report on the left to start refining it with the AI.”

Better:

> Select a report to classify, merge, route, or resolve. AI will suggest urgency, category, duplicates, and next action — you stay in control.

Current: “The research brief and approve action will appear here.”

Better:

> AI Decision Panel: shows summary, severity reason, duplicate matches, suggested route, and missing information.

## Suggested implementation roadmap

### Phase 1: Make current interface understandable

- Rename statuses.
- Add queue-based grouping.
- Add useful empty states.
- Add issue detail view with evidence, fields, and action buttons.
- Add duplicate cluster detection by simple rules: same location + category + active status + time window.

### Phase 2: Add AI-assisted triage

- AI summary.
- AI category/urgency suggestion.
- AI duplicate match.
- AI missing-info prompt.
- AI routing suggestion.
- Human apply/override buttons.
- Audit trail for accepted/rejected AI suggestions.

### Phase 3: Build QR-to-desktop continuity

- QR tag records mapped to location/asset.
- Reporter QR landing page.
- Confirmation/status page.
- Reporter follow-up magic link.
- Desktop view showing QR source context.

### Phase 4: Add operational dashboard

- Mission control overview.
- SLA risk.
- Repeated asset/location clusters.
- Vendor waiting.
- Category/site trends.
- Multi-site hierarchy.

### Phase 5: Add safer automation

- Auto-fill low-risk fields.
- Auto-route low-risk routine issues.
- Require approval for high-risk actions: merge, close, vendor dispatch, external messages.
- Admin settings: Off / Suggest / Auto-fill / Auto-route by category/site/team.

## Bottom line

Fridson’s opportunity is to become a **human-factors operating layer for buildings**, not just another issue tracker. The winning shape is:

- **Reporter mode:** QR, photo, 1–2 taps, no login.
- **Operator mode:** triage inbox, AI reasoning, duplicate clustering, routing, SLA/status, evidence-rich desktop decision panel.
- **Technician/vendor mode:** clear work order, evidence, access instructions, status updates.
- **Manager mode:** mission control, repeated issue insights, asset/location trends, vendor performance.

The current draft has the beginnings of this with the report list + workspace + agent panel. The next step is to make the workflow explicit, make AI visible and explainable, and make the desktop interface answer: **what needs my attention, why, and what should I do next?**

## Research notes and caveats

- I inspected the visible Fridson draft read-only. I did not click through individual issue details or mutate the app.
- Some HMI standards are not fully public. I used public standards summaries, HSE guidance, EEMUA/ISA summaries, Rockwell’s public Process HMI Style Guide, NN/g, GOV.UK, and vendor documentation as accessible sources.
- CMMS case studies from vendors such as MaintainX should be treated as directional product evidence, not independent proof.
- AI product interfaces evolve quickly; product documentation was used for current patterns where possible.
