---
date: 2026-02-23
author: Root
parent: product-brief-Testing-2026-02-22.md
persona: Study Manager
status: draft
---

# Feature Brief: Study Manager Workspace
## CluePoints Integrated Platform — User-Centric Workspace

---

## Overview

The Study Manager is the operational owner of a clinical trial. She sits at the intersection of execution (CDMs, central monitors, data managers) and governance (risk leads, program managers). Her workspace must serve two simultaneous functions:

1. **Aggregator** — pulling up signals from her team's operational work into a single study health picture
2. **Decision surface** — surfacing the items that require her judgment, approval, or escalation before they become problems

This brief defines the specific workspace requirements for the Study Manager persona: what she sees, what she can do, how AI assists her, and how her workspace connects to the rest of the platform.

---

## Persona Recap

**Elena** — Study Manager at a mid-to-large CRO, responsible for a Phase II/III trial with 20–30 active sites across 3 regions and a team of 4–6 CDMs, 2 central monitors, and 1–2 data managers.

**Access pattern:** Daily, primarily mornings and end-of-day. Heavier use on Monday (weekly planning), Thursday (status prep), and around data lock milestones.

**Reports to:** Program Manager / Sponsor oversight lead

**Directly manages:** CDMs, central monitors (depending on org structure)

**Key tensions:**
- Needs high-level view but must be able to drill to detail fast when something escalates
- Responsible for team performance but lacks visibility into individual workloads
- Expected to produce status updates but has no single source of truth to pull from
- Risk escalations often reach her via email/Slack before they surface in the platform

---

## What the Study Manager Workspace Must Deliver

### 1. Study Health Overview

The primary panel. On login, Elena needs an at-a-glance picture of her study's current state — not a list of raw data points, but a synthesized health signal she can act on or ignore.

**Required elements:**

| Element | Description |
|---------|-------------|
| Overall study health indicator | RAG (Red/Amber/Green) composite signal derived from site risk, query aging, KRI adherence, and milestone status |
| Site risk distribution | Breakdown of sites by risk tier — how many red/amber/green, trend vs. last week |
| Query aging summary | % of open queries within SLA vs. overdue; trend direction |
| KRI adherence rate | % of triggered KRIs with an assigned action within SLA |
| Milestone proximity | Next key milestone with days remaining and current confidence indicator |
| Last updated timestamp | When each signal was last refreshed |

**Design principles:**
- Show trend direction (↑↓→), not just current state
- Exception-first: amber and red items should be visually dominant
- One-click drill-through from any summary element to the underlying detail view in the relevant module

---

### 2. Escalation & Decision Queue

The most time-sensitive panel. Items here require Elena's active decision before they can move forward. If this queue is empty, the study is running well. If it is backed up, something is breaking down.

**Item types that appear here:**

| Source | Item type | Expected action |
|--------|-----------|-----------------|
| CDM | Risk escalation — site issue flagged beyond CDM authority | Acknowledge, assign, or escalate to Risk Lead |
| Central Monitor | Site tier change recommendation | Approve or return with comments |
| Risk Lead | Risk plan amendment requiring SM sign-off | Review and approve/reject |
| System | SLA breach — no action taken on a KRI breach within defined window | Assign owner, adjust SLA, or escalate |
| AI Agent | AI-generated recommendation requiring SM validation before execution | Review, approve, or dismiss |

**Queue behavior:**
- Sorted by urgency (safety-flagged items first, then SLA age)
- Each item shows: source, item description, age, last actor, and recommended action
- Inline resolution for straightforward decisions (approve/return/escalate) without leaving workspace
- Items older than 48 hours highlighted; items older than 72 hours trigger a notification

---

### 3. Team Activity & Workload View

Elena needs to understand what her team is doing, where they are stretched, and whether workloads are balanced — without having to ask.

**Required elements:**

| Element | Description |
|---------|-------------|
| Per-team-member action queue depth | How many open items each CDM/central monitor has assigned |
| SLA performance per team member | % of items resolved within SLA per person, rolling 7 days |
| Last activity timestamp | When each person last logged an action in the system |
| Overdue item concentration | Are overdue items clustered on one person (capacity problem) or spread (systemic problem)? |

**Key actions from this panel:**
- Reassign items from one team member to another directly from workspace
- Flag a team member as "unavailable" to pause auto-assignment routing to them
- Open a team member's full action queue in a side panel without leaving workspace

**What this is not:**
- Not a performance management tool — this is a workload visibility tool
- Not a real-time chat or communication surface — Elena uses existing channels for that
- Does not expose individual performance scores or metrics to peers

---

### 4. Site Cluster View

Sites rarely have problems in isolation. The Study Manager often needs to spot patterns across sites before the individual signals become visible — a country cluster, a CRO site group, a cohort of recently activated sites.

**Required elements:**

| Element | Description |
|---------|-------------|
| Site groupings | Sites grouped by region, country, CRO, and activation cohort |
| Group-level health signal | Aggregated risk score and query aging for each group |
| Outlier detection | AI-flagged groups where health is degrading faster than expected or diverging from peers |
| Drill-through | From group to site list, from site list to individual site card |

**Key actions from this panel:**
- Tag a site group as "under review" — this surfaces the tag on individual site cards for CDMs and central monitors
- Create a group-level risk note that attaches to all sites in the cluster
- Assign a targeted monitoring action to all sites in a group in a single operation

---

### 5. AI Summary & Drafting Surface

Elena spends significant time producing status content — study updates for program managers, risk summaries for risk leads, site-specific narratives for escalations. The workspace should do the first draft.

**AI capabilities available from the Study Manager workspace:**

| Capability | Trigger | Output |
|------------|---------|--------|
| Weekly study status summary | Auto-generated every Thursday, or on-demand | 1-page study health narrative covering sites, queries, KRIs, and milestones |
| Escalation briefing | Triggered when Elena initiates an escalation to Risk Lead or Program Manager | Structured briefing note with context, prior actions, and recommended next step |
| Site cluster narrative | Triggered when Elena tags a site group as "under review" | Summary of what the cluster's signals indicate and what actions have been taken |
| Team workload rebalancing suggestion | Triggered when queue depth imbalance exceeds threshold | Suggested reassignment plan based on current items, SLA risk, and team capacity |
| Risk plan amendment summary | Triggered when a risk plan change is under review | Plain-language summary of what changed, why, and what the impact is |

**AI interaction model:**
- AI drafts are generated proactively (weekly summary, cluster narrative) or on-demand from explicit workspace buttons
- All drafts are presented for review before any action is taken — no AI content is sent or logged without Elena's explicit approval
- Elena can edit inline or request a revision with a comment
- Approved drafts are logged with the AI-generated flag and Elena's approval timestamp (audit trail)

---

### 6. Escalation Pathways (Inbound and Outbound)

The Study Manager workspace is a hub in the escalation network. Items flow in from CDMs and central monitors; items flow out to Risk Leads and Program Managers.

**Inbound escalations (from CDMs / Central Monitors):**
- Appear in the Decision Queue (Panel 2)
- Tagged with escalating person, original signal, and time since raised
- Elena receives a workspace notification when an inbound escalation ages past 24 hours without action

**Outbound escalations (to Risk Lead / Program Manager):**
- Initiated from any panel in the workspace via a consistent "Escalate" action
- Elena selects the recipient role (Risk Lead or Program Manager) — the system routes to the correct person
- An AI-drafted escalation briefing is offered before submission (see Panel 5)
- Escalation is logged in the item history and appears in the recipient's workspace Decision Queue
- Elena's workspace shows the status of her outbound escalations (pending, acknowledged, resolved)

**Escalation SLAs (configurable per organization):**
- Inbound from CDM: Elena expected to acknowledge within 4 hours, resolve or escalate within 24 hours
- Outbound to Risk Lead: Risk Lead expected to acknowledge within 8 hours
- SLA breach triggers workspace notification and supervisor visibility

---

## What the Study Manager Workspace Does NOT Do

To maintain focus and avoid scope creep:

- **Does not replace module views** — for deep query management or detailed RBQM configuration, Elena navigates to the relevant module. The workspace surfaces summaries and decision items, not full module functionality.
- **Does not show patient-level data** — individual patient records, adverse events, and clinical data are accessed in the relevant module. Workspace shows aggregated signals only.
- **Does not surface financial or contractual data** — budget, change orders, and contract milestones are out of scope for this workspace.
- **Does not manage site activation workflows** — site activation steps, regulatory submissions, and investigator qualification data are managed in the CTMS and are not surfaced here.
- **Does not generate regulatory-submission documents** — AI summaries are operational aids, not regulatory artifacts.

---

## Information Hierarchy

How information flows to and from the Study Manager workspace:

```
Program Manager Workspace
        ↑ (portfolio roll-up, escalations out)
        │
Risk Lead Workspace
        ↑ (risk governance escalations out)
        │
┌─────────────────────────────────────┐
│        STUDY MANAGER WORKSPACE      │  ← this brief
│                                     │
│  Study Health │ Decision Queue      │
│  Team View    │ Site Cluster View   │
│  AI Surface   │ Escalation Status   │
└─────────────────────────────────────┘
        │
        ↓ (escalations in, team workload signals)
CDM Workspace       Central Monitor Workspace
```

---

## Open Questions

The following questions should be resolved before PRD authoring:

| # | Question | Why it matters | Owner |
|---|----------|---------------|-------|
| 1 | Does Elena manage one study or multiple studies simultaneously? | If multiple, the workspace needs a study-switcher and cross-study rollup at her level, not just at Program Manager level | Product / UX |
| 2 | What is the org model — CRO-side SM or sponsor-side SM? | Affects data access permissions, who is in "her team," and escalation routing | Product |
| 3 | Is the Risk Lead always a distinct person from the Study Manager, or is the SM sometimes the risk owner? | Affects whether risk governance panel belongs in SM workspace or is a separate role | Product |
| 4 | What is the right cadence for the AI weekly summary — automatic push, or on-demand only? | Determines notification model and whether Elena feels the AI is working for her vs. generating noise | UX research |
| 5 | Does the team workload view need to be visible to CDMs looking up, or is it SM-only? | Privacy/visibility model for subordinate workload data | Product / Legal |
| 6 | How does escalation routing work when the Risk Lead or Program Manager is on leave / unassigned? | Affects escalation SLA model and fallback routing design | Platform / Engineering |

---

## Acceptance Criteria (MVP)

The Study Manager workspace is considered complete for MVP when:

- [ ] Elena can log in and see overall study health (RAG, site distribution, query aging, KRI adherence) without navigating to any module
- [ ] Inbound escalations from CDMs and central monitors appear in her Decision Queue and can be actioned inline (approve, return, escalate, assign)
- [ ] Team workload view shows queue depth and SLA performance per team member; items can be reassigned from this view
- [ ] Site cluster view shows region/country groupings with aggregated health signals and supports group-level tagging and action assignment
- [ ] AI-generated weekly study summary is available on demand; Elena can review, edit, and approve before it is sent or logged
- [ ] Outbound escalations to Risk Lead and Program Manager can be initiated from any workspace panel, with AI-drafted briefing offered before submission
- [ ] All actions taken from the workspace are logged with actor, timestamp, and source item for audit trail purposes
- [ ] Workspace respects role-based data access — Elena sees only her assigned study/studies and her team members

---

*Document created: 2026-02-23*
*Parent: product-brief-Testing-2026-02-22.md*
*Next step: PRD authoring — Study Manager workspace functional requirements*
