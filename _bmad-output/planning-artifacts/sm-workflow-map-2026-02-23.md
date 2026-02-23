---
date: 2026-02-23
author: Root
parent: feature-brief-study-manager-workspace-2026-02-23.md
status: draft
purpose: Map Elena's core workflows to the 3-area workspace structure; identify content gaps and missing workflows before PRD authoring
---

# Study Manager Workflow Map
## Elena's Core Workflows → 3-Area Workspace Structure

---

## How to Read This Document

The [Feature Brief](feature-brief-study-manager-workspace-2026-02-23.md) defined **what content exists** across 6 panels. This document maps **how Elena actually works** — her core daily and periodic workflows — and shows where each workflow step lives within the 3-area workspace structure.

The 3-area model:

```
┌──────────────────────────────────────────────────────────────────────┐
│  FIRES                                                               │
│  Urgent items requiring action before anything else. Change-oriented │
│  (what's new / what just broke), not just state-oriented.           │
├──────────────────────────────────────────────────────────────────────┤
│  ACTIONS RIBBON                                                      │
│  Persistent bar. The daily verbs: generate, reassign, escalate,     │
│  search, switch study. One click to start any common workflow.       │
├──────────────────────────────────────────────────────────────────────┤
│  WORK PENDING                                                        │
│  The full queue. Decision items not yet urgent, team workload,       │
│  site clusters, outbound escalation status, AI drafts awaiting      │
│  review. Organized and prioritized, but not on fire.                │
└──────────────────────────────────────────────────────────────────────┘
```

---

## Core Workflows

### W1 — Morning Triage
**Frequency:** Daily (primary morning session)
**Duration:** ~10 minutes
**Trigger:** Elena logs in

| Step | What Elena Does | Where It Lives | Panel Source |
|------|-----------------|----------------|--------------|
| 1 | Scans for **delta items** — what changed since yesterday | FIRES | ⚠️ Gap: no delta view designed yet (see §Gaps) |
| 2 | Reviews urgent decision queue items (>24h without action, safety-flagged) | FIRES | Decision Queue (Panel 2) |
| 3 | Checks study health RAG — if changed, understands why | FIRES | Study Health Overview (Panel 1) |
| 4 | Scans team workload for anyone overloaded or inactive since yesterday | WORK PENDING | Team Activity View (Panel 3) |
| 5 | Notes anything that needs a decision before her first meeting | FIRES → WORK PENDING | Decision Queue (Panel 2) |

**Outcome:** Elena knows what she must do today vs. what can wait. Takes no more than 10 minutes.

**Key constraint:** This workflow only works if the FIRES area is **change-oriented**, not just current-state. Elena already knows the study is at Amber — she needs to know it went *from Green to Amber overnight*.

---

### W2 — Escalation Decision
**Frequency:** Multiple times per day
**Duration:** 5–15 minutes per item
**Trigger:** Inbound escalation from CDM or Central Monitor; or a system SLA breach notification

| Step | What Elena Does | Where It Lives | Panel Source |
|------|-----------------|----------------|--------------|
| 1 | Sees item in Decision Queue — tagged with source, original signal, and time since raised | FIRES (if urgent/aged) or WORK PENDING (if new/low urgency) | Decision Queue (Panel 2) |
| 2 | Reviews item context inline — what was the original signal, what did the CDM already do | WORK PENDING (item detail) | Decision Queue (Panel 2) |
| 3 | Makes a decision: acknowledge + assign, approve tier change, return with comment, or escalate up | WORK PENDING → action | Decision Queue (Panel 2) |
| 4 | **If escalating up:** triggers AI escalation briefing draft | ACTIONS RIBBON → modal | AI Surface (Panel 5) |
| 5 | Reviews and edits AI draft | Modal / inline | AI Surface (Panel 5) |
| 6 | Approves and sends escalation to Risk Lead or Program Manager | Modal → confirm | Escalation Pathways (Panel 6) |
| 7 | Item moves to Outbound Escalation status — Elena can track whether it's been acknowledged | WORK PENDING | Escalation Pathways (Panel 6) |

**Outcome:** Item is actioned or escalated. Logged with actor, timestamp, action taken. If escalated, Elena has visibility into status.

**Key constraint:** Steps 1–3 must be completable **without leaving the workspace** (inline resolution). Steps 4–6 require a modal or panel expansion but should not require full navigation away.

---

### W3 — Status Report Preparation
**Frequency:** Weekly (Thursday default); on-demand before sponsor calls
**Duration:** 30–60 minutes including review and edit
**Trigger:** Thursday auto-generation or Elena clicks "Generate Status Summary" in Actions Ribbon

| Step | What Elena Does | Where It Lives | Panel Source |
|------|-----------------|----------------|--------------|
| 1 | Triggers or receives auto-generated AI weekly summary | ACTIONS RIBBON (on-demand) or FIRES (if auto-pushed) | AI Surface (Panel 5) |
| 2 | Reviews draft against study health signals — does the narrative match the data? | Modal / expanded AI panel | AI Surface (Panel 5) + Study Health (Panel 1) |
| 3 | Cross-checks site cluster view for any cluster narrative that should be included | Side-by-side or tab | Site Cluster (Panel 4) |
| 4 | Edits AI draft inline or requests revision with comment | Modal | AI Surface (Panel 5) |
| 5 | Approves draft — logged with AI-generated flag and Elena's approval timestamp | Confirm action | AI Surface (Panel 5) |
| 6 | Routes the approved summary to Program Manager / Sponsor | ⚠️ Gap: routing destination not designed (see §Gaps) | — |

**Outcome:** A reviewed, human-approved status summary is available with full audit trail.

**Key constraint:** Step 6 is undefined. "Approved and logged" is not the same as "delivered." The workflow breaks at the last step until routing is designed.

---

### W4 — Weekly Team Planning
**Frequency:** Weekly (Monday)
**Duration:** 20–30 minutes
**Trigger:** Start of week; often follows a Monday morning triage

| Step | What Elena Does | Where It Lives | Panel Source |
|------|-----------------|----------------|--------------|
| 1 | Reviews team workload — who has what, who's overloaded, who's under-assigned | WORK PENDING | Team Activity View (Panel 3) |
| 2 | Checks for inactive team members (last activity >24h) or anyone flagged "unavailable" | WORK PENDING | Team Activity View (Panel 3) |
| 3 | Reviews AI workload rebalancing suggestion if imbalance threshold was triggered | WORK PENDING (notification) or FIRES | AI Surface (Panel 5) |
| 4 | Reassigns items directly from team workload view | WORK PENDING → drag/reassign action | Team Activity View (Panel 3) |
| 5 | Reviews site cluster health — which sites / regions need focused attention this week | WORK PENDING | Site Cluster View (Panel 4) |
| 6 | Sets informal weekly priority in her head; no formal "plan" artifact generated | — | — |

**Outcome:** Team workload is balanced; Elena knows which sites and regions will demand attention this week.

**Key constraint:** Step 6 is informal — there is no mechanism for Elena to record or share her weekly priorities within the platform. This is likely intentional (out of scope) but worth flagging.

---

### W5 — Site Cluster Investigation
**Frequency:** Ad hoc, triggered by anomaly in health overview or AI outlier flag
**Duration:** 15–45 minutes depending on severity
**Trigger:** Health overview shows a region degrading; AI flags a cluster anomaly; CDM raises a pattern they're seeing

| Step | What Elena Does | Where It Lives | Panel Source |
|------|-----------------|----------------|--------------|
| 1 | Notices anomaly signal — region degrading, cluster flagged | FIRES (if AI-flagged) or WORK PENDING (browsing) | Study Health (Panel 1) or Site Cluster (Panel 4) |
| 2 | Navigates to Site Cluster View, filters by region/country/cohort | WORK PENDING | Site Cluster View (Panel 4) |
| 3 | Reviews group-level health signals — which groups are degrading, trend vs. last week | WORK PENDING | Site Cluster View (Panel 4) |
| 4 | Drills into the cluster to see individual site cards | WORK PENDING → drill | Site Cluster View (Panel 4) |
| 5 | **Wants to compare two clusters** to find differentiating factor ("why is Region A worse than Region B?") | ⚠️ Gap: cross-cluster comparison not supported (see §Gaps) | — |
| 6 | Tags cluster as "under review" | WORK PENDING → tag action | Site Cluster View (Panel 4) |
| 7 | AI generates cluster narrative — what the signals indicate, what actions have been taken | WORK PENDING → modal | AI Surface (Panel 5) |
| 8 | Reviews, edits, and approves cluster narrative | Modal | AI Surface (Panel 5) |
| 9 | Assigns group-level monitoring action to all sites in cluster | WORK PENDING → bulk action | Site Cluster View (Panel 4) |

**Outcome:** Cluster is tagged, monitored, documented. CDMs and central monitors see the "under review" tag on affected site cards. Group action is assigned.

---

### W6 — Risk Plan Review and Sign-off
**Frequency:** Periodic — triggered by Risk Lead, not Elena
**Duration:** 15–30 minutes
**Trigger:** Risk Lead submits a risk plan amendment requiring SM approval

| Step | What Elena Does | Where It Lives | Panel Source |
|------|-----------------|----------------|--------------|
| 1 | Item appears in Decision Queue, source = Risk Lead | WORK PENDING (or FIRES if aged/urgent) | Decision Queue (Panel 2) |
| 2 | AI generates plain-language summary of what changed and why | WORK PENDING → auto-generated | AI Surface (Panel 5) |
| 3 | Elena reviews AI summary and the underlying amendment | WORK PENDING → detail view | AI Surface (Panel 5) |
| 4 | Approves or rejects with comments | WORK PENDING → action | Decision Queue (Panel 2) |
| 5 | Decision logged; item returns to Risk Lead's workspace | Confirm action | Escalation Pathways (Panel 6) |

**Outcome:** Risk plan amendment is approved or returned. Full audit trail including Elena's review of the AI summary.

**Assumption:** Risk Lead and Study Manager are **distinct roles** (Stakeholder Question 2 not yet resolved). If the SM is also the risk owner, this workflow is replaced by a bidirectional risk governance workflow — see stakeholder questions.

---

## 3-Area Content Map

What lives where, derived from the workflows above:

### FIRES
| Content | Source workflow | Panel source |
|---------|----------------|--------------|
| Delta items since last login (new escalations, tier changes, SLA breaches) | W1 | ⚠️ Not yet designed |
| Safety-flagged decision queue items | W1, W2 | Panel 2 |
| Decision queue items aged >48h | W1, W2 | Panel 2 |
| AI-flagged cluster anomalies requiring immediate review | W5 | Panel 4 + Panel 5 |
| Study health RAG change (Green→Amber, Amber→Red) since last login | W1 | ⚠️ Not yet designed (delta) |

### ACTIONS RIBBON
| Action | Source workflow | Notes |
|--------|----------------|-------|
| Generate Status Summary | W3 | Triggers AI summary modal |
| Initiate Escalation | W2 | Starts outbound escalation flow |
| Reassign Item | W2, W4 | Opens quick-assign modal |
| Tag Site Cluster | W5 | Opens cluster selection + tag |
| Search (site, item, person) | W1–W6 | ⚠️ Not yet designed |
| Switch Study | All (multi-study mode) | Study Triage integration |

### WORK PENDING
| Content | Source workflow | Panel source |
|---------|----------------|--------------|
| Full decision queue (non-urgent items) | W2, W6 | Panel 2 |
| Team workload view | W1, W4 | Panel 3 |
| Outbound escalation status | W2 | Panel 6 |
| Site cluster view | W4, W5 | Panel 4 |
| AI drafts awaiting review/approval | W3, W5 | Panel 5 |
| Risk plan items pending SM review | W6 | Panel 2 |

---

## Workflow Gaps

Three gaps found in this analysis that are **not covered** by the 6 panels in the feature brief:

### Gap 1 — Delta View (W1: Morning Triage)
**Problem:** The health overview shows current state (Amber). Elena needs to see *change* — what moved from Green to Amber, what escalation arrived overnight, what SLA crossed a threshold while she was away.

**What's needed:** Every element in the FIRES area must have a delta dimension — not "3 sites at Red" but "2 new Red sites since last login." This likely requires a "last login" anchor timestamp per user session and a diff layer on top of each health signal.

**Risk if unaddressed:** Elena opens the workspace, sees the same Amber she saw yesterday, and ignores FIRES — missing the new escalation that came in at 11pm.

---

### Gap 2 — Status Summary Routing (W3: Status Report Preparation)
**Problem:** The workflow defines AI generation → review → edit → approve, but stops there. There is no "send to" step.

**What's needed:** A routing action when Elena approves the summary:
- Option A: Export to PDF / copy to clipboard (lowest-lift, email externally)
- Option B: In-platform message to Program Manager's workspace
- Option C: Auto-attach to a study milestone/meeting record

**Risk if unaddressed:** The AI summary becomes a document that lives in CluePoints and goes nowhere. Elena prints it or pastes it into an email — undermining the workflow value.

---

### Gap 3 — Cross-Cluster Comparison (W5: Site Cluster Investigation)
**Problem:** The site cluster view supports browsing, tagging, and drill-down within a single cluster. It does not support *comparing* two clusters side by side to identify differentiating signals.

**What's needed:** A comparison mode where Elena can select two site groups (e.g., Region A vs. Region B) and see their health signals, KRI performance, and query aging displayed side by side.

**Risk if unaddressed:** Elena's most common question — "why is one cluster worse than another?" — requires her to navigate back and forth between views and hold the comparison in her head. This is where CDMs currently do ad hoc Excel work to answer a question CluePoints should answer natively.

---

### Gap 4 — Search / Find (All Workflows)
**Problem:** No search surface is designed anywhere in the SM workspace. Elena frequently needs to navigate to a specific site by name, find a specific open item, or look up a team member's queue.

**What's needed:** A persistent search input in the Actions Ribbon. Scope: sites, open items in the decision queue, and team members assigned to the study.

**Risk if unaddressed:** Elena types a site name into her browser search or navigates to a module to find something she should be able to reach in one step from her workspace.

---

## Assumptions Made in This Workflow Map

These assumptions were made because Stakeholder Questions 1 and 2 are unresolved. If the answers differ, the affected workflows need revision.

| Assumption | Affects | What changes if assumption is wrong |
|------------|---------|--------------------------------------|
| Elena is a **CRO-side SM** — her team is CRO staff | W4 (Team Planning) — "her team" = CDMs and central monitors on her CRO | If sponsor-side: team view may show a mix of sponsor staff + CRO contacts; CRO workload visibility depends on contract |
| Risk Lead and Study Manager are **distinct roles** | W6 (Risk Plan Review) — SM receives amendments, doesn't create them | If SM is sometimes risk owner: W6 becomes bidirectional; SM workspace conditionally expands to include KRI threshold management and tier change initiation |
| **Single study mode** is the design target | All workflows | Multi-study mode (Study Triage View) would add a W0 — "cross-study morning scan" — before Elena drills into any single-study workflow |

---

*Created: 2026-02-23*
*Parent: feature-brief-study-manager-workspace-2026-02-23.md*
*Feeds into: PRD authoring — SM workspace functional requirements*
*Open questions: stakeholder-questions-sm-workspace-2026-02-23.md*
