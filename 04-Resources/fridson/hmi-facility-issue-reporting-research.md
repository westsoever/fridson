# HMI / Facility Issue Reporting UX Research for Fridson

## Scope
Research focus: HMI/operator-interface and facility/property-maintenance issue reporting best practices, with emphasis on desktop usability, cognitive load, alarm/error reporting, maintenance request intake, form design, dashboards, prioritization, multi-site contexts, and QR-to-desktop continuity.

## Executive synthesis

A Fridson-style product should treat building issue reporting as a **human-factors intake and triage system**, not just a ticket form. The strongest pattern across industrial HMI, public-service form design, and CMMS maintenance reporting is: **reduce human memory burden at intake, convert vague observations into structured, actionable work, then show operators a prioritized portfolio view with clear drill-down paths**.

Key implications:

1. **Only ask for information that changes the next action.** GOV.UK says services should know why every question is being asked and only ask users for information really needed[^1](https://design-system.service.gov.uk/patterns/question-pages/). NN/g similarly recommends single-column structure, logical grouping, upfront expectations, plain language, and support/error handling to reduce cognitive load[^2](https://www.nngroup.com/articles/4-principles-reduce-cognitive-load/).
2. **Issue severity should be operationalized, not left entirely to the reporter.** Alarm-management standards emphasize rationalization and prioritization so alerts are meaningful, actionable, and support timely decision-making[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards). HSE’s alarm guidance says priorities should be based on potential consequence if the operator does not respond, with roughly three priority levels and a target distribution around 5% high / 15% medium / 80% low[^4](https://www.hse.gov.uk/pubns/chis6.pdf).
3. **Desktop should be the command center; QR/mobile should be the lowest-friction capture layer.** NN/g says QR codes need clear context and should deep-link to the relevant action rather than a generic homepage[^5](https://www.nngroup.com/articles/qr-code-guidelines/). Facility-management sources show QR codes can connect physical assets/spaces directly to CMMS request pages and reduce phone/email/sticky-note transcription[^6](https://fiixsoftware.com/blog/why-you-should-be-using-qr-codes-for-facility-management/).
4. **Desktop dashboards should follow high-performance HMI principles: overview → operating list → detail → diagnostics.** Rockwell’s Process HMI Style Guide recommends progressive disclosure, matching displays to user goals/tasks/mental models, avoiding visual clutter, and reserving bright/intense colors for alarms[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).
5. **Multi-site facility contexts need standard definitions and hierarchy.** Multi-site CMMS guidance emphasizes standardizing work-order intake, approvals, escalation paths, KPIs, asset hierarchy, and data capture methods so leaders compare trusted data across sites[^8](https://limble.com/blog/multi-site-facility-management)[^9](https://www.getmaintainx.com/blog/practical-guide-to-multi-site-maintenance-reporting).

---

## 1. HMI/operator-interface principles relevant to Fridson

### 1.1 Progressive disclosure and display hierarchy

High-performance HMI design is built around progressive disclosure: show the right amount of information at the right operational level. Rockwell’s guide explicitly says display hierarchy and organization should provide progressive disclosure[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf). It describes a four-level structure: Level 1 overview for high-level KPIs and top priorities; Level 2 operating displays for primary tasks; Level 3 detail for troubleshooting; Level 4 support for detailed subsystems, sensors, and faceplates[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

**Fridson translation:**
- **Level 1: Portfolio overview** — buildings/areas with open urgent issues, SLA breaches, repeated assets, unresolved safety/comfort problems.
- **Level 2: Work queue** — triage board/list for facility managers: new, needs info, assigned, in progress, waiting vendor, resolved.
- **Level 3: Issue detail** — reporter context, photos, location/asset, AI classification, similar history, suggested assignment, comments, status timeline.
- **Level 4: Asset/location diagnostics** — asset history, repeated failure patterns, vendor records, QR tag metadata, documents, sensor/IoT hooks later.

### 1.2 Design around operator goals, not system architecture

Rockwell’s guide says HMI displays should match users’ goals, tasks, and mental model rather than the mechanical design or P&ID diagrams[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf). EPRI’s control-room HSI guidance covers information displays, soft controls, alarms, automation, computerized procedures, and portable devices, with emphasis on situation awareness, decision-making, and reducing human error through cognitive-centered design[^10](https://www.epri.com/research/products/000000003002004310).

**Fridson translation:** structure desktop around facility-manager jobs-to-be-done:
- “What requires my attention now?”
- “What is blocked and why?”
- “Who should handle this?”
- “Is this recurring?”
- “Which buildings/assets are becoming risky?”

Avoid making the main navigation mirror database objects such as “Assets / Locations / Tickets / Users” as the first mental model. Use task-first navigation with database drill-downs underneath.

### 1.3 Visual hierarchy and color discipline

Rockwell’s guide recommends that “every pixel has a purpose,” muted non-data pixels, grayscale/light-gray backgrounds, and bright/intense colors only for alarms; it also warns that color cannot be the sole differentiator and should be paired with shape/icons/text[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

**Fridson translation:**
- Do not make every status a colorful badge. Reserve red/orange for “needs action now.”
- Use text + icon + color for severity/status, not color alone.
- Keep default state calm: gray/neutral backgrounds, clear typography, dense but readable tables.
- Put the most urgent queue or KPI top-left, since Rockwell notes top-left is the greatest-emphasis region[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

### 1.4 Response time and feedback

Rockwell’s HMI style guide gives performance expectations: Level 2/3 displays should load in under 2 seconds, Level 1/4 in under 5 seconds, and system response to user entry should occur in 0.5–2 seconds to confirm receipt[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

**Fridson translation:**
- On desktop, every triage action should produce immediate acknowledgement: assigned, priority changed, AI route accepted, vendor notified, reporter asked for more information.
- Avoid AI “thinking” without a visible status. If AI classifies a report, show “Analyzing photo/location…” followed by the proposed category, urgency, confidence, and reason.

---

## 2. Alarm/error-reporting lessons for facility issue prioritization

### 2.1 An alarm must require a response

Human-factors alarm guidance defines an alarm as an indication of malfunction/deviation/abnormal condition requiring a specific human response; if no response is required, it should be status information rather than an alarm[^11](https://humanfactors101.com/topics/alarms/). HSE similarly states alarms must require operator action and that process status indicators should not be designated as alarms[^4](https://www.hse.gov.uk/pubns/chis6.pdf).

**Fridson translation:** distinguish sharply between:
- **Issues requiring action**: leak, blocked fire exit, broken lock, no heat, elevator fault.
- **Observations/status**: “looks worn,” “paint scuffed,” “FYI noise sometimes.”
- **Requests**: “please add signage,” “can we get more bins?”

The UI should not treat all submissions as equal “tickets.” It should convert intake into an actionable type with response expectations.

### 2.2 Prevent alarm floods and queue fatigue

HSE’s Better Alarm Handling guidance gives alarm-rate targets: long-term average should be no more than one alarm every ten minutes during normal operation, and fewer than ten alarms in the first ten minutes after a major upset[^4](https://www.hse.gov.uk/pubns/chis6.pdf). HumanFactors101 highlights extreme incident examples such as Milford Haven, where operators faced 275 alarms in 11 minutes, and Esso Longford, where operators dealt with 8,500 alarms in a 12-hour shift[^11](https://humanfactors101.com/topics/alarms/).

**Fridson translation:** facility managers can experience a softer version of alarm flooding when every QR report, duplicate complaint, chat message, and vendor update is equal in the inbox. Fridson should:
- Merge duplicate/repeated reports by location/asset/time window.
- Batch low-priority updates into digest views.
- Surface “new high-risk issue,” “SLA breach,” and “repeated asset failure” as distinct alerts.
- Make “needs human decision” smaller than “all activity.”

### 2.3 Use few, consequence-based priority levels

ISA-18.2 materials emphasize alarm objectives, prioritization, classification, and design principles so alarms are meaningful and actionable[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards). HSE recommends about three priority levels, assigned based on the consequence if the operator fails to respond, with an approximate distribution of 5% high, 15% medium, and 80% low[^4](https://www.hse.gov.uk/pubns/chis6.pdf).

**Fridson translation:** avoid asking occupants “How urgent is this?” as the primary priority source. Use a 3-level internal urgency model:
- **Urgency 3 / Immediate:** safety, security, water/electrical damage, access blocked, regulatory risk, severe tenant impact.
- **Urgency 2 / Soon:** comfort/service degradation, operational disruption, visible deterioration that may worsen.
- **Urgency 1 / Routine:** cosmetic, minor inconvenience, planned improvement.

Let users optionally say “this is urgent,” but have AI/system rules infer priority from category, asset, location, photos, repeated reports, time of day, and SLA.

### 2.4 Support acknowledgement, shelving, suppression, and audit

Rockwell notes unacknowledged alarms should be visibly distinct until acknowledged and describes shelving to temporarily suppress alarms during abnormal situations[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf). ISA-18.2 covers the lifecycle from identification and rationalization to implementation, maintenance, and ongoing change management[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards). HSE recommends audits, reviews, operator feedback, and a site/company alarm strategy[^4](https://www.hse.gov.uk/pubns/chis6.pdf).

**Fridson translation:**
- Add explicit **Acknowledge** for new high-priority issues so the team knows a human has seen them.
- Add **Snooze / waiting on vendor / scheduled** states so non-actionable issues stop cluttering “needs action.”
- Add an **audit timeline**: submitted → classified → acknowledged → assigned → vendor contacted → resolved → reporter notified.
- Track priority overrides and AI-confidence changes for later improvement.

---

## 3. Desktop form design for maintenance intake and triage

### 3.1 Ask fewer, clearer questions

GOV.UK question-page guidance says teams should know why every question is asked and only ask for information really needed[^1](https://design-system.service.gov.uk/patterns/question-pages/). It recommends starting with one question per page to help users focus, not asking users to re-enter information already provided, and labeling optional fields with “(optional)”[^1](https://design-system.service.gov.uk/patterns/question-pages/). NN/g recommends logical grouping, visual hierarchy, transparency about requirements/time/saved progress, plain language, familiar UI conventions, and timely support[^2](https://www.nngroup.com/articles/4-principles-reduce-cognitive-load/).

**Fridson intake fields should be split by role:**

**Occupant / QR reporter minimum viable fields**
1. Location is prefilled from QR tag.
2. “What is wrong?” free-text or quick category chips.
3. Photo/video optional but encouraged.
4. Contact method optional/required depending on follow-up need.
5. “Is anyone in danger or is damage spreading?” simple safety gate.

**Facility manager triage fields**
1. Category / trade.
2. Urgency.
3. Assigned person/vendor.
4. SLA / due date.
5. Asset/location linkage.
6. Duplicate/repeated issue linkage.

Do not expose facility-manager fields to occupants unless necessary.

### 3.2 Use progressive disclosure instead of one intimidating form

NN/g states single-column layouts outperform multicolumn designs for completion, and progressive disclosure/“one thing per page” helps complex forms avoid overwhelming users[^2](https://www.nngroup.com/articles/4-principles-reduce-cognitive-load/). GOV.UK similarly recommends starting with one question per page and grouping multiple questions only when research shows it helps, such as internal users repeating/switching tasks quickly[^1](https://design-system.service.gov.uk/patterns/question-pages/).

**Fridson translation:**
- **Mobile QR flow:** one screen per decision, large controls, photo-first.
- **Desktop admin flow:** compact, grouped panels are acceptable for trained repeat users, but use progressive sections: Summary, Triage, Assignment, History, Communication.
- **AI assist:** show “suggested category/urgency/assignee” as editable defaults, not hidden automation.

### 3.3 Design error handling around recovery, not blame

GOV.UK validation guidance says that when there is a validation error, tell users what went wrong and how to fix it; show an error summary at the top, inline messages next to fields, move keyboard focus to the error summary, add “Error:” to the page title, and retain previously entered information[^12](https://design-system.service.gov.uk/patterns/validation/). GOV.UK also advises waiting until users try to move to the next step rather than validating on blur, except where research shows real-time validation helps[^12](https://design-system.service.gov.uk/patterns/validation/).

**Fridson translation:**
- If a report lacks location, say: “Choose the room or area so we can send the issue to the right team.”
- Preserve photos/text after validation errors.
- On desktop, show a top error summary for multi-field triage forms and inline errors for specific fields.
- Avoid premature errors while a user is still typing a description.

### 3.4 Reduce cognitive load by offloading memory into the interface

NN/g defines cognitive load as the mental resources required to operate a system and recommends minimizing extraneous load, reducing visual clutter, using familiar mental models, and showing previously entered information rather than making users remember it[^13](https://www.nngroup.com/articles/minimize-cognitive-load/).

**Fridson translation:**
- Show the QR-derived location and asset visibly in the form.
- Show previous issues at the same location/asset before the manager creates a new work order.
- Pre-fill reporter, building, floor, asset, trade, and suggested vendor where possible.
- Provide recognition-based choices (“Leak,” “Temperature,” “Light,” “Door/lock,” “Cleaning”) rather than requiring users to invent the correct category.

---

## 4. Dashboard and prioritization best practices

### 4.1 Dashboard should be an action surface, not a report dump

Industrial HMI and CMMS sources converge on the idea that dashboards should support timely decisions. ISA-18.2 emphasizes HMI design for situational awareness and timely decision-making[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards). Inductive Automation describes HMIs as interfaces/dashboards that centralize data, show graphs/charts/digital dashboards, manage alarms, and integrate with SCADA/ERP/MES systems[^14](https://inductiveautomation.com/resources/article/what-is-hmi). MaintainX’s multi-site reporting guide says effective reporting must trigger actions, with reviews that focus on trends and clear follow-ups for outliers[^9](https://www.getmaintainx.com/blog/practical-guide-to-multi-site-maintenance-reporting).

**Fridson dashboard should answer in order:**
1. What needs action now?
2. What is about to breach SLA?
3. What is blocked?
4. What is repeating?
5. Where are site/team/vendor patterns emerging?

### 4.2 Recommended desktop dashboard layout

**Top bar / portfolio controls**
- Building/site selector, saved views, search, date range, role filter.

**Level 1 summary strip**
- Urgency 3 open.
- New unacknowledged.
- SLA breach / due today.
- Repeated issue clusters.
- Vendor waiting.

**Primary work queue**
- Sort default: urgent + unacknowledged + SLA risk + age.
- Columns: urgency, issue summary, location/asset, AI category, reporter, created, SLA, assignee/vendor, status, duplicate count.
- Keyboard-friendly row navigation and bulk actions.

**Right-side detail pane**
- Opens without losing queue context.
- Shows photos, AI reasoning, location map/floor/asset, history, similar issues, timeline, next action.

**Secondary analytics**
- Trends by site, category, asset, vendor, response time, recurrence.
- Keep analytics secondary to action queue for daily operators.

### 4.3 Prioritization logic for Fridson

Use a composite triage model, visible and editable:

**Priority score inputs**
- Consequence category: safety/security/damage/compliance/comfort/cosmetic.
- Location criticality: entrance, toilet, elevator, server room, common area, tenant unit.
- Asset criticality: HVAC, access control, plumbing, electricity, fire/safety equipment.
- Time sensitivity: active leak, after-hours, event day, SLA approaching.
- Repetition: multiple reports same asset/location.
- Confidence: AI certainty from text/photo/location.

**Display output**
- Urgency 1–3.
- Reason: “Urgency 3 because: water leak + electrical room + photo confidence high.”
- Action: “Assign plumber vendor,” “Ask reporter for photo,” “Merge with existing issue,” “Schedule inspection.”

---

## 5. Multi-site facility/property maintenance contexts

### 5.1 Standardize workflows, KPIs, and asset hierarchy

Limble recommends consistent workflows for work-order intake, approvals, preventive maintenance schedules, and escalation paths, plus shared checklists and SLAs for quality across sites[^8](https://limble.com/blog/multi-site-facility-management). MaintainX’s guide says multi-site reporting requires standard KPI definitions, data capture methods, and asset hierarchies/naming conventions so leaders compare trusted data rather than different methodologies[^9](https://www.getmaintainx.com/blog/practical-guide-to-multi-site-maintenance-reporting).

**Fridson translation:**
- Use global issue categories but allow site-level routing rules.
- Use standardized asset/location naming: Site → Building → Floor → Area → Asset.
- Define SLA by urgency/category/site, not ad hoc per issue.
- Make every QR tag map to a canonical location/asset record.

### 5.2 Compare sites with context, not leaderboard shaming

MaintainX warns that ranking sites without context can lead to wrong conclusions; leaders should compare similar asset classes and layer context over raw numbers[^9](https://www.getmaintainx.com/blog/practical-guide-to-multi-site-maintenance-reporting). Limble recommends portfolio views that can drill down from portfolio to region/site/building using the same login[^8](https://limble.com/blog/multi-site-facility-management).

**Fridson translation:**
- Compare similar spaces/assets: “toilet issues per 1,000 visits,” “HVAC response by building age,” “elevator recurrence by vendor.”
- Let users drill from portfolio → site → floor/area → issue/asset.
- Include context notes: renovation, weather, event, tenant move-in, vendor change.

### 5.3 Case-study signals from CMMS implementations

MaintainX reports several CMMS case-study outcomes: Michaels reduced MTTR by 70% and increased MTBF by 20% across seven distribution centers; THIRA Health centralized over 4,900 work orders through a maintenance portal; Cintas standardized procedures across 200 sites in nine weeks; Cayman Islands Public Works used QR codes at public facilities so citizens could submit requests directly[^15](https://www.getmaintainx.com/blog/facility-maintenance-examples-7-cmms-success-stories). These are vendor-reported claims, so they should be treated as directional evidence rather than independent proof.

**Fridson implication:** the strongest market pattern is that digitizing intake is valuable when it also standardizes work orders, naming, procedures, reporting, and audit trails—not when it merely replaces email with a form.

---

## 6. QR-to-desktop continuity

### 6.1 QR codes need information scent and context

NN/g says QR codes lack information scent and need contextual information to convince users to scan; unlabeled codes are not trustworthy or enticing[^5](https://www.nngroup.com/articles/qr-code-guidelines/). It also says QR codes should link to information directly related to the code context rather than a generic homepage[^5](https://www.nngroup.com/articles/qr-code-guidelines/).

**Fridson QR label pattern:**
- “Report an issue in this room”
- “Scan to report cleaning, damage, or equipment problems”
- “Takes under 30 seconds. No login required.”
- Include fallback short URL / code for accessibility and broken camera scenarios.

### 6.2 QR should carry physical context into the digital workflow

Fiix says QR codes can be attached to assets to provide rapid access to the maintenance page in a CMMS, and that someone who sees a maintenance need can scan and quickly submit a request, receiving notification that the request is being handled[^6](https://fiixsoftware.com/blog/why-you-should-be-using-qr-codes-for-facility-management/). Fiix also notes that without QR codes, facility managers receive phone calls, emails, and sticky notes that must be interpreted and transcribed manually[^6](https://fiixsoftware.com/blog/why-you-should-be-using-qr-codes-for-facility-management/).

**Fridson translation:** every QR scan should prefill:
- Site/building/floor/room/area.
- Asset ID if asset-specific.
- Tenant/customer/account if appropriate.
- Reporting channel/source.
- Default category suggestions based on tag type.

### 6.3 Continuity should support “scan now, manage later”

NN/g notes QR codes can support transitions or authentication between mobile and another screen/device[^5](https://www.nngroup.com/articles/qr-code-guidelines/). For Fridson, the most important continuity is not necessarily desktop authentication for occupants; it is the operational handoff from physical report to desktop triage.

**Continuity recommendations:**
- After mobile submission, generate a short issue ID and confirmation page.
- Send reporter a magic link or email/SMS status page if contact is provided.
- In desktop, show the original QR tag, photos, and reporter language unchanged alongside AI interpretation.
- If a manager opens a QR-linked issue on desktop, provide full triage controls without requiring re-entry.
- If a report is started on mobile but needs more detail, allow “continue on desktop” link/email for staff or reporters.

---

## 7. Specific recommendations for Fridson

### Recommendation 1 — Reframe desktop around “mission control,” not “ticket admin”

Create a calm, HMI-style desktop homepage with:
- Top-left urgent queue.
- Acknowledgement state for new urgent items.
- SLA and blocked-work indicators.
- Repeated issue clusters.
- Drill-down hierarchy from portfolio to issue detail.

Rationale: HMI sources emphasize situational awareness, timely decision-making, progressive disclosure, and visual hierarchy[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards)[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

### Recommendation 2 — Use a 3-level urgency system with visible reasoning

Implement Urgency 1/2/3 with system-suggested classification and editable reasoning. Base it on consequence, not reporter emotion alone.

Rationale: HSE recommends approximately three priority levels and consequence-based prioritization[^4](https://www.hse.gov.uk/pubns/chis6.pdf). ISA materials emphasize alarm objectives, prioritization, classification, and actionable decision support[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards).

### Recommendation 3 — Separate occupant intake from operator triage

Occupants should see a minimal QR form. Facility managers should see structured triage controls. Technicians/vendors should see work execution details.

Rationale: GOV.UK and NN/g both emphasize asking only necessary questions, grouping logically, reducing form load, and preventing unnecessary re-entry[^1](https://design-system.service.gov.uk/patterns/question-pages/)[^2](https://www.nngroup.com/articles/4-principles-reduce-cognitive-load/).

### Recommendation 4 — Make duplicate detection and clustering a core feature

Group reports by same QR tag/location/asset/category/time window. Show “5 people reported this toilet leak” as one issue with multiple reporters, not five equal tickets.

Rationale: Alarm-management guidance focuses on reducing alarm floods and nuisance alarms so operators can notice what matters[^4](https://www.hse.gov.uk/pubns/chis6.pdf)[^11](https://humanfactors101.com/topics/alarms/).

### Recommendation 5 — Add “acknowledge / snooze / waiting / scheduled” states

Do not leave every issue in a generic “open” bucket. Add operational states that remove non-actionable items from the urgent queue while preserving auditability.

Rationale: HMI alarm workflows distinguish unacknowledged conditions and support shelving/suppression where appropriate[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).

### Recommendation 6 — Use QR tags as the source of truth for location context

Every QR code should deep-link to a specific room/asset form, not a homepage. It should include a plain-language label, fallback URL/code, and durable redirect handling.

Rationale: NN/g recommends context labels and direct links for QR codes[^5](https://www.nngroup.com/articles/qr-code-guidelines/). Fiix describes QR codes as a bridge from physical assets to CMMS maintenance pages[^6](https://fiixsoftware.com/blog/why-you-should-be-using-qr-codes-for-facility-management/).

### Recommendation 7 — Build the desktop issue detail as a decision panel

Issue detail should include:
- Original report quote and photo.
- AI category/urgency/assignee suggestion with confidence.
- “Why this priority?” explanation.
- Similar past issues.
- Asset/location history.
- Suggested next action.
- Timeline/audit trail.

Rationale: NN/g recommends offloading memory into the interface and using familiar patterns to reduce cognitive load[^13](https://www.nngroup.com/articles/minimize-cognitive-load/). Multi-site maintenance sources emphasize structured data capture, failure causes, asset hierarchy, and actionable reporting[^9](https://www.getmaintainx.com/blog/practical-guide-to-multi-site-maintenance-reporting).

### Recommendation 8 — Standardize multi-site data before overbuilding analytics

Before advanced dashboards, define standard categories, location hierarchy, asset naming, SLA rules, status vocabulary, and vendor routing rules.

Rationale: Limble and MaintainX both emphasize standardized workflows, KPIs, asset hierarchies, and site-level reporting as prerequisites for trustworthy multi-site visibility[^8](https://limble.com/blog/multi-site-facility-management)[^9](https://www.getmaintainx.com/blog/practical-guide-to-multi-site-maintenance-reporting).

### Recommendation 9 — Keep AI human-in-the-loop

AI should propose, not silently decide, for early Fridson versions:
- Category.
- Urgency.
- Duplicate match.
- Assignee/vendor.
- Reporter follow-up question.
- Preventive-maintenance insight.

Show confidence and allow one-click correction. Store corrections as training signals.

Rationale: HMI and alarm systems emphasize human situational awareness and timely decision-making rather than opaque automation[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards)[^10](https://www.epri.com/research/products/000000003002004310).

### Recommendation 10 — Prototype three concrete desktop screens next

1. **Mission Control Dashboard** — portfolio/site overview + urgent queue.
2. **Triage Inbox** — structured list with filters, bulk actions, AI-suggested routing.
3. **Issue Decision Panel** — original report + AI interpretation + history + actions.

For mobile/QR, prototype:
1. **QR landing page** — prefilled location, issue prompt, photo upload, safety gate.
2. **Confirmation/status page** — issue ID, expected response, optional contact updates.
3. **Reporter follow-up page** — answer one clarifying question without login.

---

## Best source list

- EEMUA 191 Edition 4 release: alarm systems are an essential part of operator interfaces and support operators in abnormal situations; aligned with ISA 18.2 and IEC 62682[^16](https://www.eemua.org/news/good-practice-for-all-aspects-of-industrial-alarm-systems-%E2%80%93-new-edition-of-eemua-191-released).
- ISA-18 series: alarm lifecycle, HMI situational awareness, rationalization, prioritization, metrics[^3](https://www.isa.org/standards-and-publications/isa-standards/isa-18-series-of-standards).
- HSE Better Alarm Handling: concrete alarm rate and prioritization targets[^4](https://www.hse.gov.uk/pubns/chis6.pdf).
- Rockwell Process HMI Style Guide: progressive disclosure, hierarchy levels, visual hierarchy, color discipline, alarm breadcrumbs/shelving[^7](https://literature.rockwellautomation.com/idc/groups/literature/documents/wp/proces-wp023_-en-p.pdf).
- EPRI HSI guidance: control-room/digital human-system interface design across displays, alarms, automation, portable devices[^10](https://www.epri.com/research/products/000000003002004310).
- NN/g forms and cognitive load: structure, transparency, clarity, support; minimize extraneous mental load[^2](https://www.nngroup.com/articles/4-principles-reduce-cognitive-load/)[^13](https://www.nngroup.com/articles/minimize-cognitive-load/).
- GOV.UK form/question/validation patterns: ask only necessary questions; one thing per page; accessible error summaries and inline messages[^1](https://design-system.service.gov.uk/patterns/question-pages/)[^12](https://design-system.service.gov.uk/patterns/validation/).
- NN/g QR guidelines: context labels, direct links, mobile-friendly destinations, device transitions[^5](https://www.nngroup.com/articles/qr-code-guidelines/).
- Fiix QR facility management: QR as bridge from physical assets/spaces to CMMS request pages; reduces phone/email/sticky-note transcription[^6](https://fiixsoftware.com/blog/why-you-should-be-using-qr-codes-for-facility-management/).
- Limble / MaintainX multi-site maintenance reporting: standardization, hierarchy, KPIs, site comparisons, action-oriented reporting[^8](https://limble.com/blog/multi-site-facility-management)[^9](https://www.getmaintainx.com/blog/practical-guide-to-multi-site-maintenance-reporting).

## Research gaps / caveats

- The full ISA-18, ISA-101, EEMUA 191, and High Performance HMI Handbook materials are standards/books and not fully accessible from public pages. I used public standard summaries, HSE guidance, EEMUA’s release page, and Rockwell’s public style guide as accessible substitutes.
- One attempted NN/g dashboard URL (`https://www.nngroup.com/articles/dashboard-design/`) returned 404, so dashboard guidance here relies on HMI sources and maintenance-reporting sources instead of that page.
- One Control.com article extraction failed due to page-conversion errors, so I did not rely on it for factual claims.
- CMMS case-study outcomes from MaintainX are vendor-reported. They are useful directional signals but should be independently validated before being used as investor-grade proof.
