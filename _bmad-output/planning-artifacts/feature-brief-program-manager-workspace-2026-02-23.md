---
date: 2026-02-23
author: Root
parent: product-brief-Testing-2026-02-22.md
persona: Program Manager
status: draft
---

# Feature Brief: Program Manager Workspace
## CluePoints Integrated Platform — User-Centric Workspace

---

## Overview

The Program Manager is the portfolio overseer for a therapeutic area. She sits above the study-level execution layer — above CDMs, central monitors, and study managers — and below the sponsor's senior leadership. She is accountable for the performance of the entire program: not just whether any one trial is on track, but whether the portfolio as a whole is healthy, appropriately resourced, and free of systemic risks that no single study manager can see.

Her workspace must serve two simultaneous functions:

1. **Portfolio monitor** — maintaining a fast, reliable pulse on health across 4–6 trials simultaneously, without requiring her to enter each study's modules individually or wait for status updates from study managers.
2. **Escalation endpoint** — items that exceed Study Manager or Risk Lead authority surface to Nadia for final decision. She is the terminal node for in-platform escalations; items that require sponsor-level input exit the platform through her.

This brief defines the specific workspace requirements for the Program Manager persona: what she sees, what she can do, how AI assists her, and how her workspace sits at the top of the CluePoints escalation hierarchy.

---

## Persona Recap

**Nadia** — Program Manager at a sponsor organization, responsible for a portfolio of 4–6 active trials within a single therapeutic area (e.g., oncology or cardiovascular). She is accountable to senior leadership for portfolio-level reporting, to the CRO for delivery oversight, and to the clinical operations team for resource allocation decisions across studies.

**Access pattern:** Bi-weekly as the default cadence, with some weekly touchpoints when a study is at a critical milestone or when leadership reporting is imminent. Not a daily user. Her infrequent login cadence makes the delta view — what changed since she was last in the platform — her most critical orientation mechanism.

**Reports to:** Senior leadership / therapeutic area head / VP of Clinical Operations

**Collaborates with:** Study Managers (receives status, directs attention), Risk Leads (governance escalations), Sponsors / Medical Leadership (reporting out)

**Uses CluePoints as:** One of several tools. She also works in email, Microsoft Word, and presentation software for leadership reporting. CluePoints is her source of signal; it is not her communication channel.

**Key tensions:**

- Has no portfolio view in CluePoints today — synthesizes across studies from emails and status documents assembled by Study Managers
- Cannot answer leadership questions directly from the platform; must ask Study Managers to pull data that CluePoints holds
- Aware that the signal she needs exists in the platform but cannot surface it at her level of abstraction
- Responsible for spotting cross-study patterns (systemic site issues, regional enrollment trends, protocol training gaps) that no individual Study Manager is positioned to see — but currently does this through a manual briefing process rather than platform data
- Visits the platform infrequently, so her tolerance for navigation and reconstruction is low — she needs to reach portfolio health in seconds, not minutes

---

## What the Program Manager Workspace Must Deliver

### 1. Program Health Overview

The primary panel. The first thing Nadia sees on login. It presents the full portfolio as a set of study tiles — one per assigned trial — synthesized into a single coherent view that tells her whether her program is healthy, where to look, and what is moving.

This panel is not a navigation index. It is a health surface. Each tile must encode enough signal that Nadia can make a triage decision — "this study needs attention, this one is fine" — without opening anything.

**Required elements per study tile:**

| Element | Description |
|---------|-------------|
| Study name and phase | Study identifier and current clinical phase (Phase II, Phase III, etc.) |
| Overall health RAG | Composite Red/Amber/Green signal derived from the Study Manager's study health signal — site risk distribution, query aging, KRI adherence, and milestone status rolled up to a single portfolio-visible indicator |
| RAG delta indicator | Change in health status since Nadia's last login — e.g., "Amber (was Green, 3 days ago)." This is distinct from the current RAG; the delta is what tells Nadia what is moving |
| Open escalation count | Number of items in the cross-study escalation queue attributed to this study; badge displayed on tile |
| Milestone proximity | Next key milestone (e.g., enrollment complete, database lock, CSR submission) with days remaining and a confidence indicator (On Track / At Risk / Off Track) |
| Last-updated timestamp | When the study's data was last refreshed into the portfolio view; indicates data currency, not just display time |
| Study Manager | Name of the SM assigned — so Nadia knows who to contact if she needs to discuss |

**Tile sorting and filtering:**

- Default sort: Red tiles first, then Amber, then Green — within each color, sorted by open escalation count descending
- Secondary sort: milestone proximity (studies with a milestone in the next 30 days promoted)
- Nadia can re-sort by: study name, last updated, escalation count, milestone date
- Filtering: Nadia can filter tiles by health status (e.g., show Red and Amber only) for rapid triage

**Tile drill-down:**

Clicking a tile opens a study detail panel inline (see Panel 6 — Study Detail Drill-Down) without navigating away from the Program Health Overview. The portfolio view remains visible behind the detail panel. Nadia can close the detail panel and return to the portfolio without losing her place.

**Design principles:**

- Portfolio is Nadia's default orientation. She never starts inside a single study; she always starts here.
- Exception-first: Red and Amber tiles are visually dominant. A portfolio where all studies are Green should look calm; a portfolio where two studies are Red should look urgent.
- The delta view ("was Green") is not a tooltip or secondary label — it is a first-class element of each tile. Nadia checks in infrequently; she needs to know what moved, not just what the current state is.

---

### 2. Cross-Study Escalation Queue

Items that have been escalated to Nadia from Risk Leads and Study Managers across her portfolio. This is the in-platform escalation inbox at the program level.

Unlike the Study Manager's Decision Queue — which can contain many operational items requiring daily attention — the Program Manager's escalation queue should be small and high-stakes. If this queue contains more than five items, something is wrong in the escalation model below Nadia. Items that reach her should represent decisions or situations that genuinely exceed the authority or visibility of the Study Manager or Risk Lead.

**Item types that appear here:**

| Source | Item type | Expected action |
|--------|-----------|-----------------|
| Study Manager | Escalation requiring PM authority or sponsor visibility — e.g., site suspension with program-level implications, protocol deviation pattern | Acknowledge, direct response, schedule discussion, or escalate to sponsor (offline) |
| Risk Lead | Cross-study risk governance decision — e.g., threshold change recommendation with program-level impact | Acknowledge, approve, or return with direction |
| System | SLA breach — PM-level escalation queue item aged beyond configured threshold without PM action | Acknowledge and act; SLA breach notification sent to supervisor |
| AI | AI-detected cross-study pattern requiring PM awareness or decision — e.g., same site issue appearing across 3 studies in the portfolio | Review AI finding, acknowledge, assign to SM for investigation, or escalate to sponsor |

**Queue item display:**

Each item in the queue shows:

| Field | Description |
|-------|-------------|
| Study | Which study this escalation originated from |
| Escalating party | Who raised it (Role + Name) — e.g., "Study Manager — Elena C." |
| Escalation type | Categorized: Site Issue / Protocol Deviation / KRI / Milestone Risk / Cross-Study Pattern / Other |
| Summary | One-to-two sentence plain-language description of the issue, either written by the escalating party or AI-synthesized from the underlying signal |
| Age | Time since the item was escalated to Nadia's queue |
| Prior actions | What has already been done by the SM / Risk Lead before escalating |

**Inline decision actions:**

Nadia can resolve items from the queue without leaving the workspace:

| Action | Effect |
|--------|--------|
| Acknowledge | Marks item as reviewed; stops aging notification; does not close the item |
| Direct response | Opens an inline response field; Nadia's response is logged and visible to the escalating party in their workspace |
| Schedule discussion | Logs that a discussion has been scheduled; allows Nadia to note the expected resolution date; temporarily pauses aging alerts |
| Escalate to sponsor (offline) | Logs that the item has been escalated externally; item is closed in-platform with a note ("escalated to sponsor via [channel], [date]"); item is removed from the queue but remains in item history |

**Queue behavior:**

- Sorted by age descending by default (oldest unacknowledged items first)
- Safety-flagged items surface to the top regardless of age
- Items aged >24 hours without acknowledgment appear in FIRES and surface a notification
- Items aged >48 hours without resolution appear in FIRES with a higher-urgency flag
- Nadia can filter by study, escalation type, and age

---

### 3. Milestone Tracker

The portfolio-wide view of upcoming study milestones across all assigned trials. This panel is Nadia's primary tool for leadership reporting on program progress.

Nadia is often asked by senior leadership: "Where is each study against plan?" This panel answers that question directly, organized by horizon and confidence, without requiring Nadia to ask each Study Manager to compile milestone data.

**Panel structure:**

Milestones are organized by time horizon:

**Next 30 days:**
- All milestones across the portfolio due within 30 days
- Displayed with: study name, milestone type, planned date, current confidence (On Track / At Risk / Off Track), and any active risk flags to the timeline

**Next 90 days:**
- All milestones due between 31 and 90 days out
- Same fields; lower urgency visual treatment
- Nadia uses this section for forward planning and for leadership questions about the medium-term program outlook

**Milestone types tracked:**

| Milestone type | Description |
|---------------|-------------|
| Enrollment complete | Last patient enrolled in the study |
| Database lock | All data cleaned and locked for analysis |
| CSR submission | Clinical Study Report submitted to regulatory agency |
| Interim analysis | Planned interim data review point |
| First patient in | Enrollment start — relevant for studies in activation |
| Site activation target | % of target sites activated by a planned date |

**Confidence indicators:**

Each milestone displays a confidence indicator derived from current study health signals:

| Confidence | Definition |
|------------|-----------|
| On Track | No active flags against this milestone; study health signals are consistent with meeting the planned date |
| At Risk | One or more signals suggest the milestone date may slip — e.g., enrollment lag, site activation shortfall, data quality issues creating cleaning backlog |
| Off Track | Study signals indicate a slip is likely or has been confirmed by the Study Manager; date revision may be pending |

**Flagged risks to timeline:**

For any milestone showing At Risk or Off Track, the tracker displays the specific signals driving the flag — e.g., "Enrollment 23% below target pace; current trajectory misses planned enrollment complete by an estimated 6 weeks." These are AI-synthesized from the underlying study health data.

**Leadership reporting use:**

The Milestone Tracker is designed to be screenshot-able or exportable into a format Nadia can use directly in a leadership briefing slide. The visual layout should be legible as a table and should require minimal reformatting for external use.

---

### 4. AI Program Summary

The highest-value feature for this persona.

Nadia currently assembles a portfolio status narrative manually — pulling Study Manager summaries from emails, cross-referencing milestone data from project management tools, and writing a program status document for leadership herself. This takes hours. The AI Program Summary automates the first draft of this document.

**What it produces:**

A weekly AI-generated narrative covering:

| Section | Content |
|---------|---------|
| Overall program status | One-paragraph assessment of the portfolio's health — where studies are against plan, whether systemic risks exist, and whether the program is trending positively or negatively |
| Studies requiring attention | Bulleted summary of any Red or Amber studies, with the primary reason for the health flag and any active escalations |
| Milestone status | Narrative summary of milestone health across the portfolio — which milestones are on track, which are at risk, and any milestone slippage confirmed since the last summary |
| Flagged risks | AI-identified risks that Nadia should be aware of — cross-study patterns, site concentration issues, data quality trends, and any items in her escalation queue that have not yet been resolved |
| Since last summary | Delta section — what changed since the previous AI summary (new escalations, health status changes, milestone confidence shifts). This section is specifically formatted for the "update" use case where Nadia's audience already has prior context |

**Generation cadence:**

The AI Program Summary is generated weekly by default (Thursdays, aligned with status reporting cycles). Nadia can also generate it on-demand at any time via the Actions Ribbon — for example, ahead of an ad hoc leadership call.

**Review and approval workflow:**

1. Summary is generated (auto or on-demand) and appears in Nadia's workspace as a draft requiring review
2. Nadia reads the draft — checking it against the Program Health tiles and Milestone Tracker for accuracy
3. Nadia can edit any section inline, or request a revision from the AI with a comment ("The enrollment section understates the risk — sharpen the language")
4. Nadia approves the draft — approval is logged with Nadia's name, timestamp, and AI-generated flag (audit trail)
5. Approved summary is available for download/export (PDF, DOCX). The platform does not route or send it — Nadia owns delivery through her own communication channels

**Why export-only (not platform-routed):**

This is a deliberate scope decision. See Resolved Design Decisions §2 — AI Summary Routing.

**Design requirement:**

The AI Program Summary must be written in professional prose suitable for a leadership briefing — complete sentences, executive-level language, no platform jargon. It is not a data table or a KPI dashboard. It should read as if a senior analyst assembled it from the platform's data. Nadia should be able to use it with minor edits, not a full rewrite.

---

### 5. Cross-Study Risk Trends

The panel that makes the Program Manager's unique perspective possible. Nadia's most important capability is spotting systemic risk before it becomes a crisis — the kind of risk that no individual Study Manager can see because each SM is looking at only one study.

The Cross-Study Risk Trends panel uses AI to surface patterns that span two or more studies in Nadia's portfolio. It does not ask Nadia to browse study-by-study looking for similarities; it surfaces the pattern to her.

**Pattern types the AI detects and surfaces:**

| Pattern type | Example |
|-------------|---------|
| Cross-study site issue | The same site (or same site management organization) is flagged for data quality issues across 3 studies in the portfolio |
| Regional enrollment underperformance | Sites in a specific country or region are underperforming against enrollment targets across multiple studies — suggests a regional regulatory, logistical, or patient access issue rather than a study-specific problem |
| Protocol or training-related data quality pattern | A specific type of data entry error or protocol deviation is appearing across multiple studies — suggests a shared training gap or protocol design issue rather than a site-specific problem |
| CRO performance pattern | A specific CRO or CRO site group is showing consistent underperformance on query response rates or KRI breach resolution across multiple studies |
| Shared site risk concentration | Multiple studies in the portfolio have significant enrollment or data quality concentration in the same sites — creating portfolio-level dependency risk |

**Panel display per pattern:**

| Field | Description |
|-------|-------------|
| Pattern type | Category label |
| Studies affected | Which studies in the portfolio show this pattern (with tile-style health indicators) |
| AI confidence | High / Medium / Low — how strong is the signal that this is a real pattern vs. coincidence |
| First detected | When the AI first identified this pattern |
| Pattern summary | Two-to-three sentence plain-language description of what the AI observed across studies |
| Recommended action | AI-suggested response — e.g., "Consider a cross-study review of site X's data management practices" or "Escalate regional enrollment shortfall to program leadership" |

**Actions from this panel:**

| Action | Effect |
|--------|--------|
| Assign to Study Manager(s) | Creates an investigation task for one or more SMs to examine the pattern within their study; task appears in SM's WORK PENDING |
| Note for leadership report | Flags this pattern for inclusion in the next AI Program Summary |
| Dismiss | Marks the pattern as acknowledged but not requiring action; pattern is logged and removed from active view; Nadia can explain why she dismissed it (optional note field) |
| Escalate to sponsor (offline) | Same behavior as in the Escalation Queue — logs the action, closes the in-platform item with a note |

**Data model dependency:**

This panel requires AI to detect patterns across multiple studies. This presupposes cross-study data aggregation. See Open Questions §3 — this is flagged as a capability dependency question for engineering.

---

### 6. Study Detail Drill-Down

From any program-level panel, Nadia can drill into a specific study's health detail without navigating to a module. This panel is the execution point for the "three clicks from portfolio to site" design requirement.

**What the drill-down shows:**

When Nadia selects a study (from a tile, a milestone entry, an escalation item, or a risk trend pattern), a study detail view opens inline — not a new page — showing the equivalent of the Study Manager's study health view:

| Section | Content |
|---------|---------|
| Study health snapshot | The same composite RAG breakdown the SM sees — site distribution, query aging summary, KRI adherence rate, milestone status — but in read-only format appropriate for a PM reviewer |
| Open escalations | All items currently in the SM's escalation queue, and all items that have been escalated up to Nadia from this study — with their current status |
| Key signals | Top-3 AI-identified signals for this study — the most important things happening right now that Nadia should be aware of |
| Last SM status summary | The most recently approved AI-generated Study Manager weekly summary — linked directly from the drill-down view |
| Active cross-study patterns | Any Cross-Study Risk Trends (Panel 5) that include this study — shown in context so Nadia can see how this study relates to the pattern |

**Navigation design — "three clicks from portfolio to site":**

The design target is that Nadia can reach a specific site's health detail within three clicks from the Program Health Overview:

1. Click 1 — Click a study tile in Program Health Overview → opens Study Detail Drill-Down
2. Click 2 — Click "View Sites" in the drill-down → opens the study's site list view
3. Click 3 — Click a specific site → opens that site's health card

Every drill-down path introduced in future iterations must be tested against this three-click constraint before being accepted. Navigation paths that require four or more steps to reach site-level detail violate the design principle.

**Read-only access:**

The study detail drill-down is read-only from the Program Manager workspace. Nadia cannot edit risk plans, modify queries, or change site configurations from this view. She can initiate escalation actions (direct response, schedule discussion, escalate to sponsor) and add notes, but she does not access the study's operational management controls.

---

## What the Program Manager Workspace Does NOT Do

To maintain focus and avoid scope creep into adjacent tools and personas:

- **Does not manage individual queries** — query-level review, assignment, and response are CDM and Study Manager responsibilities. Nadia sees query aging as an aggregated health signal, not a list of individual queries she must act on.
- **Does not expose team workloads at the CDM or CM level** — individual workload visibility belongs to the Study Manager workspace. Nadia sees study-level health, not the work queue of any individual contributor.
- **Does not replace portfolio or financial management tools** — budget tracking, resource forecasting, change orders, and contract milestones are managed in dedicated project management and financial systems. No budget or resourcing data appears in this workspace.
- **Does not generate regulatory submission documents** — AI summaries produced in this workspace are operational leadership-briefing aids, not regulatory artifacts. They carry no compliance weight and should not be treated as regulated documents.
- **Does not act as a communication channel to sponsors or senior leadership** — the workspace produces content (AI Program Summary, export) that Nadia uses in her own communication channels. CluePoints does not send or route content to stakeholders outside the platform.
- **Does not provide a single-study operational view** — Nadia does not manage sites, reassign CDM tasks, or modify risk plans from her workspace. Those actions belong to the Study Manager's operational layer.

---

## Information Hierarchy

How information flows to and from the Program Manager workspace within the CluePoints escalation model:

```
External: Senior Leadership / Sponsor
        ↑ (program summary export — Nadia's responsibility, outside platform)
        |
┌──────────────────────────────────────────────────────────────────────┐
│               PROGRAM MANAGER WORKSPACE        ← this brief          │
│                                                                       │
│  Program Health Overview    |  Cross-Study Escalation Queue          │
│  Milestone Tracker          |  AI Program Summary                    │
│  Cross-Study Risk Trends    |  Study Detail Drill-Down               │
│                                                                       │
│  Terminal escalation node — items escalated here that require         │
│  sponsor input exit the platform ("escalate to sponsor offline")     │
└──────────────────────────────────────────────────────────────────────┘
        ↑ (escalations in from Risk Lead and Study Manager)
        |
Risk Lead Workspace
        ↑ (risk governance escalations in)
        |
Study Manager Workspace
        ↑ (operational escalations in)
        |
CDM Workspace          Central Monitor Workspace
```

**The PM workspace is the terminal escalation node within the platform.** Items escalated to Nadia that cannot be resolved by her within the platform are closed with an "escalated to sponsor (offline)" action and exit the platform. There is no escalation path above the Program Manager inside CluePoints. This is a deliberate design boundary — the platform does not attempt to model sponsor-level governance.

**Inbound to PM workspace:**
- Escalations from Study Managers (exceeding SM authority)
- Escalations from Risk Leads (cross-study risk governance)
- AI-detected cross-study patterns requiring PM awareness
- System-generated SLA breach notifications

**Outbound from PM workspace:**
- In-platform: directed responses back to SMs / Risk Leads (logged, visible in their workspaces)
- Out-of-platform: AI Program Summary (export); sponsor escalations (offline, logged as such)

---

## Resolved Design Decisions

### Decision 1 — Portfolio is the only abstraction (RESOLVED 2026-02-23)

**Decision:** Nadia's workspace has no single-study mode. She always sees the portfolio first, and she drills into individual studies from the portfolio view when she needs detail. There is no "switch to single-study view" and no mode where Nadia works exclusively within one study.

**Rationale:** The Program Manager's unique value is cross-study synthesis. If she had a single-study mode, she would be replicating Study Manager functionality in a second persona — creating redundancy without adding value. Her workspace is designed around the questions she uniquely answers: "Which of my studies needs attention?" "Is there a cross-portfolio pattern?" "What do I tell leadership about the overall program?" None of these questions are answered from inside a single study.

**Architectural implication:** The Program Health Overview tiles (Panel 1) are not navigation shortcuts to study module views. They are health tiles that open the Study Detail Drill-Down (Panel 6) inline. Panel 6 is read-only and deliberately limited in depth — enough for Nadia to understand what's happening in a study, not enough for her to manage it. If Nadia determines she needs to take an operational action within a study, her correct path is to contact the Study Manager — not to navigate into study module views herself.

**What this means for the SM's multi-study mode:** The Study Manager workspace includes a Study Triage View for SMs assigned to 2–3 studies. This is NOT the same as the Program Manager workspace. The SM's multi-study view is an operational triage tool; the PM workspace is a governance and synthesis surface. They should not share a UI component or be confused in the design.

---

### Decision 2 — AI Summary Routing (RESOLVED 2026-02-23)

**Decision:** The AI Program Summary is approved by Nadia for use externally. The platform's responsibility ends at approval + export. CluePoints does not route, send, or deliver the approved summary to any external stakeholder — senior leadership, sponsors, or otherwise.

**Rationale:** This is a deliberate scope limit. Attempting to route the summary would require the platform to:
- Model the sponsor's org structure and personnel
- Build a communication channel (email integration, portal, etc.)
- Manage delivery confirmation and response tracking
- Handle the variable formats and protocols different sponsors and leadership teams use

None of these are CluePoints' core competency, and all of them would require integration work that delays delivery of the core value (the AI-generated summary itself). The platform exports professional-quality content; Nadia owns how and where she uses it.

**Implementation:** On approval, the summary becomes available in two ways:
- Download as PDF
- Download as DOCX (editable)

No email send, no in-platform message, no external routing. The "send" step is Nadia's, through her existing channels.

**Connection to SM workflow gap:** This resolves the same gap identified in the SM Workflow Map (Gap 2 — Status Summary Routing). The resolution is consistent across both personas: the platform generates and approves content; delivery is the user's responsibility. This is the Q3 gap from the SM workflow map, resolved here at the program level as a deliberate product stance.

---

### Decision 3 — Decision authority at portfolio level (RESOLVED 2026-02-23)

**Decision:** Nadia is the final escalation endpoint within CluePoints. She cannot escalate within the platform — there is no escalation path above her inside the system. Items that require sponsor-level input or board-level visibility are handled by Nadia through her own external channels, and the action is logged in the platform.

**The "escalate to sponsor (offline)" action:**

When Nadia selects "escalate to sponsor (offline)" on an escalation queue item or a cross-study risk pattern:

1. The platform prompts Nadia for a brief note: what is being escalated, to whom, via what channel (free text, not required)
2. The item is marked as "Escalated to Sponsor" in the platform
3. The item is removed from Nadia's active escalation queue
4. The item remains in the item's full history (accessible via audit log)
5. The escalating party (SM or Risk Lead who raised the item) sees in their workspace: "Item escalated to sponsor by Program Manager — [date]"

**What this does not do:**

- Does not send any communication to the sponsor
- Does not create a task or notification for any sponsor-side user in the platform
- Does not guarantee or track sponsor response

**Rationale:** CluePoints does not have a sponsor-side user model for this workflow at this time. The platform is CRO-side (or sponsor-internal clinical operations). Sponsor-side governance workflows — if they exist — are out of scope for this workspace iteration. This boundary is consistent with the product brief's description of Nadia as a sponsor-side program manager using CluePoints as one of several tools; it does not make CluePoints the sponsor's primary governance system.

**If this assumption is wrong:** If sponsors are confirmed CluePoints platform users (see Open Questions §2), then the "escalate to sponsor (offline)" action would be replaced with an in-platform escalation to a sponsor-side workspace. This would require a sponsor persona brief and significant additional scope.

---

## Open Questions

The following questions remain open before PRD authoring:

| # | Question | Why it matters | Owner |
|---|----------|---------------|-------|
| 1 | Does the Program Manager see data across ALL studies in her therapeutic area, or only studies where she is explicitly assigned as PM? | Portfolio scope definition — affects how tiles are populated, whether Nadia can see a study that was recently assigned without a PM, and how the data access model works | Product |
| 2 | Can sponsors see the Program Manager workspace, or is it CRO-internal? This connects to Stakeholder Question 1 from the SM brief about CRO-side vs. sponsor-side personas — resolve there first, as the answer determines whether the PM workspace is a sponsor tool or a CRO delivery oversight tool | If sponsors are users, the PM workspace content, language, and data access model changes significantly; resolved design decision §3 ("escalate to sponsor offline") would be revisited | Product / Legal |
| 3 | The Cross-Study Risk Trends panel requires AI to detect patterns across multiple studies simultaneously. Does CluePoints have a cross-study data aggregation layer today, or is this a new capability that this workspace would require the platform to build? If it is new, this panel is likely a Phase 2 feature and the MVP scope for the PM workspace must be re-scoped accordingly | Determines whether Cross-Study Risk Trends (Panel 5) is buildable for MVP or must be deferred; affects MVP acceptance criteria | Engineering / Data Architecture |
| 4 | What is the default generation cadence for the AI Program Summary — weekly (Thursday, aligned with SM summary), bi-weekly (aligned with Nadia's typical login cadence), or always on-demand? Should it auto-generate on a schedule, or should Nadia always trigger it manually? | Determines the notification model and whether Nadia discovers the summary or it appears proactively; a bi-weekly auto-generation may be better aligned with her actual usage than weekly | UX Research / Product |
| 5 | Does the Milestone Tracker pull milestone data from a CTMS, from manually entered data in CluePoints, or from Study Manager-managed entries in the platform? If the source is a CTMS, this is an integration dependency that could gate whether this panel is buildable at all for MVP | Determines the data dependency for Panel 3; if milestone data is not in CluePoints and requires a CTMS integration, Milestone Tracker may need to be descoped from MVP or replaced with a lighter version that only surfaces milestones Study Managers have manually entered | Engineering / Data |

---

## 3-Area Workspace Structure

The Program Manager workspace maps to the same 3-area model as all other workspace personas:

```
┌──────────────────────────────────────────────────────────────────────┐
│  FIRES                                                               │
│  Studies that changed RAG status since last login                   │
│  Escalations from Risk Lead / Study Manager aged > 24 hours         │
│  Critical milestone confidence drops (On Track → At Risk / Off Track)│
│  Cross-study patterns newly detected by AI since last login         │
├──────────────────────────────────────────────────────────────────────┤
│  ACTIONS RIBBON                                                      │
│  Generate Program Summary  |  Drill Into Study  |  Export Report    │
│  Acknowledge Escalation    |  Search Portfolio  |  Filter by Status  │
├──────────────────────────────────────────────────────────────────────┤
│  WORK PENDING                                                        │
│  Program Health Overview tiles (full portfolio)                     │
│  Cross-Study Escalation Queue (non-urgent items)                    │
│  Milestone Tracker (30-day and 90-day horizons)                     │
│  Cross-Study Risk Trends review                                     │
│  AI Program Summary drafts awaiting review and approval             │
└──────────────────────────────────────────────────────────────────────┘
```

**FIRES — the delta view is critical for this persona:**

Because Nadia may go several days or a week between logins, the FIRES area must communicate change, not just state. A study showing Amber is not a fire. A study that went from Green to Amber since her last login is a fire. Every element in the FIRES area must carry a delta dimension anchored to Nadia's last login timestamp.

Specific FIRES triggers:

| Trigger | Source |
|---------|--------|
| Study RAG change (any direction) since last login | Program Health Overview (Panel 1) |
| New escalation item in queue, unacknowledged for > 24 hours | Cross-Study Escalation Queue (Panel 2) |
| Milestone confidence drop (On Track → At Risk, or At Risk → Off Track) | Milestone Tracker (Panel 3) |
| AI Program Summary auto-generated and awaiting review | AI Program Summary (Panel 4) |
| New cross-study risk pattern detected since last login | Cross-Study Risk Trends (Panel 5) |

**ACTIONS RIBBON — Nadia's verbs:**

| Action | Description |
|--------|-------------|
| Generate Program Summary | Triggers on-demand AI Program Summary generation; surfaces draft in workspace |
| Drill Into Study | Opens the Study Detail Drill-Down (Panel 6) for a selected study |
| Acknowledge Escalation | Marks an escalation item as reviewed without requiring full resolution |
| Export Report | Exports the approved AI Program Summary or Milestone Tracker as PDF / DOCX |
| Search Portfolio | Search across the portfolio by study name, site name, or escalation item keyword |
| Filter by Status | Quick-filter the Program Health tiles by RAG status (Red only, Red + Amber, All) |

---

## Acceptance Criteria (MVP)

The Program Manager workspace is considered complete for MVP when:

**Program Health Overview (Panel 1):**
- [ ] Nadia logs in and sees one tile per assigned study without navigating to any module
- [ ] Each tile displays: study name, phase, composite health RAG, RAG delta since last login, open escalation count, next milestone with confidence, last-updated timestamp, and Study Manager name
- [ ] Tiles are sorted by health status (Red first) by default; Nadia can re-sort by study name, escalation count, and milestone proximity
- [ ] Clicking a study tile opens the Study Detail Drill-Down inline without navigating away from the portfolio view

**Cross-Study Escalation Queue (Panel 2):**
- [ ] All escalation items from Study Managers and Risk Leads across Nadia's portfolio appear in the queue
- [ ] Each item displays: originating study, escalating party, escalation type, plain-language summary, age, and prior actions taken
- [ ] Nadia can acknowledge, respond directly, schedule discussion, or log an "escalate to sponsor (offline)" action inline — without leaving the workspace
- [ ] "Escalate to sponsor (offline)" action closes the item in-platform with a timestamped note; the escalating party sees the status update in their workspace
- [ ] Items aged > 24 hours without acknowledgment appear in FIRES
- [ ] All actions are logged with actor, timestamp, and action type for audit trail

**Milestone Tracker (Panel 3):**
- [ ] All milestones across Nadia's portfolio are displayed, organized into Next 30 Days and Next 90 Days horizons
- [ ] Each milestone shows: study name, milestone type, planned date, confidence indicator (On Track / At Risk / Off Track), and flagged risk notes
- [ ] Milestones showing At Risk or Off Track include an AI-synthesized explanation of the signals driving the flag
- [ ] Panel is exportable in a format usable for leadership reporting (conditional on data source resolution — see Open Question 5)

**AI Program Summary (Panel 4):**
- [ ] Weekly auto-generation of AI Program Summary occurs on a configured schedule; Nadia receives a FIRES notification when a new draft is ready
- [ ] On-demand generation is available from the Actions Ribbon at any time
- [ ] Summary covers all required sections: overall program status, studies requiring attention, milestone status, flagged risks, and delta since last summary
- [ ] Nadia can edit any section inline or request an AI revision with a comment
- [ ] Approval action is available; approval is logged with Nadia's name, timestamp, and AI-generated flag
- [ ] Approved summary is downloadable as PDF and DOCX; no platform-initiated routing or sending occurs
- [ ] Summary prose is written at executive communication quality — complete sentences, leadership-appropriate language, no platform jargon

**Cross-Study Risk Trends (Panel 5):**
- [ ] AI-detected cross-study patterns are displayed with: pattern type, affected studies, AI confidence level, first detection date, pattern summary, and recommended action
- [ ] Nadia can assign a pattern to Study Manager(s) for investigation, note it for the leadership report, dismiss with an optional note, or escalate to sponsor (offline)
- [ ] Newly detected patterns since last login appear in FIRES
- [ ] Dismiss action removes the pattern from active view but retains it in item history
- [ ] (Conditional on Open Question 3: if cross-study data aggregation is not available at MVP, this panel may be deferred to Phase 2)

**Study Detail Drill-Down (Panel 6):**
- [ ] Nadia can reach a study's health detail from any program-level panel with one click
- [ ] Drill-down shows: study health snapshot (composite RAG, site distribution, query aging, KRI adherence, milestone status), open escalations, top-3 AI key signals, last approved SM status summary, and active cross-study patterns involving this study
- [ ] Nadia can reach a specific site's health card within three clicks from the Program Health Overview (Portfolio → Study Drill-Down → Site List → Site Card)
- [ ] Drill-down is read-only; Nadia cannot modify operational data from this view
- [ ] All escalation actions available from Panel 2 are also accessible from within the drill-down view

**Delta and FIRES behavior (all panels):**
- [ ] All FIRES items carry a delta indicator anchored to Nadia's last login timestamp — showing what changed, not just the current state
- [ ] A study tile showing a RAG change since last login is visually distinct from a tile showing the same RAG as the last login
- [ ] FIRES area is empty (or shows a "no new changes since last login" confirmation) when nothing has changed — not silently blank

**Audit and access:**
- [ ] All actions taken from the workspace are logged with actor, timestamp, source item, and action type
- [ ] Nadia sees only studies she is assigned to as Program Manager (scope controlled by role-based access)
- [ ] Workspace respects existing CluePoints data access permissions for each study — Nadia does not see study data she was not already authorized to access

---

*Document created: 2026-02-23*
*Parent: product-brief-Testing-2026-02-22.md*
*Next step: PRD authoring — Program Manager workspace functional requirements*
*Related: feature-brief-study-manager-workspace-2026-02-23.md, sm-workflow-map-2026-02-23.md*
