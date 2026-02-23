---
date: 2026-02-23
author: Root
parent: product-brief-Testing-2026-02-22.md
persona: Risk Lead
status: draft
---

# Feature Brief: Risk Lead Workspace
## CluePoints Integrated Platform — User-Centric Workspace

---

## Overview

The Risk Lead is the risk governance owner for a portfolio of trials. Unlike the Study Manager — who executes operational oversight day-to-day — the Risk Lead sets the strategic parameters by which risk is identified, measured, and responded to across multiple studies. He does not manage individual queries, conduct site visits, or oversee team workloads. His domain is the RBQM strategy itself: defining KRI/KQI thresholds, verifying that risk plans are being executed as written, and exercising final approval authority on decisions that exceed the Study Manager's scope.

The Risk Lead workspace must serve two simultaneous functions:

1. **Governance monitor** — a cross-study view that tells David whether his risk plans are working: whether KRI breaches are occurring, whether they are being actioned within SLA, and whether any systemic patterns have emerged across studies that his current risk plans do not account for.
2. **Approval authority** — the decisional surface for items that require his sign-off: site tier change recommendations, risk plan amendment requests, and AI-flagged threshold recalibration recommendations.

This is a fundamentally different workspace from every other persona's. The Study Manager, CDM, and Central Monitor all see the world one study at a time, drilling in as needed. The Risk Lead sees the world at the portfolio level first. The portfolio is not a navigation option for David — it is his default unit of work. Drill-down to individual studies is available, but the workspace never defaults to a single-study view.

This brief defines what David's workspace must contain, what it must enforce (governance, not operations), how AI pattern detection delivers its highest value for this persona, and what design questions must be resolved before PRD authoring can proceed.

---

## Persona Recap

**David** — Risk Lead at a mid-to-large pharmaceutical sponsor. He owns the risk-based monitoring strategy for a portfolio of 4–8 active trials in a therapeutic area. He is the organizational authority on RBQM methodology for his program: he defines KRI thresholds, sets risk tier criteria, approves changes to risk plans, and is accountable to the head of clinical operations for the quality of the risk monitoring framework across his studies.

**Access pattern:** Primarily weekly governance cycles — typically a Monday review of KRI adherence and an end-of-week check on approval queue aging. Supplemented by reactive access triggered by escalations from Study Managers or AI-flagged patterns requiring immediate attention. David is not a daily user in the way a CDM or Central Monitor is; his high-value interactions are episodic and high-stakes.

**Reports to:** Head of Clinical Operations / VP Clinical Development (sponsor-side)

**Interacts with:** Study Managers (receives escalations, approves tier changes), Program Manager (escalates systemic portfolio observations), RBQM module (owns risk plan definitions), CDMs and Central Monitors (indirectly, via risk plan execution)

**Key tensions:**

- Cannot see the state of his risk plans from a single location — must navigate into individual study modules to observe KRI status, making cross-study awareness nearly impossible without dedicated report-running
- Finds out about systemic issues through escalation chains, not proactive signal — by the time an issue reaches him, it has already been surfaced, assessed, and partially handled by the SM and CDM
- Uncertain whether risk plans are being executed as written versus adapted in the field without his knowledge — KRI thresholds may be working as he designed, or they may be consistently producing false alarms that the team has learned to ignore; he cannot tell which
- Approval queue can accumulate silently — tier change recommendations and plan amendments may age without his awareness if he does not proactively check; no existing surface shows him the age distribution of items awaiting his decision
- No mechanism exists for him to observe cross-study patterns — if the same KRI is breaching across four studies simultaneously, no one is in a position to see this except David, and David currently has no tool that shows it to him

---

## What the Risk Lead Workspace Must Deliver

### 1. Risk Governance Dashboard

The primary panel. David's workspace must open to a cross-study governance view that immediately answers: "What is happening across my portfolio of risk plans right now?"

This is not a study list. It is a governance health signal per study, designed to be scanned in under two minutes, with exception-first visual design that draws David's eye to the studies that need his attention.

**Required elements — per-study row:**

| Element | Description |
|---------|-------------|
| Study identifier | Study name/ID and phase; sponsor-assigned identifier |
| Overall risk plan health signal | RAG composite signal: Red = plan is failing (multiple unresolved breaches past SLA, escalation backlog), Amber = plan is stressed (SLA adherence declining, recurring breach pattern), Green = plan is executing as designed |
| KRI breach count | Total active KRI breaches in the current monitoring cycle, with trend indicator vs. prior cycle (↑↓→) |
| KRI breach trend | Direction and rate of change — is breach count increasing, stable, or resolving? |
| Threshold adherence rate | % of KRI breaches actioned within the SLA defined in the risk plan; this is the primary adherence metric and the clearest proxy for whether the risk plan's response system is functioning |
| Sites with unresolved escalations past SLA | Count of sites where an escalation has exceeded the defined resolution SLA; these are the most operationally exposed sites in David's portfolio |
| Open items awaiting David's decision | Count of tier changes, amendments, and recalibration requests pending his approval; age of oldest item |
| Last risk plan review date | When the study's risk plan was last reviewed or amended — studies with stale risk plans against an active trial are a governance gap |

**Design principles for this panel:**
- Exception-first visual hierarchy: Red and Amber rows must be visually dominant; Green rows should recede
- All trend indicators show directionality, not just current state — a study moving from Green to Amber is more urgent than a stable Amber
- One-click drill-down from any summary row to the Risk Plan Adherence View for that study (Panel 3)
- The dashboard is the entry point for David's weekly governance cycle — it should be the first screen he sees and should answer his first question before he has to click anything

**What this panel is not:**
- Not a detailed query or site management view — no individual query lists, no site contact history
- Not a milestone tracker — enrollment and timeline health belong to the PM workspace
- Not a team workload view — David does not monitor individual CDM or CM performance

---

### 2. Approval Queue

The decisional surface. Items here require David's active judgment before they can be actioned by anyone else. Unlike the Study Manager's Decision Queue (which handles operational escalations), David's Approval Queue is a governance queue — every item represents a decision at the risk strategy level.

**Item types that appear in the Approval Queue:**

| Source | Item type | What David must decide |
|--------|-----------|------------------------|
| Study Manager | Site risk tier change recommendation | Approve or return with comments; tier change cannot be executed without Risk Lead approval |
| Study Manager | Risk plan amendment request | Approve the amendment as proposed, approve with modifications, or reject with rationale |
| AI (system-generated) | KRI threshold recalibration recommendation | Review supporting data, approve threshold adjustment, or dismiss with rationale |
| Study Manager | Escalation from SM authority — risk signal that exceeds SM scope | Acknowledge, investigate, or escalate to Program Manager |
| System | SLA breach on David's own approval queue items | Acknowledgment required — an aged item is itself a governance failure |

**Per-item display requirements:**

| Field | Description |
|-------|-------------|
| Study | Study name and ID |
| Item type | Category (tier change / amendment / recalibration / escalation) |
| Source | Who submitted (SM name, AI agent, system) |
| Recommendation | Plain-language summary of what is being requested and why |
| Supporting data | KRI breach history, site performance trend, AI analysis — linked inline, not requiring module navigation |
| Age since submitted | Days/hours since the item entered David's queue; items >48 hours highlighted; items >72 hours trigger notification |
| AI-generated summary | Plain-language explanation of the recommendation's rationale and expected impact if approved |

**Queue behavior:**
- Sorted by urgency: safety-adjacent items first, then SLA age (oldest first within category)
- Inline approval/rejection — David can approve or reject with a structured comment without leaving the workspace
- Structured comment field on rejection: requires David to specify reason (insufficient data / threshold rationale needed / scope exceeds plan amendment / return to SM for more context) — unstructured rejection is not permitted; all rejections must carry a reason that routes back to the submitter
- Approved items are logged with David's identity, timestamp, and the approval context (what supporting data was presented at time of decision) — this is a regulated audit trail, not a soft log
- Items David dismisses without acting (e.g., AI recalibration recommendation he judges unnecessary) require a "dismiss with rationale" action — no silent dismissal

---

### 3. Risk Plan Adherence View

David's primary governance concern is not whether KRIs breach — it is whether the response system is working. A KRI breach is expected; a KRI breach that sits unactioned for 10 days is a governance failure.

The Risk Plan Adherence View is the detailed per-study view David uses to answer: "Is the risk plan being executed as I wrote it?"

**Triggered by:** Clicking into any study row from the Risk Governance Dashboard (Panel 1), or navigating directly to a specific study from the Actions Ribbon.

**Required elements for each study:**

| Element | Description |
|---------|-------------|
| KRI breach log | All KRI breaches in the current and prior monitoring cycles; for each breach: which KRI triggered, breach date, severity, assigned owner, action taken, resolution date, and whether resolution occurred within SLA |
| SLA adherence timeline | Visual timeline showing the gap between breach date and action date for each breach; SLA threshold line drawn; items above the line are SLA failures |
| Response owner performance | Aggregated by response owner (CDM, CM) — are breaches being actioned on time? Are specific owners consistently missing SLA? (Note: this is aggregate performance data for governance purposes, not a performance management view — David sees patterns, not individual performance scores) |
| Tier change history | Log of all site tier changes within the study, with rationale, date, and whether David approved or it was within SM authority |
| Risk plan version history | Which version of the risk plan is currently active; what changed between versions and when; David's amendment approvals in the history |
| Deviation from risk plan | AI-flagged instances where operational actions appear to deviate from the risk plan's defined response protocol — sites where tier changes were delayed beyond the plan's prescribed trigger, KRIs that were overridden without documented rationale |

**Key actions from this view:**
- Propose a threshold amendment directly from the breach log (e.g., if a specific KRI is consistently breaching by a small margin, David can initiate a recalibration from the adherence view)
- Flag a specific breach pattern as "under investigation" — this surfaces a note on the relevant CDM/CM's workspace
- Navigate to Risk Plan Management (Panel 5) to edit threshold parameters in the context of what the adherence data shows

**What this view is not:**
- Not a query management view — individual queries behind the KRI signals are not displayed here
- Not a site-level monitoring dashboard — site contact history, visit reports, and operational site notes are not part of this view
- Not a real-time data feed — adherence data refreshes on the same cycle as the underlying RBQM module (typically daily)

---

### 4. Cross-Study Pattern Surface

This is where the Risk Lead workspace creates the most value that no human process can replicate. No individual Study Manager, CDM, or Central Monitor can see across studies — each sees only their own. David is the only person in the governance structure positioned to observe portfolio-level patterns. But without tooling, he cannot see them either.

The Cross-Study Pattern Surface is an AI-generated proactive intelligence feed. It is not a queue of items requiring immediate action — it is a signal surface that tells David: "Here is something happening across multiple studies that no single-study view would reveal."

**Pattern types surfaced:**

| Pattern type | Example | Significance |
|--------------|---------|--------------|
| Same KRI category breaching across multiple studies | Protocol deviation rate KRI is above threshold in Studies A, C, and F simultaneously | Suggests a threshold calibration issue (the threshold is too sensitive) or a systemic data collection problem across the program — not a study-specific issue |
| Same site type underperforming across studies | Academic medical center sites in all three Phase III trials showing elevated query aging vs. community sites | Suggests a site-type-specific training or resource issue; risk plans may need a site-type-stratified tier threshold |
| Divergence between risk plan version and breach pattern | Studies that amended a specific KRI threshold 6 months ago show lower adherence SLA performance post-amendment | Suggests the amendment may have had unintended consequences — the changed threshold produces a different operational response pattern |
| New risk signal not covered by current risk plans | A data completeness metric is trending negatively across four studies but no KRI is currently defined to capture it | Suggests a gap in the risk plan framework; David may need to define a new KRI category |
| SLA adherence decline correlated across studies | Threshold adherence rate drops across multiple studies in the same 2-week period | May indicate a platform event, a CRO-side staffing change, or a training gap — not study-specific |

**Pattern display requirements:**

| Field | Description |
|-------|-------------|
| Pattern description | Plain-language summary of what AI detected |
| Studies affected | Which studies are involved; count and list |
| Signal strength | AI confidence level and evidence basis (number of data points, consistency of signal) |
| Suggested response | AI-recommended action: investigate, escalate to PM, amend threshold across studies, schedule a risk plan review |
| Age of pattern | When AI first detected this pattern; whether it is strengthening or stabilizing |
| Status | New / Under review / Dismissed / Actioned |

**Key design principle:** This panel is proactive intelligence, not an action queue. Most patterns David sees here will not require immediate action — they inform his next risk plan review cycle. The panel should feel like a briefing, not an alarm. The FIRES area (see 3-Area Structure below) will surface the subset of patterns that are time-sensitive or safety-adjacent.

**AI interaction model for this panel:**
- Patterns are generated on a defined cycle (default: weekly, aligned to David's governance cadence) and on-demand
- David can "subscribe" to a pattern — marking it as one he wants to track across future cycles
- David can dismiss a pattern with a rationale — the AI logs the dismissal and suppresses similar patterns for a defined period unless the signal strengthens significantly
- David can ask a follow-up question on any pattern: "Why is the same KRI breaching in Studies A, C, and F but not in Study B?" — the AI responds inline with a comparative analysis

---

### 5. Risk Plan Management

David needs to view and amend the risk plans he owns from his workspace — not by navigating into the RBQM configuration module for each study individually. The workspace provides a governance-level interface to risk plans that exposes the elements David needs for his oversight role, without duplicating the full configuration capability of the RBQM module.

**Accessible from:** Actions Ribbon (direct access to any study's risk plan) or drill-through from the Risk Plan Adherence View (Panel 3) when in context of a specific study.

**Required capabilities:**

| Capability | Description |
|------------|-------------|
| Review current KRI/KQI thresholds | For any assigned study: view all active KRI thresholds, their current status (active/suspended/under review), and their version history |
| Review risk tier definitions | The criteria that trigger a site tier change (what KRI combination at what severity moves a site from Tier 1 to Tier 2, etc.) |
| Propose a threshold amendment | David can initiate a threshold change from his workspace. This creates a draft amendment with: proposed new threshold, rationale, expected impact on breach frequency (AI-estimated), and a routing workflow. The amendment is not applied until the routing workflow completes. |
| Amendment routing workflow | David's proposed amendment routes to the Study Manager for acknowledgment before taking effect. SM acknowledgment confirms operational awareness (the SM will need to brief her CDMs and CMs on the threshold change). David has authority to approve his own amendments; SM acknowledgment is informational, not a veto. If SM has not acknowledged within a defined SLA, David can apply the amendment with a noted override. |
| Risk plan version history | Full history of risk plan versions for any study: what changed, who approved, when it took effect, and what the operational impact was (as measured by the adherence view post-amendment) |
| Cross-study threshold comparison | For a given KRI category, compare the threshold levels set across all assigned studies — useful for identifying inconsistencies that may not be intentional (Study A has protocol deviation KRI set at 5%, Study B at 8%, with no documented rationale for the difference) |

**What this panel is not:**
- Not a full RBQM configuration interface — raw data collection rules, query configuration, and monitoring plan architecture are managed in the RBQM module
- Not a study setup tool — David amends existing risk plans; he does not create them from scratch in this workspace
- Not a submission-ready document editor — risk plans have a regulated format managed in the RBQM module; the workspace provides a governance view, not a regulatory artifact editor

---

### 6. Escalation Pathways

The Risk Lead workspace sits at a defined point in the escalation network. Items flow in from Study Managers (escalations that exceed SM authority). Items flow out to Program Managers (systemic portfolio-level risk observations that exceed David's authority or require program-level resource decisions).

**Inbound escalations (from Study Managers):**
- Appear in the Approval Queue (Panel 2) when they are active decision items
- Appear in the FIRES area when aged or safety-adjacent
- Each inbound escalation shows: originating SM, original signal, SM's assessment and recommendation, and time since raised
- David receives a workspace notification when an inbound escalation ages past 8 hours without acknowledgment (per configurable SLA)
- David's response options: Approve/reject SM's recommendation, request additional context from SM, escalate to Program Manager with David's own assessment, or mark as "under investigation" with a stated return timeline

**Outbound escalations (to Program Manager):**
- Initiated from any panel in the workspace via a consistent "Escalate to Program Manager" action
- Triggered when David observes a systemic portfolio-level pattern that requires PM-level visibility or resource allocation (e.g., a cross-study pattern suggesting a fundamental risk plan design flaw affecting multiple programs)
- AI-drafted escalation memo offered before submission: structured briefing covering the pattern, the affected studies, David's analysis, and his recommended PM-level response
- David can edit the AI draft inline or request a revision with a comment before submission
- Escalation is logged with full context; appears in PM's workspace as a governance observation (not an operational action item)
- David's workspace shows the status of outbound escalations: pending acknowledgment / acknowledged / closed with response

**Escalation SLAs (configurable per organization):**

| Escalation direction | SLA expectation | SLA breach action |
|---------------------|-----------------|-------------------|
| SM → Risk Lead (inbound to David) | Acknowledge within 8 hours, resolve or escalate within 48 hours | Workspace notification to David + notification to PM that an escalation is aging |
| Risk Lead → PM (outbound from David) | PM acknowledges within 24 hours | Workspace notification to David that acknowledgment is overdue |

---

## What the Risk Lead Workspace Does NOT Do

To maintain the governance boundary and avoid scope creep:

- **Does not manage individual queries** — query-level work belongs to CDM and Central Monitor workspaces. David's workspace shows KRI breach patterns and threshold adherence rates; it does not display query lists, query aging queues, or query response interfaces.
- **Does not show team workloads** — CDM and CM workload visibility is the Study Manager's domain. David does not need to know which CDM has how many open queries; he needs to know whether the overall response system is meeting SLA. Workload views are not part of this workspace.
- **Does not perform site monitoring actions** — site contact drafts, visit reports, targeted monitoring assignments, and site-level intervention actions are initiated from the CM and CDM workspaces. David may approve a tier change that triggers monitoring intensity changes, but he does not initiate the monitoring actions themselves.
- **Does not replace the RBQM module for deep configuration** — the RBQM module is the system of record for risk plan configuration, data collection rules, and statistical monitoring parameters. David's workspace shows governance summaries and supports threshold amendment workflows; it does not replicate or replace the RBQM module's configuration surface. Deep configuration changes require module navigation.
- **Does not surface patient-level data** — individual patient records, adverse events, and patient-level data narratives are not part of this workspace. David works at the level of KRI aggregates and risk signals, not individual patient data points.
- **Does not generate regulatory-submission documents** — AI-generated summaries and escalation memos are operational governance aids with full audit trail. They are not regulatory artifacts (e.g., clinical study report risk sections, RBQM regulatory submission documents). Those remain in the RBQM module's document management function.
- **Does not initiate site tier changes** — David approves tier change recommendations submitted by Study Managers and Central Monitors. He cannot initiate a tier change himself. The workspace enforces this boundary: there is no "initiate tier change" action available to David — only "approve" or "reject" actions on submitted recommendations.

---

## Information Hierarchy

How information flows to and from the Risk Lead workspace:

```
Program Manager Workspace
        ↑ (systemic portfolio-level risk observations, escalations requiring PM resource authority)
        │
┌────────────────────────────────────────────────────────┐
│               RISK LEAD WORKSPACE                      │  ← this brief
│                                                        │
│  Risk Governance Dashboard  │  Approval Queue          │
│  Risk Plan Adherence View   │  Cross-Study Patterns    │
│  Risk Plan Management       │  Escalation Status       │
└────────────────────────────────────────────────────────┘
        │                            │
        │ (receives escalations,     │ (governance owner of
        │  approves tier changes,    │  risk plan definitions;
        │  receives plan amend       │  amends thresholds,
        │  acknowledgments from SM)  │  reviews version history)
        │                            │
Study Manager Workspace(es)       RBQM Module
   (one or more SMs               (system of record for
    below David in the             KRI configuration,
    governance structure)          statistical rules,
                                   risk plan documents)
```

**Key structural notes:**
- The Risk Lead workspace sits above Study Manager workspaces in the escalation chain, and below the Program Manager workspace
- Unlike the SM workspace (which receives signals from CDMs and CMs below it), the Risk Lead workspace does not receive signals from CDMs or CMs directly — it receives them only after they have passed through SM review
- The RBQM module is a lateral connection, not a hierarchical one — David is the governance owner of risk plan definitions, and the workspace provides a governance-level interface to those definitions; the module is the system of record

---

## 3-Area Structure: Fires / Actions Ribbon / Work Pending

The Risk Lead workspace uses the same 3-area spatial organization as all other persona workspaces, adapted for the portfolio-first, governance-centric nature of David's role.

```
┌──────────────────────────────────────────────────────────────────────┐
│  FIRES                                                               │
│  Unresolved escalations past SLA; tier change recommendations        │
│  aged >48h without David's decision; AI-flagged systemic patterns    │
│  requiring immediate attention; studies that moved from Amber to     │
│  Red since David's last login (delta, not just current state)        │
├──────────────────────────────────────────────────────────────────────┤
│  ACTIONS RIBBON                                                      │
│  Approve tier change  │  Propose risk plan amendment                 │
│  Escalate to PM       │  Generate governance summary                 │
│  Search across studies (site, KRI, study name, open item)           │
├──────────────────────────────────────────────────────────────────────┤
│  WORK PENDING                                                        │
│  Full approval queue (non-urgent items)                              │
│  Risk Plan Adherence View (per-study drill-down)                     │
│  Cross-Study Pattern Surface (AI-generated portfolio intelligence)   │
│  Risk Plan Management (threshold review and amendment workflow)      │
│  Outbound escalation status (to PM)                                  │
└──────────────────────────────────────────────────────────────────────┘
```

### FIRES — Detailed Content

| Content | Trigger | Source |
|---------|---------|--------|
| Escalation from SM past 8-hour SLA without David's acknowledgment | SLA timer | Inbound escalation (Panel 6) |
| Tier change recommendation aged >48 hours without decision | Age threshold | Approval Queue (Panel 2) |
| Risk plan amendment request aged >48 hours without decision | Age threshold | Approval Queue (Panel 2) |
| AI-flagged systemic pattern with high signal strength (safety-adjacent KRI, broad study impact) | AI pattern detection | Cross-Study Pattern Surface (Panel 4) |
| Study risk plan health signal moved from Amber to Red since last login | Delta detection (last-login anchor) | Risk Governance Dashboard (Panel 1) |
| SLA adherence rate dropped below minimum acceptable threshold for any study since last login | Delta detection | Risk Governance Dashboard (Panel 1) |

**Key constraint on FIRES:** Like the SM workspace, the Risk Lead FIRES area must be change-oriented, not state-oriented. David already knows Study X is at Amber — he needs to know it moved to Red overnight. Every FIRES item must carry a delta indicator: "since last login" or "since [timestamp]." A governance dashboard that shows current state but not change is operationally insufficient for an episodic user who may not log in daily.

### ACTIONS RIBBON — Detailed Content

| Action | Description | Triggers |
|--------|-------------|---------|
| Approve Tier Change | Opens the oldest pending tier change recommendation for inline review and decision | Approval Queue (Panel 2) |
| Propose Risk Plan Amendment | Opens amendment workflow for any assigned study; David selects study, KRI, proposed threshold, and rationale | Risk Plan Management (Panel 5) |
| Escalate to Program Manager | Opens outbound escalation flow with AI draft memo offered | Escalation Pathways (Panel 6) |
| Generate Governance Summary | AI-generates a portfolio-level governance briefing covering all studies — for use in leadership reviews or program manager updates | AI drafting surface |
| Search across studies | Persistent search: find a study by name/ID, find an open approval item by type, find a KRI by category, find a site by name | Cross-workspace search |

### WORK PENDING — Detailed Content

| Content | Source panel | Workflow |
|---------|-------------|---------|
| Full approval queue (all pending items, sorted by age and urgency) | Panel 2 | Review → Approve/Reject with comment |
| Risk Plan Adherence View (per study) | Panel 3 | Select study → review breach log → propose amendment |
| Cross-Study Pattern Surface (AI portfolio intelligence) | Panel 4 | Review pattern → subscribe / dismiss / act |
| Risk Plan Management (threshold review and amendment workflow) | Panel 5 | Select study → review thresholds → propose amendment |
| Outbound escalation status tracker | Panel 6 | Monitor pending → acknowledged → resolved status |

---

## Resolved Design Decisions

### Decision 1 — Cross-Study as Default: Portfolio is the Primary Abstraction (RESOLVED 2026-02-23)

**Decision:** The Risk Lead workspace has no single-study equivalent to the Study Manager workspace. Portfolio is the default abstraction. There is no "single-study mode."

**Rationale:** Every other persona in the platform (CDM, Central Monitor, Study Manager) defaults to a single-study view because their work is study-specific — they manage queries, sites, and team members for one study at a time. The Risk Lead's work is inherently cross-study: he governs a risk plan framework that spans his portfolio, and the most important signals he can receive are portfolio-level patterns that no single-study view reveals. Defaulting the Risk Lead workspace to a single study would systematically deprive him of the cross-study intelligence that is his primary value-add.

**Architectural implication:** David's workspace always opens to the Risk Governance Dashboard (Panel 1) showing all assigned studies in a portfolio view. Drill-down to individual studies is available from every panel — but it is always a drill-down, never a default. There is no study-switcher in the traditional sense; instead, any panel supports a "filter to study X" action that narrows the view while keeping the portfolio frame visible.

**Design enforcement:** The Actions Ribbon search and study-filter controls allow David to narrow any view to a specific study when he needs detail. But the landing state, the FIRES area, and the Risk Governance Dashboard are always portfolio-first. Individual study names appear as rows, tiles, or drill-targets — never as the workspace's default scope.

**Note on the SM-as-risk-owner scenario:** If Stakeholder Question 2 (below) resolves to "B" or "C" (SM sometimes or often IS the risk owner), the portfolio-first design may need a conditional mode. A person who is simultaneously SM and Risk Lead on the same study needs to see that study in both operational detail and governance overview — the portfolio-first frame would be maintained at the workspace level, but individual study cards would expose both operational and governance views when the user holds both roles. This conditional logic is not designed in this brief; it is flagged as a structural implication of Q2's resolution.

---

### Decision 2 — Governance vs. Operational Boundary: Risk Lead Approves, Does Not Execute (RESOLVED 2026-02-23)

**Decision:** The Risk Lead can approve tier changes but cannot initiate them. He can amend risk plans but cannot perform site monitoring actions. The workspace enforces this boundary in the UI.

**Rationale:** Clinical trial oversight has a defined authority model. Site monitoring actions (targeted monitoring assignments, site contact drafts, query initiation) are within CDM and Central Monitor authority. Tier change decisions that exceed CM/SM authority escalate to the Risk Lead for approval — but the Risk Lead does not independently decide to change a site's tier without a CM/SM recommendation. Risk plan amendments are within David's authority but require SM acknowledgment because the SM and her team must adapt their operations to the new thresholds. These boundaries are not bureaucratic — they preserve the audit trail integrity of RBQM decisions and ensure that operational teams are not bypassed by governance-level actors.

**UI enforcement — specific exclusions:**
- No query management interface is exposed in the Risk Lead workspace. Query lists, query response forms, and query assignment tools do not appear. If David clicks through to a site card from an adherence view, he sees risk-relevant site signals (KRI breach history, tier history), not query detail.
- No team workload views are exposed. CDM and CM action queue depths and SLA performance are aggregated into the adherence metrics David sees, not shown as individual workload tables.
- No site contact or monitoring action initiation surfaces appear. David cannot draft a site contact, schedule a monitoring visit, or assign a targeted review from his workspace.
- No "initiate tier change" action exists. The Approval Queue contains only inbound recommendations submitted by SMs and CMs. David's only tier change actions are approval or rejection.

**Scope statement:** The Risk Lead workspace is a governance and approval surface. It is designed to feel like a control tower, not a workbench. David monitors, approves, and adjusts risk strategy. He does not execute clinical monitoring operations. Any future feature request that proposes adding operational execution capability to the Risk Lead workspace should be explicitly evaluated against this boundary — additions require deliberate justification, not incremental scope creep.

---

## Open Questions

The following questions remain open before PRD authoring can proceed:

| # | Question | Why it matters | Owner |
|---|----------|---------------|-------|
| 1 | Is the Risk Lead role always distinct from the Study Manager, or can they be the same person? | This is flagged as Q2 in stakeholder-questions-sm-workspace-2026-02-23.md. Its resolution directly determines whether the Risk Lead workspace is a standalone persona workspace or a conditional "risk owner mode" layered onto the SM workspace. The current brief is written assuming always-distinct (Scenario A). If the answer is B or C, the workspace architecture changes: the Risk Lead workspace may merge with the SM workspace conditionally, the portfolio-first design may need a per-role overlay, and the approval authority model must account for a person approving their own SM-level recommendations. This is the highest-priority open question for Risk Lead workspace PRD authoring. | Product |
| 2 | Does the Risk Lead have cross-CRO visibility — can David see risk plan adherence for all CROs working on a sponsor's study, or is his view scoped to a single CRO's operational data? | Many sponsor-side studies involve multiple CROs. If David can only see one CRO's adherence data, his cross-study governance view is incomplete — a systemic pattern may be CRO-specific and invisible to him unless cross-CRO data is available. Conversely, CRO-scoped data access may be contractual; surfacing one CRO's performance data to a sponsor Risk Lead with cross-CRO visibility raises data governance questions. | Product / Legal |
| 3 | How does threshold amendment routing work? If David proposes a KRI threshold change, does it route to the SM for acknowledgment, or does he have unilateral authority to apply threshold changes immediately? | The current brief assumes SM acknowledgment is required but is informational, not a veto — David can override if the SM does not acknowledge within SLA. This assumption needs validation. If David has unilateral authority (no SM acknowledgment needed), the routing workflow simplifies significantly. If SM acknowledgment is a genuine veto right (not just informational), the amendment workflow becomes bidirectional and could deadlock if SM and Risk Lead disagree. The answer has clinical precedent in RBQM governance models and should be grounded in how CluePoints's current customers handle threshold change authority. | Product / Clinical SME |
| 4 | Is the Risk Plan Adherence View data currently available in CluePoints, or would computing it require new platform instrumentation? | The adherence view requires knowing: (a) when a KRI breach was detected, (b) when the first documented CDM/CM action was taken in response, and (c) whether that action interval falls within the risk plan's defined SLA. If CluePoints currently logs KRI breach detection timestamps and action timestamps linked to specific breach events, the adherence calculation is derivable from existing data. If the platform does not currently link action timestamps to specific KRI breach events, computing SLA adherence requires new event logging instrumentation — a potentially significant engineering scope addition. This question must be resolved before the Risk Plan Adherence View can be scoped for MVP. | Engineering / Data |
| 5 | What is David's notification and alert model for the Cross-Study Pattern Surface? If AI flags a systemic pattern, does David receive a push notification (email, in-platform alert) that brings him back to the workspace, or does he only see patterns when he logs in and reviews the panel? | David is an episodic user — he may not log in for 3–4 days between governance cycles. If an AI-detected pattern requires timely attention (e.g., the same safety-adjacent KRI is breaching across four studies simultaneously), a pull-only model (David sees it when he next logs in) may be inadequate. A push model (email or notification that surfaces the pattern and links to the workspace) is more appropriate for high-signal patterns but requires a notification architecture and a severity threshold model for what triggers a push vs. stays in the panel for next login. | Product / UX |

---

## Acceptance Criteria (MVP)

The Risk Lead workspace is considered complete for MVP when:

**Risk Governance Dashboard (Panel 1):**
- [ ] David lands on a cross-study portfolio view on login — no single-study default, no study selection required to see portfolio health
- [ ] Each assigned study shows: overall risk plan health RAG, KRI breach count with trend indicator, threshold adherence rate, sites with unresolved escalations past SLA, and count/age of items awaiting David's decision
- [ ] Studies in Red and Amber status are visually dominant; Green studies recede
- [ ] FIRES area shows delta items — studies that changed RAG status and escalations that aged past SLA since David's last login — not just current state
- [ ] One-click drill-through from any study row to the Risk Plan Adherence View for that study

**Approval Queue (Panel 2):**
- [ ] All pending tier change recommendations, risk plan amendment requests, and AI-flagged recalibration recommendations appear in David's queue
- [ ] Each item shows: study, source, item type, recommendation, supporting data (inline), age since submitted
- [ ] Items aged >48 hours are visually highlighted; items aged >72 hours trigger a workspace notification
- [ ] David can approve or reject any item inline, without leaving the workspace
- [ ] Rejection requires a structured rationale from a defined list; unstructured rejection is not permitted
- [ ] All approval and rejection actions are logged with actor identity, timestamp, decision, rationale, and the supporting data presented at time of decision (regulated audit trail)
- [ ] Dismissed AI recommendations (e.g., recalibration recommendations David judges unnecessary) require a "dismiss with rationale" action — no silent dismissal permitted

**Risk Plan Adherence View (Panel 3):**
- [ ] For any assigned study, David can view the KRI breach log: breach date, KRI triggered, severity, assigned owner, action taken, resolution date, and SLA compliance status
- [ ] SLA adherence timeline shows the breach-to-action interval for each breach, with the defined SLA threshold marked
- [ ] Risk plan version history shows all amendments with what changed, who approved, and when the amendment took effect
- [ ] David can initiate a threshold amendment directly from the breach log when in context of a specific study

**Cross-Study Pattern Surface (Panel 4):**
- [ ] AI-generated patterns are surfaced showing cross-study KRI correlations, site-type performance patterns, and risk plan gaps
- [ ] Each pattern shows: description, affected studies, signal strength, suggested response, pattern age, and current status
- [ ] David can subscribe to a pattern (track across future cycles), dismiss with rationale, or initiate an action (escalate to PM, open amendment workflow)
- [ ] High-signal patterns (safety-adjacent KRI, broad study impact) surface in FIRES, not only in the Work Pending panel

**Risk Plan Management (Panel 5):**
- [ ] David can view current KRI/KQI thresholds and risk tier definitions for any assigned study without navigating to the RBQM module
- [ ] David can initiate a threshold amendment from the workspace — proposed threshold, rationale, and AI-estimated impact on breach frequency
- [ ] Amendment routing workflow sends the amendment to the relevant Study Manager for acknowledgment; David can see acknowledgment status
- [ ] Cross-study threshold comparison is available for any KRI category — David can see all assigned studies' threshold levels for a specific KRI side by side

**Escalation Pathways (Panel 6):**
- [ ] Inbound escalations from Study Managers appear in the Approval Queue and age-based notifications are sent when SLA is approaching or breached
- [ ] David can escalate to Program Manager from any panel, with an AI-drafted escalation memo offered before submission
- [ ] Outbound escalation status is visible in Work Pending: pending acknowledgment / acknowledged / closed with PM response
- [ ] All escalation actions are logged with full context for audit trail

**All panels:**
- [ ] All actions taken from the workspace are logged with actor, timestamp, and source item — regulatory-grade audit trail
- [ ] Workspace respects role-based data access — David sees only studies assigned to him within his portfolio; no cross-portfolio data leakage
- [ ] The governance boundary is enforced in the UI: no query management surfaces, no team workload views, no site monitoring action initiation, no "initiate tier change" action
- [ ] FIRES area is change-oriented: all FIRES items carry a "since last login" delta indicator, not only current state
- [ ] Cross-study view is the permanent default: no single-study landing state is reachable as a default; drill-down to individual studies is always available but always a deliberate navigation act

---

*Document created: 2026-02-23*
*Parent: product-brief-Testing-2026-02-22.md*
*Next step: Resolve Open Questions 1–5 before PRD authoring for Risk Lead workspace*
*Structural dependency: Resolution of stakeholder-questions-sm-workspace-2026-02-23.md Q2 is a prerequisite for finalizing whether this workspace is standalone or conditionally merged with the SM workspace*
