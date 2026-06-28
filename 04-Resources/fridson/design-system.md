# Fridson Design System

Use this file as the design-system and product-interface guidance for building Fridson: an AI-assisted facility issue reporting and triage system.

## 1. Design system recommendation

### Implementation base

Use:

- **shadcn/ui** for React component patterns.
- **Radix UI** for accessible primitives.
- **Tailwind CSS** for styling, spacing, layout, and design tokens.
- **TanStack Table** for the desktop triage inbox and data-heavy views.

Do not use Material Design as the main visual base. Fridson should not feel like a generic consumer/mobile dashboard. It should feel like a calm, precise desktop operations console.

### Reference systems

Use these systems as inspiration:

1. **Linear** — primary workflow reference for triage, speed, density, keyboard-first actions, duplicate handling, and low-noise issue management.
2. **IBM Carbon** — reference for enterprise-grade tables, forms, status indicators, data density, and visual restraint.
3. **GOV.UK Design System** — reference for reporter-facing forms, validation, accessibility, and plain-language question flows.
4. **High-performance HMI principles** — reference for command-center behavior, urgency discipline, progressive disclosure, and color restraint.

Target combination:

> Linear’s speed + Carbon’s enterprise restraint + GOV.UK’s clarity + high-performance HMI alarm discipline.

## 2. Product personality

Fridson should feel:

- Calm
- Operational
- Fast
- Trustworthy
- Evidence-led
- Minimal but not empty
- AI-assisted but human-controlled
- Designed for desktop triage, not casual browsing

Avoid:

- Generic SaaS dashboard feel
- Colorful toy-like cards
- Overuse of gradients
- AI chat as the main interface
- Ambiguous status labels
- Large empty panels with no operational value
- Making every report look equally urgent

## 3. Core interface model

Fridson has four primary user modes.

### 3.1 Reporter mode

For occupants, guests, staff, or tenants submitting an issue.

Primary device: mobile via QR code.

Goal: submit a useful report in under 30 seconds.

Flow:

1. Scan QR code.
2. Location is prefilled.
3. Add photo or video.
4. Choose issue type or write short description.
5. Answer safety gate: “Is anyone in danger or is damage spreading?”
6. Submit.
7. Receive confirmation/status link.

Do not require login unless absolutely necessary.

### 3.2 Operator mode

For facility managers or admins triaging incoming reports.

Primary device: desktop.

Goal: decide what happens next.

Core tasks:

- Acknowledge urgent reports.
- Accept valid reports.
- Merge duplicates.
- Route to team/vendor.
- Ask reporter for missing information.
- Snooze/schedule non-urgent work.
- Resolve or decline.

### 3.3 Technician/vendor mode

For people executing the work.

Goal: understand the job quickly and update status.

Needs:

- Work order summary.
- Location/asset.
- Photos/evidence.
- Access instructions.
- Priority/SLA.
- Comments.
- Status update controls.

### 3.4 Manager mode

For portfolio/site oversight.

Goal: see risk, recurrence, and performance.

Needs:

- Mission control dashboard.
- Urgent open issues.
- SLA breaches.
- Repeated issue clusters.
- Vendor waiting states.
- Asset/location trends.
- Site/category comparisons.

## 4. Primary desktop screens

### 4.1 Mission Control Dashboard

Purpose: answer “what needs attention now?”

Use this as the default desktop homepage when no specific issue is selected.

Layout:

- Top bar: site/building selector, saved views, search, date range, user/account controls.
- Summary strip: urgent open, new unacknowledged, SLA risk, duplicate clusters, waiting vendor.
- Primary queue: actionable issues sorted by urgency, acknowledgement, SLA risk, and age.
- Right rail: AI insights and recommended next actions.
- Secondary analytics: recurrence, category trends, site/vendor performance.

Avoid showing analytics before action items. Daily operators need action first, analysis second.

### 4.2 Triage Inbox

Purpose: process incoming reports quickly.

Recommended columns:

- Urgency
- Issue summary
- Location / asset
- AI category
- Source / reporter
- Created age
- SLA
- Assigned team/vendor
- Status
- Duplicate count

Default grouping:

1. New / unacknowledged
2. Urgency 3 / immediate
3. Possible duplicates
4. Needs information
5. SLA risk / due soon
6. Waiting vendor
7. Scheduled
8. Resolved

Do not default to simple severity grouping. The default should be decision-first.

Actions:

- Acknowledge
- Accept
- Merge
- Link related
- Route
- Ask for info
- Snooze
- Schedule
- Resolve
- Decline

Power-user requirements:

- Keyboard shortcuts.
- Bulk actions.
- Saved views.
- Fast filters.
- Row preview without leaving queue context.

### 4.3 Issue Decision Panel

Purpose: decide what should happen to a selected report/incident.

Preferred layout: three zones.

#### Left: original evidence

Show:

- Reporter quote.
- Photos/videos.
- QR tag source.
- Site/building/floor/room/asset.
- Reporter/contact/channel.
- Submission time.

#### Center: editable work record

Show:

- Issue title.
- Category/trade.
- Urgency.
- Status.
- Assignee/vendor.
- SLA/due date.
- Internal notes.
- Reporter communication.

#### Right: AI Decision Panel

Show:

- AI interpretation.
- Suggested category.
- Suggested urgency.
- Reasoning.
- Duplicate matches.
- Similar history.
- Suggested assignee/vendor.
- Missing information prompt.
- Audit trail.

AI should never be hidden in a separate chat-first experience. It should sit beside the work.

### 4.4 Asset / Location History

Purpose: identify recurrence and context.

Show:

- Prior reports for this asset/location.
- Repeated categories.
- Previous fixes.
- Vendor history.
- Mean time to resolution.
- Open/closed trend.
- QR tag metadata.
- Preventive maintenance suggestions.

### 4.5 QR Sticker Management

Purpose: manage the physical-to-digital reporting layer.

Each QR sticker should map to:

- Site
- Building
- Floor
- Room/area
- Asset ID, if applicable
- Default categories
- Default routing rules
- Default vendor/team
- Label text
- Fallback short URL/code
- Status: active, replaced, retired

QR labels should clearly say what they do, for example:

> Report an issue in this room  
> Scan to report cleaning, damage, or equipment problems  
> Takes under 30 seconds. No login required.

## 5. Component system

Build with shadcn/ui components, customized for Fridson.

### 5.1 Core components

Use/customize:

- Button
- Input
- Textarea
- Select
- Combobox
- Badge
- Card
- Sheet / drawer
- Dialog
- Tabs
- Dropdown menu
- Tooltip
- Popover
- Toast
- Skeleton
- Command menu
- Data table
- Checkbox
- Radio group
- Switch
- Separator
- Alert

### 5.2 Fridson-specific components

Create these custom components:

#### TriageRow

A dense issue/report row for the triage inbox.

Must support:

- Urgency indicator
- Acknowledgement state
- Issue title
- Location/asset
- Category
- Status
- Age/SLA
- Assignee/vendor
- Duplicate count
- Evidence thumbnail
- AI suggestion indicator

#### DuplicateClusterRow

Shows several reports grouped into one incident.

Must support:

- Canonical issue title
- Number of reports
- First seen / last seen
- Locations/assets involved
- Current owner/status
- Merge/link controls

#### AIDecisionPanel

Right-side AI panel for selected issue.

Sections:

- Interpretation
- Urgency reasoning
- Duplicate matches
- Suggested routing
- Missing information
- Audit trail

#### SeverityReasoningCard

Shows why an urgency level was suggested.

Content:

- Suggested urgency
- Reasoning bullets
- Evidence used
- Rule vs AI indicator
- Confidence
- Override action

#### DuplicateMatchCard

Shows a possible duplicate.

Content:

- Existing issue title
- Similarity/confidence
- Matching reason
- Status
- Owner
- Created/updated time
- Linked report count
- Actions: merge, link, keep separate, ignore

#### SuggestedRouteCard

Shows AI/rule-suggested assignment.

Content:

- Suggested team/vendor
- Reason
- SLA consequence
- Apply/override actions

#### MissingInformationCard

Shows missing data needed to act.

Examples:

- Need photo
- Need exact room
- Need access permission
- Need whether damage is spreading

Actions:

- Ask reporter
- Mark not needed
- Fill manually

#### AuditTrailItem

Shows decision history.

Examples:

- AI suggested Plumbing.
- User changed category to Cleaning.
- Rule escalated to Urgency 3.
- Duplicate suggestion ignored.
- Vendor notified.

## 6. Design tokens

### 6.0 Implementation (shipped in `fridson-app/src/styles.css`)

Canonical brand palette — **cobalt primary**, not teal/green:

| Token | Value | Use |
|-------|-------|-----|
| `--primary` / `--ring` | `#2D5BFF` | CTAs, focus rings, chart primary series, active nav accent |
| `--background` | `#F4F6FB` | Page background |
| `--card` | `#FFFFFF` | Elevated panels |
| `--foreground` | `#0B1220` | Body text |
| `--muted-foreground` | `#4A5568` | Secondary text |
| `--secondary` / `--surface` | `#E6ECFB` | Soft surfaces, sidebar accent bg |

**Border radius (B2B — tighter than consumer SaaS):**

| Token | Value |
|-------|-------|
| `--radius` | `6px` |
| `--radius-md` | `6px` (buttons, badges, inputs) |
| `--radius-lg` | `8px` (cards) |

**Chart series:** `--chart-1` … `--chart-5` map to primary, AI, urgency, muted.

**Status chip helpers:** `src/lib/tokens/status.ts`, `src/lib/tokens/urgency.ts` — always use these instead of raw Tailwind palette classes.

**App shell:** `AppHeader` + `PageContainer` in `src/components/app-shell/`; sidebar nav groups in `app-sidebar.tsx`.

### 6.1 Color principles

Use calm neutral defaults. Reserve intense color for abnormal conditions requiring action.

Do not make every status badge colorful.

Color must never be the only differentiator. Pair color with text, icon, and/or shape.

Suggested use:

- Red: urgent/immediate/action required now.
- Amber/orange: soon/SLA risk/warning.
- Green: resolved/completed/safe.
- Blue: informational/system status.
- Purple/indigo: AI assistance.
- Gray: normal, inactive, neutral, historical.

### 6.2 Urgency tokens

Define:

```ts
urgency.1 = Routine
urgency.2 = Soon
urgency.3 = Immediate
```

#### Urgency 1 — Routine

Meaning:

- Cosmetic
- Minor inconvenience
- Cleaning/restock where not critical
- Improvement request

Visual:

- Neutral/low-emphasis badge
- No alarm styling

#### Urgency 2 — Soon

Meaning:

- Service degradation
- Comfort issue
- Operational disruption
- Could worsen if ignored

Visual:

- Amber badge
- Medium emphasis

#### Urgency 3 — Immediate

Meaning:

- Safety/security risk
- Active leak or spreading damage
- Electrical/fire/regulatory concern
- Critical asset failure
- Access blocked
- Multiple repeated reports in short window

Visual:

- Red badge
- Strong emphasis
- Requires acknowledgement
- Use icon + text + color

### 6.3 Status tokens

Do not collapse all statuses into one ambiguous badge.

Separate these categories.

#### Intake status

- New
- Needs info
- Accepted
- Declined

#### Work status

- Assigned
- In progress
- Waiting vendor
- Scheduled
- Resolved

#### AI status

- Suggested
- Applied
- Auto-applied
- Overridden
- Failed
- Needs review

#### Reporter status

- Notified
- Awaiting reply
- No contact
- Follow-up received

### 6.4 AI tokens

Use purple/indigo sparingly to mark AI assistance.

AI labels:

- AI suggested
- AI applied
- Rule applied
- Human override
- Needs review
- Low confidence

Always clarify whether a field came from:

- Reporter input
- QR metadata
- Rule
- AI inference
- Human edit

### 6.5 Spacing and density

Desktop operator screens should be dense but readable.

Guidelines:

- Use compact rows for queues.
- Use clear section separation.
- Prefer side panels/drawers over full-page interruptions.
- Preserve queue context when opening details.
- Keep common actions close to the issue.

Reporter mobile screens should be spacious and simple.

## 7. Typography

Use a clean, highly legible sans-serif.

Recommended choices:

- Inter
- Geist Sans
- System UI fallback

Desktop hierarchy:

- Page title: clear but not oversized.
- Queue rows: high information density.
- Metadata: smaller, muted.
- Urgent labels: text + icon + color.
- AI reasoning: concise bullets.

Avoid marketing-style typography in the operational interface.

## 8. Layout patterns

### 8.1 Desktop app shell

Recommended structure:

- Header/top bar
- Left navigation or saved views rail
- Main queue/workspace
- Right decision/AI panel

Header should include:

- Product/workspace name
- Site/building selector
- Search
- Saved views
- Notifications/urgent count
- User menu

### 8.2 Empty states

Empty states must teach the next action.

Bad:

> Select an issue.

Better:

> Select a report to classify, merge, route, or resolve. AI will suggest urgency, category, duplicates, and next action — you stay in control.

For AI panel empty state:

Bad:

> The research brief and approve action will appear here.

Better:

> AI Decision Panel shows summary, severity reason, duplicate matches, suggested route, and missing information.

When no issue is selected, show queue-level insights:

- Duplicate clusters found
- New urgent items
- Reports missing information
- SLA risk

### 8.3 Loading states

AI actions must show explicit progress.

Examples:

- Analyzing photo…
- Checking similar reports…
- Applying routing rule…
- Drafting reporter question…

Never leave the user wondering if AI is working.

### 8.4 Feedback states

Every operator action must produce immediate feedback.

Examples:

- Acknowledged
- Routed to Plumbing
- Merged into Issue #123
- Reporter asked for photo
- Snoozed until Monday
- Vendor notified
- Resolved and reporter notified

Use toast for lightweight confirmation and audit trail for permanent history.

## 9. Forms

### 9.1 Reporter QR form

Use GOV.UK-style clarity.

Principles:

- Ask only what is necessary.
- One decision at a time.
- Plain language.
- Clear optional labels.
- Preserve user input after errors.
- Explain why required fields are needed.

Minimum fields:

1. Prefilled location from QR.
2. What is wrong?
3. Photo/video.
4. Safety gate.
5. Optional contact method.

Example labels:

- What is wrong here?
- Add a photo if you can.
- Is anyone in danger or is damage spreading?
- How can we update you? Optional.

### 9.2 Desktop operator form

Use compact sections:

- Summary
- Triage
- Assignment
- Evidence
- History
- Communication
- Audit

AI suggestions should appear as editable defaults/chips, not hidden automation.

### 9.3 Validation

Validation messages should say:

1. What went wrong.
2. How to fix it.
3. Why it matters, if useful.

Examples:

- Choose a room or area so we can route this to the right team.
- Add a photo or confirm no photo is available.
- This looks like an existing open issue. Merge, link, or continue as new.

Do not validate aggressively while the user is typing unless it clearly helps.

## 10. AI behavior rules

### 10.1 AI should assist, not silently decide

AI may suggest:

- Category
- Urgency
- Duplicate match
- Assignee/vendor
- SLA
- Missing information
- Reporter follow-up question
- Resolution note

AI should not silently perform high-risk actions.

Require human approval for:

- Merging issues
- Closing issues
- Dispatching vendors
- Sending external messages
- Escalating urgent incidents
- Changing SLA-critical fields

### 10.2 Show reasoning

Every AI suggestion should answer:

- What was suggested?
- Why?
- What evidence was used?
- How confident is the system?
- What will happen if applied?
- How can the user override it?

Example:

> Suggested Urgency 3 because: active leak, basement mechanical room, two reports in 51 minutes, and possible equipment damage.

### 10.3 Use progressive automation

Automation levels:

1. Off
2. Suggest
3. Auto-fill
4. Auto-route low-risk issues
5. Auto-create work orders for approved categories

High-risk categories should stay approval-gated.

### 10.4 Track AI decisions

Audit log should record:

- AI suggestions
- Accepted suggestions
- Rejected suggestions
- Human overrides
- Auto-applied fields
- Rule-triggered actions
- Confidence changes

Use this for later tuning.

## 11. HMI principles

Fridson is a facility operations interface. Use HMI discipline.

### 11.1 Progressive disclosure

Use four levels:

1. Overview / mission control
2. Operating queue / triage inbox
3. Issue decision detail
4. Asset/location diagnostics

Do not show all complexity at once.

### 11.2 Alarm discipline

Only urgent, actionable problems should look like alarms.

If no specific human response is required, it should not be styled like an alarm.

### 11.3 Consequence-based urgency

Urgency should be based on consequence if ignored, not reporter emotion alone.

Inputs:

- Safety
- Security
- Damage risk
- Compliance
- Comfort impact
- Asset criticality
- Location criticality
- Repetition
- SLA risk
- Time of day

### 11.4 Avoid queue fatigue

Reduce noise by:

- Clustering duplicates
- Batching low-priority updates
- Snoozing scheduled/waiting issues
- Separating “needs decision” from “all activity”
- Requiring acknowledgement only for important items

## 12. Navigation

Primary desktop navigation:

- Mission Control
- Triage Inbox
- Issues
- Assets
- Locations
- QR Stickers
- Vendors / Teams
- Analytics
- Settings

Default view should be Mission Control or Triage Inbox, not Assets.

## 13. Recommended route/page structure

Suggested app routes:

```txt
/                         Mission Control
/triage                   Triage Inbox
/issues                   All Issues
/issues/:id               Issue Detail
/assets                   Assets
/assets/:id               Asset Detail
/locations                Locations
/locations/:id            Location Detail
/qr                       QR Stickers
/qr/:id                   QR Sticker Detail
/vendors                  Vendors/Teams
/analytics                Analytics
/settings                 Settings
/report/:qrCode           Public QR reporter flow
/report/:qrCode/status    Reporter status page
```

## 14. Keyboard shortcuts

Desktop triage should be keyboard-friendly.

Suggested shortcuts:

- `j` / `k`: next/previous issue
- `a`: acknowledge
- `enter`: open/select
- `m`: merge duplicate
- `r`: route/assign
- `s`: snooze
- `i`: ask for info
- `d`: decline
- `e`: edit
- `/`: search
- `cmd+k`: command menu

Show shortcuts in tooltips and command menu.

## 15. Content and labels

Use precise operational language.

Avoid ambiguous labels:

- Failed
- Awaiting
- Open
- Processing
- AI done

Use specific labels:

- AI failed to classify
- Awaiting reporter
- Awaiting vendor
- New unacknowledged
- Assigned
- Scheduled
- Resolved
- Duplicate suggested
- Needs location

## 16. Visual examples in words

### Triage row example

```txt
[Urgency 3] Pump room leak visible
Basement · B1 Mechanical · 2 reports · first seen 16:29 · latest 17:20
AI: Plumbing / leak · Duplicate cluster · SLA 1h · Unacknowledged
Actions: Acknowledge · Merge · Route
```

### AI Decision Panel example

```txt
AI interpretation
Issue: Visible water leak in basement pump room.
Impact: Possible equipment damage if not handled quickly.
Suggested urgency: 3 / Immediate
Why: active leak + mechanical room + repeated reports within 1 hour.
Suggested route: Plumbing vendor / mechanical maintenance.
Duplicate: 86% match with Issue #104, still open.
Actions: Apply · Merge · Route · Ask reporter · Override
```

### QR reporter form example

```txt
Report an issue in Pump Room B1
Location already selected from QR code.

What is wrong?
[Leak / water] [Noise] [Broken equipment] [Other]

Add a photo
[Upload photo]

Is anyone in danger or is damage spreading?
[Yes] [No] [Not sure]

Submit report
```

## 17. Implementation instructions for AI agent

When building Fridson UI:

1. Use shadcn/ui components as the base.
2. Keep the visual design neutral and operational.
3. Build desktop around Mission Control, Triage Inbox, and Issue Decision Panel.
4. Do not make AI a separate chatbot-first interface.
5. Put AI suggestions beside the issue and make them editable.
6. Always show AI reasoning for urgency, duplicate, and routing suggestions.
7. Separate intake status, work status, AI status, and reporter status.
8. Cluster duplicate reports instead of showing them as equal independent tickets.
9. Use a 3-level urgency model: Routine, Soon, Immediate.
10. Use QR codes as source-of-truth context for location/asset.
11. Make reporter flow mobile-first and minimal.
12. Make operator flow desktop-first, dense, and keyboard-friendly.
13. Use calm colors and reserve red/orange for actionable urgency.
14. Preserve queue context when viewing issue detail.
15. Provide immediate feedback for every action.
16. Store AI and human decisions in an audit trail.

## 18. Design quality checklist

Before accepting a screen, verify:

- Does it answer what the user should do next?
- Is the most urgent actionable item visually obvious?
- Are duplicates clustered?
- Is AI helping inside the workflow?
- Can the user override AI suggestions?
- Is urgency explained?
- Are statuses specific and non-ambiguous?
- Is color used sparingly?
- Can a trained desktop operator move quickly?
- Can a first-time reporter submit without understanding Fridson?
- Is QR context carried into the issue record?
- Are validation errors recoverable and clear?
- Does every action create visible feedback?
- Is there an audit trail for important decisions?

## 19. Summary

Fridson should use **shadcn/ui + Radix UI + Tailwind + TanStack Table** as the technical design-system base.

The product should feel like:

> A calm AI-assisted facility operations console, with Linear-style triage speed, Carbon-style enterprise restraint, GOV.UK-style form clarity, and high-performance HMI urgency discipline.

The interface should always prioritize:

1. What needs attention now.
2. Why it matters.
3. What evidence exists.
4. Whether it is duplicate or recurring.
5. What action should happen next.
6. Whether AI is suggesting, applying, or being overridden.
