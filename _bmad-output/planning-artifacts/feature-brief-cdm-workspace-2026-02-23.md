---
date: 2026-02-23
author: Root
parent: product-brief-Testing-2026-02-22.md
persona: Clinical Data Manager
status: draft
---

# Feature Brief: Clinical Data Manager (CDM) Workspace
## CluePoints Integrated Platform — User-Centric Workspace

---

## Overview

The Clinical Data Manager is the primary executor in the clinical oversight chain. Unlike the Study Manager — who aggregates signals and makes governance decisions — or the Central Monitor — who interprets population-level statistical patterns — the CDM works at the level of individual queries, specific data records, and concrete site interactions. Her work is high-volume, time-sensitive, and query-centric. The workspace must serve her accordingly.

The CDM workspace must serve two simultaneous functions:

1. **Triage surface** — cutting through the volume of open queries, site signals, and protocol deviations she is responsible for and surfacing the right things in the right order so she always knows what to do next
2. **Execution surface** — allowing her to respond to queries, review site anomalies, and trigger AI assistance directly from the workspace without module navigation

This is not a governance workspace. The CDM does not approve risk plans, manage team workloads, or own risk tier decisions. Those responsibilities belong to the Study Manager and Risk Lead. The CDM workspace is deliberately scoped to what she can and must act on herself — with clear escalation paths to those who own what she cannot.

The defining design challenge for this workspace is **volume management without information loss**. A CDM managing 3–6 concurrent trials may have 40–80 open queries at any given time, across 10–20 assigned sites. The workspace must make this manageable through intelligent prioritization — not by hiding items, but by surfacing them in the right order with enough context to act quickly.

---

## Persona Recap

**Sarah** — Clinical Data Manager at a mid-size CRO, responsible for data oversight across 3–6 concurrent Phase II/III trials. She works in CluePoints daily, and CluePoints is her primary operational tool — not a supplementary dashboard.

**Access pattern:** Daily, often multiple sessions. Morning session for triage and priority query work; afternoon for site review and escalation follow-up. High-frequency interaction with query management and site risk data.

**Reports to:** Study Manager (on each assigned study)

**Works alongside:** Central Monitor (receives anomaly signals from CM's site analysis), Medical Reviewer (escalates safety-relevant deviations upward)

**Key tensions:**

- Manages a high volume of queries across multiple studies simultaneously — without a unified view, she reconstructs context from scratch each session
- Responsible for timely query response but dependent on site coordinators who may be slow to respond; her SLA clock runs regardless
- Expected to flag site issues early but must distinguish between genuine anomalies and routine data noise — without always having the statistical context to do so
- AI-generated query suggestions exist in the query module today but are buried — she doesn't see them during her regular workflow
- When she escalates to the Study Manager, she needs acknowledgment; currently she has no visibility into whether her escalations have been received or acted on

**What success looks like:** Sarah opens CluePoints and within 30 seconds understands her top priorities across all her assigned studies. She can respond to an overdue query, review a site anomaly signal, trigger an AI agent to draft responses for lower-priority queries, and track a pending escalation — all without leaving the workspace. Her day starts with direction, not navigation.

---

## What the CDM Workspace Must Deliver

### 1. Query Queue

The primary operational panel. The CDM lives in query management — this panel is the workspace representation of her core daily work. It must handle volume intelligently and surface the right queries first.

**Required elements:**

| Element | Description |
|---------|-------------|
| Query list | All queries assigned to Sarah, across all her studies, in a single prioritized list |
| Overdue indicator | Queries past their response SLA, displayed at the top of the queue; days overdue shown per item |
| Safety flag | Queries associated with a safety-relevant data issue or adverse event flagged visually (distinct from standard overdue indicators) |
| Per-query context | For each item: study name, site identifier, subject ID (masked per configuration), query text, date raised, date due, current status |
| Filter/sort controls | Filter by study, site, status (open / awaiting site response / pending CDM review), query type; sort by priority, age, site |
| Inline response | CDM can draft and submit a query response directly from this panel without navigating to the query management module |
| AI draft indicator | Queries for which an AI agent has prepared a draft response are visually marked; draft is accessible inline |

**Priority ordering logic:**

1. Safety-flagged queries (regardless of age)
2. Overdue queries (sorted by days overdue, descending)
3. Queries approaching SLA — due within 24 hours
4. Standard open queries (sorted by age, oldest first)
5. Queries awaiting site response (visible but deprioritized — no CDM action required yet)

**Key actions from this panel:**

- **Respond inline** — open query response composer directly in the panel; submit response without leaving workspace
- **Review AI draft** — view AI-generated response draft; edit, approve, or reject
- **Assign to site** — (re)assign query to a specific site contact
- **Escalate** — flag a query for Study Manager attention with one click and a required comment
- **Mark as pending site** — indicate a response has been sent and CDM is awaiting site reply; removes from CDM's active action set
- **Bulk trigger AI drafting** — select multiple queries and request AI-drafted responses in one action

**What this panel does NOT do:**

- Does not create new queries (query creation belongs in the query management module)
- Does not show queries assigned to other CDMs on the same study (Sarah sees her assigned queue only — see Open Question 1)
- Does not surface queries in a read-only status with no pending CDM action unless Sarah explicitly expands the view

---

### 2. Site Anomaly Feed

The CDM is often the first person who should notice that something is wrong at a site — before it becomes a KRI breach or a formal monitoring finding. This panel surfaces anomalous signals from the sites assigned to Sarah, drawn from RBQM outputs, enrollment tracking, and data pattern analysis.

**Required elements:**

| Element | Description |
|---------|-------------|
| Anomaly list | Sites assigned to Sarah showing one or more anomalous signals, sorted by severity |
| Signal type tags | Each anomaly is categorized: KRI signal, enrollment anomaly, data pattern flag, query aging anomaly, protocol deviation rate |
| Severity ranking | A composite severity score determines list order — safety-adjacent signals rank first, statistically significant deviations rank above borderline signals |
| Study and site context | Study name, site identifier, site name, and the specific signal that triggered the flag |
| Signal age | How long the anomaly has been active; new signals (first appearance since last login) are visually distinguished |
| Trend indicator | Whether the signal is worsening, stable, or improving since it was first flagged |
| Prior action log | Whether any prior action has been taken on this site by Sarah or another team member |

**Anomaly signal types included in this panel:**

| Signal type | Source | Description |
|-------------|--------|-------------|
| KRI threshold breach | RBQM module | A key risk indicator for this site has crossed a defined threshold |
| KRI approaching threshold | RBQM module | A KRI is within a defined proximity band of its threshold (configurable — default: 80% of threshold) |
| Enrollment anomaly | Enrollment tracking | Site enrollment rate is outside expected range (above or below) relative to study plan |
| Data entry lag | EDC integration | Subject visit data has not been entered within expected window since visit date |
| Query aging anomaly | Query management | This site's query response time is significantly above study average |
| Protocol deviation spike | PD tracking | Site has logged more protocol deviations in the past 30 days than their historical baseline or study average |
| Data pattern flag | RBQM / statistical module | Central monitoring has identified a statistical anomaly in this site's data (e.g., unexpected uniformity, outlier distributions) |

**Key actions from this panel:**

- **Open site detail** — expand inline to see the full signal context for the site: KRI values, enrollment chart, query aging trend, recent deviation log
- **Trigger AI site summary** — request an AI-generated narrative summarizing the site's anomalous signals, prior actions, and recommended next step (see Panel 3)
- **Raise a query** — if the anomaly warrants a new query to the site, launch query creation pre-populated with site context (navigates to query module with context carried over)
- **Add a site note** — log an observation or action taken, attached to the site record
- **Escalate to Central Monitor or Study Manager** — flag the site for attention from a higher-authority role, with a required comment (see Panel 5)
- **Acknowledge and monitor** — mark a signal as "acknowledged — monitoring" to indicate Sarah has seen it and is tracking without immediate action; removes from primary feed position but remains visible in expanded view

**What this panel does NOT do:**

- Does not show sites assigned to other CDMs on the same study
- Does not perform statistical analysis — it surfaces outputs from the RBQM and statistical modules; it does not do independent signal computation
- Does not show all sites Sarah is assigned to — only those with an active anomalous signal. Sites with no current anomaly are visible through search or module navigation, not in this feed.

---

### 3. AI Agent Surface

The CDM is the persona most immediately served by AI assistance. Her work is high-volume and procedural enough that AI can meaningfully reduce her load — particularly in query response drafting, where the same types of queries recur across studies and sites. This panel is the CDM's interface to the platform's AI agent capabilities.

**AI agents available to the CDM from this workspace:**

| Agent | Trigger | What it produces |
|-------|---------|-----------------|
| Query Response Drafter | On-demand from Query Queue or bulk selection | Draft responses for one or more selected queries, based on query text, site history, protocol context, and prior similar query resolutions |
| Data Cleaning Opportunity Finder | On-demand from Actions Ribbon | A ranked list of data records across Sarah's assigned studies that have potential data quality issues (missing fields, implausible values, entry inconsistencies) — prioritized by study and subject |
| Site Anomaly Summarizer | On-demand from Site Anomaly Feed, per site | A narrative summary of a flagged site's anomalous signals: what the signals are, how long they have been active, what prior actions have been taken, and a recommended next step |
| Protocol Deviation Digest | On-demand from Protocol Deviation Tracker | A structured summary of open protocol deviations on Sarah's assigned sites, grouped by severity and site, with resolution status and aging |

**AI interaction model — Query Response Drafter (detailed):**

This is the highest-value and highest-risk AI workflow for the CDM. The interaction must be explicit and auditable.

```
Step 1 — Trigger
  Sarah selects one or more queries from the Query Queue and clicks
  "Draft AI Response" (or uses the bulk "Request AI drafts" action).

Step 2 — Agent activation
  Workspace shows agent status: "Drafting responses for [N] queries —
  estimated [time]." Sarah can continue working; she does not have to wait.

Step 3 — Draft available
  When drafts are ready, a notification appears in the workspace
  (FIRES area if overdue, Work Pending if standard priority).
  The Query Queue marks each drafted query with an AI draft indicator.

Step 4 — CDM review
  Sarah opens each drafted response inline. She sees:
    - The original query text
    - The AI-generated draft response
    - The confidence level (if applicable) and the basis for the draft
      (e.g., "Based on protocol section 4.2 and prior similar query
      at Site 012 resolved on [date]")
    - Edit controls — she can modify any part of the draft inline

Step 5 — CDM approval or rejection
  Sarah either:
    a) Approves as-is → response is queued for submission
    b) Edits and approves → modified response queued for submission
    c) Rejects → draft is discarded; query returns to standard queue

Step 6 — Submission
  Approved responses are submitted to the site through the query
  management system. The submission record includes:
    - AI-generated flag (visible in audit trail)
    - CDM's approval timestamp and identity
    - Whether the response was modified before approval

CONSTRAINT: No AI-drafted response is submitted to a site without
explicit CDM approval at Step 5. The system provides no mechanism
for auto-submission of AI drafts.
```

**AI interaction model — all other agents:**

The same review-before-action principle applies to all agents:

- AI outputs are always presented as drafts or recommendations, never as finalized records
- Sarah must explicitly approve or act on AI output before it has any effect on site-facing data, query records, or escalation logs
- All AI-generated content that Sarah approves is flagged as AI-assisted in the audit trail, with Sarah's approval timestamp

**Agent status visibility:**

The AI Agent Surface also shows a compact status view of currently running and recently completed agent tasks:

| Status | Display |
|--------|---------|
| Running | Agent name, triggered-at timestamp, estimated completion |
| Awaiting review | Agent name, completion timestamp, count of items needing review |
| Completed | Agent name, completion timestamp, count of items approved / rejected / submitted |
| Failed | Agent name, failure reason (surface-level), option to retry |

---

### 4. Protocol Deviation Tracker

Protocol deviations (PDs) are a distinct and significant part of the CDM's workload. Unlike queries — which are requests for site clarification or correction — protocol deviations are documented instances of non-compliance with the study protocol. They require categorization, follow-up, and in some cases escalation to the medical reviewer or study manager.

**Required elements:**

| Element | Description |
|---------|-------------|
| Open deviation list | All open protocol deviations on sites assigned to Sarah |
| Severity categorization | Each deviation categorized by severity: Major (potential patient safety or data integrity impact), Minor (no significant impact), Administrative |
| Resolution status | Status per deviation: open, under investigation, resolved pending confirmation, closed |
| Aging | Days since deviation was logged; deviations open beyond SLA are highlighted |
| Root cause tag | If root cause has been identified, the assigned category is shown (e.g., protocol misunderstanding, site staff error, equipment failure) |
| Site and study context | Study, site, subject ID (masked per configuration), deviation description |
| Action history | Log of prior actions taken on each deviation (notes, queries raised, escalations) |

**Severity display logic:**

- Major deviations are always shown at the top of the list, regardless of age
- Major deviations with patient safety implications are further flagged with a safety indicator consistent with the Query Queue's safety flag treatment
- Minor and administrative deviations are sorted by age (oldest first)

**Key actions from this panel:**

- **Add resolution note** — log an action, observation, or update against a specific deviation
- **Raise a query** — if the deviation requires clarification from the site, initiate a query pre-populated with the deviation context
- **Escalate** — escalate a major deviation to the Study Manager or Medical Reviewer (for safety-relevant deviations) via the Escalation Surface (Panel 5)
- **Close deviation** — mark a deviation as resolved and closed; requires a required resolution comment
- **Request AI deviation digest** — trigger the Protocol Deviation Digest agent (Panel 3) to generate a summary of all open deviations

**What this panel does NOT do:**

- Does not allow Sarah to create protocol deviations (deviation recording is initiated at the site or through the appropriate module)
- Does not adjudicate severity — severity classification is assigned by protocol and organizational policy, not by this panel; the panel displays, it does not classify
- Does not show deviations on sites not assigned to Sarah

---

### 5. Escalation Surface

The CDM sits in the middle of the escalation chain — she receives signals from site data and anomaly detection, and she escalates to the Central Monitor and Study Manager when issues exceed her scope or authority. This panel is the bidirectional escalation interface: outbound escalations she has raised, and inbound acknowledgments from those she escalated to.

**Outbound escalations (CDM to Central Monitor or Study Manager):**

| Element | Description |
|---------|-------------|
| Escalation list | All open outbound escalations Sarah has raised, across all her assigned studies |
| Recipient | Who the escalation was sent to (Central Monitor, Study Manager) |
| Subject | The originating item — a site anomaly, a query, a protocol deviation |
| Status | Pending (not yet acknowledged), Acknowledged, In review, Resolved, Returned with comment |
| Age | Time since escalation was raised; escalations unacknowledged for >24 hours are highlighted |
| Resolution note | If the escalation has been resolved or returned, the resolution note from the recipient is shown |

**Outbound escalation initiation flow:**

Escalation can be initiated from any panel in the workspace — Query Queue, Site Anomaly Feed, or Protocol Deviation Tracker — via a consistent "Escalate" action. When triggered:

1. Sarah selects the recipient role: Central Monitor (for site anomaly or statistical signal questions) or Study Manager (for issues requiring governance or resource decisions)
2. The system pre-populates the escalation record with the originating item context
3. Sarah adds a required comment explaining why she is escalating
4. The escalation is submitted and appears in the recipient's workspace (Central Monitor or Study Manager Decision Queue)
5. The item appears in Sarah's outbound escalation list with "Pending" status

**Inbound acknowledgments:**

When a recipient acknowledges, acts on, or returns Sarah's escalation, the update appears in this panel and triggers a workspace notification. Sarah can see:

- What action was taken on her escalation
- Any comments from the recipient
- Whether the item has been resolved or whether it requires further input from her

**Escalation SLAs (configurable per organization):**

- Outbound to Central Monitor: expected acknowledgment within 8 hours
- Outbound to Study Manager: expected acknowledgment within 4 hours (Study Manager SLA from SM workspace brief)
- If acknowledgment does not occur within the SLA window, Sarah receives a workspace notification and the escalation is visually flagged

**What this panel does NOT do:**

- Does not allow Sarah to escalate directly to the Risk Lead or Program Manager — those escalation paths belong to the Study Manager
- Does not show escalations raised by other CDMs on the same study
- Does not replace study-level risk governance; escalation through this surface is an operational handoff, not a formal risk record

---

## What the CDM Workspace Does NOT Do

To maintain focus and prevent scope creep:

- **Does not manage team workloads** — Sarah does not see other CDMs' query queues, workload depth, or SLA performance. Team workload visibility is a Study Manager function. The CDM workspace is scoped entirely to Sarah's own assigned work.
- **Does not own risk governance** — KRI threshold configuration, risk plan creation, and site risk tier decisions are the domain of the Risk Lead and Study Manager. Sarah sees the outputs of risk decisions (KRI signals, site tier indicators) but does not configure or adjudicate them.
- **Does not perform statistical analysis** — the platform's RBQM and central monitoring modules compute the signals that surface in Sarah's Site Anomaly Feed. The CDM workspace displays those signals; it does not generate them or allow Sarah to modify the underlying analytical logic.
- **Does not show patient-level clinical data** — individual adverse events, lab values, and clinical narratives are accessed in the relevant module. The CDM workspace shows query and deviation context at the level of site, subject ID, and data field — not the full clinical record.
- **Does not surface financial or contractual information** — budget, site payment status, and contract milestones are out of scope.
- **Does not manage site activation** — site initiation, regulatory submission status, and investigator qualification are managed in the CTMS and are not surfaced here.
- **Does not generate regulatory submission documents** — AI-generated summaries are operational aids. Nothing the CDM workspace produces is intended for regulatory filing.
- **Does not expose other CDMs' work** — Sarah's workspace is scoped to her assigned studies and her assigned sites within those studies. Cross-CDM workload comparison, reassignment between CDMs, and team-level views are Study Manager functions.

---

## Information Hierarchy

How information flows to and from the CDM workspace:

```
                    Study Manager Workspace
                            ↑ (escalations out — governance decisions,
                            │  issues beyond CDM authority)
                            │
                    Central Monitor Workspace
                            ↑ (escalations out — site anomalies requiring
                            │  statistical interpretation or CM authority)
                            │
        ┌───────────────────────────────────────────┐
        │           CDM WORKSPACE                   │  ← this brief
        │                                           │
        │  Query Queue      │ Site Anomaly Feed      │
        │  AI Agent Surface │ Protocol Dev. Tracker  │
        │  Escalation Surface                        │
        └───────────────────────────────────────────┘
                ↑                          ↑
                │                          │
        Query Management            RBQM / Central Monitoring
        module (query records,      module (KRI signals, enrollment
        response history,           anomalies, data pattern flags,
        SLA tracking)               site risk tiers)
                ↑
                │
        Site / EDC
        (data entry, deviation
        reporting, query responses)
```

**Signal flow summary:**

- **Into CDM workspace from below:** Query records and SLA status from query management; KRI signals, enrollment anomalies, and data pattern flags from RBQM and central monitoring outputs; protocol deviation records from deviation tracking
- **Out of CDM workspace upward:** Escalations to Central Monitor (for site anomalies requiring CM interpretation) and to Study Manager (for governance decisions, resource issues, or issues beyond CDM authority)
- **Bidirectional:** Query response drafts (CDM authors → site receives); escalation acknowledgments (SM / CM sends back to CDM)

---

## Resolved Design Decisions

### Q1 — Multi-study mode: CDMs frequently manage 3–6 studies simultaneously (RESOLVED 2026-02-23)

**Decision:** The CDM workspace must support both single-study and multi-study modes, resolved in the same architectural pattern established for the Study Manager workspace.

**Single-study mode:** When Sarah is assigned to exactly one active study, the workspace loads directly into the full single-study CDM view described in this brief: Query Queue, Site Anomaly Feed, AI Agent Surface, Protocol Deviation Tracker, and Escalation Surface — all scoped to that one study.

**Multi-study mode (2–6 studies):** When Sarah is assigned to more than one active study, the workspace defaults to a **Study Triage View** as the landing experience. This view contains:

| Element | Description |
|---------|-------------|
| Study health tiles | One tile per assigned study, showing: total open queries (with overdue count highlighted), active site anomaly count, open major protocol deviations, and the most urgent single item requiring Sarah's action |
| Cross-study Query Queue | Unified query list showing all overdue and safety-flagged queries across all studies, sorted by the same priority logic as the single-study Query Queue — safety first, overdue first, approaching SLA next |
| Cross-study anomaly summary | Count of active site anomaly signals per study, with the highest-severity signal per study surfaced directly on the tile |
| AI daily triage note | An AI-generated natural language summary of where Sarah's attention is most needed today, across all her studies (e.g., "Study A has 4 overdue queries including one safety-flagged item. Study C has a new KRI breach at Site 007 that was not present yesterday.") |
| Study-switcher | A persistent control available at all times in the workspace that allows Sarah to jump into the full single-study workspace view for any of her assigned studies |

**Mode detection:** Mode (single vs. multi-study) is determined automatically by the number of active studies assigned to Sarah. No user configuration is required. If Sarah is mid-session in single-study mode and a new study is assigned to her, the workspace promotes to multi-study mode on her next login.

**Design constraint for multi-study mode:** The cross-study triage view is a surface for prioritization and urgent action — not a full multi-study management interface. It surfaces the top of each study's queue to enable rapid triage, after which Sarah switches into a single-study context to do the actual work. The intention is to give her situational awareness across studies in under 2 minutes, then direct her attention to the highest-priority study.

**Scope note:** The multi-study CDM triage view is distinct from the Program Manager's portfolio view and the Study Manager's multi-study view. The CDM's cross-study view is entirely query- and execution-focused; it does not show team workloads, risk governance items, or cross-study analytical aggregations.

---

## Open Questions

The following questions are design-blocking and must be resolved before PRD authoring for the CDM workspace:

| # | Question | Why it matters | Owner |
|---|----------|----------------|-------|
| 1 | **Who assigns queries to CDMs?** Is assignment driven by site assignment (all queries from Sarah's sites go to Sarah automatically), manual assignment by the Study Manager, or a configurable routing rule? | Directly determines what appears in Sarah's Query Queue. If assignment is manual, the queue may be incomplete. If assignment is automatic by site, the scope of the queue is well-defined. | Product / Platform |
| 2 | **Does the CDM workspace show all queries on her assigned sites, or only queries explicitly assigned to her?** There is a meaningful difference: a site may have 12 open queries, but only 4 may be assigned to Sarah specifically. Does she see all 12 (full site picture) or only her 4 (personal workload)? | Affects volume calibration and design of the Query Queue — a "full site queries" view requires different filtering and context-labeling than a "my assigned queries" view | Product |
| 3 | **Can CDMs see each other's queues — even read-only?** If Sarah and a colleague are both assigned to the same study, can Sarah see that her colleague has an overdue query at a shared site? Or is the CDM workspace strictly personal-workload-only? | Affects whether the workspace can surface coverage gaps at the site level. Has privacy and workload-pressure implications. | Product / Legal |
| 4 | **AI query response drafting — what approval chain is needed before a CDM-approved draft is submitted to the site?** Does Sarah's approval suffice, or does the Study Manager need to countersign AI-drafted responses before site submission? | Critical for the AI interaction model. If SM countersignature is required, the Query Queue workflow changes significantly — the approved draft enters a pending-SM-review state before submission, not immediate submission. | Product / Regulatory / Legal |
| 5 | **Who generates the site anomaly signals that appear in Sarah's feed — is this always a Central Monitor output, or can the RBQM module generate them independently?** | Determines whether the Site Anomaly Feed is always downstream of a CM's analysis, or whether it is an automated output from the RBQM system that surfaces even before the CM reviews it. Affects the authority and interpretation of the signals. | Product / Engineering |
| 6 | **How are protocol deviations entered into the system — by the site directly, by the CDM, or by both?** The Protocol Deviation Tracker panel assumes Sarah sees deviations that she did not necessarily create. Is that correct? | Determines whether this panel is a full read-write interface or primarily a read-and-act interface for Sarah. | Product |
| 7 | **Can Sarah initiate escalation directly to the Medical Reviewer for safety-flagged items, or must she route through the Study Manager?** The current brief routes all CDM escalations to either Central Monitor or Study Manager. If safety-flagged deviations require direct CDM-to-Medical-Reviewer escalation, the Escalation Surface scope must expand. | Affects escalation routing logic and the permission model for which roles the CDM can contact directly. | Product / Regulatory |

---

## Acceptance Criteria (MVP)

The CDM workspace is considered complete for MVP when all of the following criteria are met:

**Single-study mode — Query Queue:**
- [ ] Sarah can log in and immediately see her full assigned query queue, sorted with safety-flagged queries first, overdue queries second (sorted by days overdue), and approaching-SLA queries third
- [ ] Each query in the queue shows: study name, site identifier, query text, date raised, date due, days overdue (if applicable), and current status
- [ ] Sarah can draft and submit a query response inline from the Query Queue without navigating to the query management module
- [ ] Queries for which an AI agent has prepared a draft are visually indicated; the draft is accessible inline with the original query text and the draft response visible side by side
- [ ] Sarah can approve an AI draft as-is, edit and approve, or reject; approved responses are submitted only after explicit CDM approval action
- [ ] Each submitted response — whether CDM-authored or AI-drafted — is recorded with actor identity, timestamp, and AI-assisted flag in the audit trail
- [ ] Sarah can bulk-select multiple queries and request AI draft responses in one action; agent status is visible in the AI Agent Surface panel

**Single-study mode — Site Anomaly Feed:**
- [ ] Sarah can see all active anomalous signals on her assigned sites, ranked by severity (safety-adjacent signals first)
- [ ] Each anomaly entry shows: study name, site identifier, signal type, signal age, trend indicator (worsening / stable / improving), and whether prior action has been taken
- [ ] New signals (first appearance since last login) are visually distinguished from previously known signals
- [ ] Sarah can acknowledge a signal and mark it as "monitoring" from the feed; acknowledged items move out of the primary position but remain accessible in the expanded view
- [ ] Sarah can trigger an AI site anomaly summary from the feed for any flagged site; the summary is produced by the AI agent and presented for review before being logged or shared

**Single-study mode — AI Agent Surface:**
- [ ] The AI Agent Surface shows currently running, awaiting-review, recently completed, and failed agent tasks
- [ ] Sarah can trigger the Data Cleaning Opportunity Finder agent from the Actions Ribbon; output is presented as a ranked list of potential data quality issues for Sarah's review — no records are modified without Sarah's action
- [ ] Sarah can trigger the Protocol Deviation Digest agent; output is presented as a draft summary for Sarah's review and approval before being logged
- [ ] No AI agent output — draft query response, site summary, deviation digest, or data cleaning recommendation — takes any system action without explicit CDM approval

**Single-study mode — Protocol Deviation Tracker:**
- [ ] Sarah can see all open protocol deviations on her assigned sites, sorted with Major deviations first (safety-flagged Major deviations at the very top), then Minor, then Administrative
- [ ] Each deviation entry shows: study, site, subject ID, severity, description, resolution status, days open, and action history
- [ ] Sarah can add a resolution note, close a resolved deviation (with required comment), escalate from this panel, or raise a linked query — all without navigating out of the workspace

**Single-study mode — Escalation Surface:**
- [ ] Sarah can initiate an escalation to Central Monitor or Study Manager from any workspace panel; the escalation record is pre-populated with the originating item context and requires a CDM comment before submission
- [ ] Sarah can see the status of all her open outbound escalations: pending, acknowledged, in review, resolved, or returned with comment
- [ ] When a recipient acknowledges or acts on an escalation, Sarah receives a workspace notification and the status updates in the Escalation Surface panel
- [ ] Escalations unacknowledged past the configured SLA window are highlighted and trigger a workspace notification to Sarah

**Multi-study mode (2 or more studies assigned):**
- [ ] Workspace automatically promotes to Study Triage View when Sarah is assigned to more than one active study; single-study mode resumes automatically if she drops to one study
- [ ] Study tiles in the Triage View show per-study: open query count, overdue query count, active site anomaly count, open Major protocol deviations, and the single most urgent item requiring action
- [ ] Cross-study Query Queue in the Triage View surfaces all overdue and safety-flagged queries across all of Sarah's studies, applying the same priority logic as the single-study queue
- [ ] An AI-generated daily triage note is available from the Triage View and accurately summarizes where Sarah's attention is most needed today across her studies
- [ ] The study-switcher is accessible from any point in the workspace and navigates Sarah into the full single-study workspace for any of her assigned studies
- [ ] Actions taken from the Triage View (inline query response, acknowledgment, escalation) are recorded in the same audit trail as actions taken from the single-study view

**Both modes — cross-cutting requirements:**
- [ ] All actions taken from the CDM workspace are logged with: actor identity, timestamp, source item, and action type — meeting the audit trail requirements of 21 CFR Part 11 / ICH E6 standards
- [ ] The workspace enforces role-based data access: Sarah sees only her assigned studies, only her assigned sites within those studies, and only her assigned queries (or all queries on her sites — resolution per Open Question 2)
- [ ] The workspace refreshes signals at a frequency sufficient for same-session awareness of new overdue items and new anomaly signals (target: signal refresh within 15 minutes of source event)
- [ ] The FIRES area of the 3-area workspace structure surfaces only items requiring immediate action — safety-flagged queries, queries overdue today, new anomaly signals since last login, and unacknowledged escalation responses; it does not surface routine work-pending items

---

*Document created: 2026-02-23*
*Parent: product-brief-Testing-2026-02-22.md*
*Next step: PRD authoring — CDM workspace functional requirements*
