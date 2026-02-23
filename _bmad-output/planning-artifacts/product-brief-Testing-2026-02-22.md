---
stepsCompleted: [1, 2, 3, 4, 5]
inputDocuments:
  - _bmad-output/brainstorming/brainstorming-session-2026-02-20.md
date: 2026-02-22
author: Root
project: Testing (CluePoints Integrated Platform)
---

# Product Brief: User-Centric Workspace — CluePoints Integrated Platform

---

## Executive Summary

CluePoints users — clinical data managers, central monitors, medical reviewers, study managers, risk leads, and program managers — currently enter the platform into siloed modules with no unified sense of "where they are" or "what matters now." Each session begins with manual navigation, context reconstruction, and cognitive overhead that delays actual clinical oversight work.

The **User-Centric Workspace** is the new entry point and landing page of the CluePoints integrated platform. It replaces a fragmented module-first experience with a role-aware, task-forward home that surfaces the user's active work, prioritized signals, and AI-assisted next actions — all in one cohesive surface.

This is not a dashboard. It is an intelligent operational hub: a living, contextual workspace that understands who the user is, what studies they own, what is at risk, and what AI agents can do on their behalf. It is the logical home for end-to-end assistive AI that guides, automates, and augments clinical monitoring workflows from a single authoritative location.

---

## Core Vision

### Problem Statement

Clinical research professionals using the CluePoints platform spend meaningful time each session re-establishing context: which studies need attention, which queries are overdue, which sites are showing anomalous patterns. This context must be manually reconstructed from multiple modules (RBQM, query management, site oversight, risk signals) every time they log in. There is no single surface that says: *here is your world, here is what matters, here is what to do next.*

As AI agents are introduced across the platform, they risk becoming isolated tools rather than a cohesive system — each accessible only through deep module navigation, with no unified agent command surface.

### Problem Impact

- **Wasted time at session start:** Users spend 5–15 minutes navigating to reassemble their working context before doing any actual oversight work.
- **Missed signals:** Risk signals and query exceptions that surface in one module go unnoticed by users primarily working in another.
- **Underutilized AI:** AI-assisted suggestions buried inside modules are acted on less frequently because they require intentional navigation to find.
- **Role-context mismatch:** A risk lead and a program manager have fundamentally different priorities from a CDM; a one-size-fits-all navigation structure forces all of them into the same default path.
- **Cognitive fatigue:** Reassembling context manually every session contributes to oversight errors and alert fatigue.

### Why Existing Solutions Fall Short

- **Current CluePoints entry:** Lands users into a module list or generic dashboard with no personalization, no prioritization, and no AI integration at the surface level.
- **Generic BI dashboards (Tableau, Power BI embeds):** Provide data views but no task context, no workflow continuity, and no action capability.
- **CTMS portals:** Centered on study metadata and milestones, not on the user's operational workflow and real-time data signals.
- **Point AI tools:** Embedded within specific modules, they create AI assistance that is modal and inaccessible from a unified surface — users cannot ask a question that spans modules.

None of these solutions treat the workspace as the user's personal operational environment. They treat it as a navigation container.

### Proposed Solution

A **role-aware, AI-integrated Workspace** that serves as the primary entry point of the CluePoints platform. On login, users land in their Workspace — a surface that:

1. **Surfaces what matters now:** Prioritized work items (queries, risk signals, site flags, overdue actions) ranked by urgency and study context.
2. **Maintains continuity:** Resumes where the user left off — active studies, open queries, in-progress reviews — with full session context preserved.
3. **Hosts AI agents natively:** End-to-end assistive AI agents are accessible directly from the Workspace. Users can trigger, monitor, and review agent actions without entering a module.
4. **Adapts to role:** CDMs see query queues and site-level anomalies; central monitors see centralized statistical signals and site performance trends; medical reviewers see patient safety flags and data narratives; study managers see cross-study risk rollups and team workloads; risk leads see KRI/KQI threshold status and risk plan adherence; program managers see portfolio health and milestone status across studies.
5. **Bridges modules:** The Workspace is the connective layer — actions taken here propagate into the relevant modules; module activity surfaces back into the Workspace feed.

### Key Differentiators

- **Context-first, not navigation-first:** The workspace knows who you are and what you're responsible for before you click anything.
- **AI as a first-class citizen:** AI agents are not buried in modules — they are part of the workspace UI, surfaced as collaborators rather than features.
- **Cross-module signal unification:** Risk signals, queries, site alerts, and protocol deviations are normalized into a single prioritized feed — no module-hopping required.
- **Clinical domain depth:** The prioritization logic is not generic ("most recent") but clinically grounded — safety signals outrank administrative items, high-risk sites surface before low-risk ones.
- **Action capability at the surface:** Users can resolve, delegate, escalate, or hand off to an AI agent directly from the Workspace without entering a module.

---

## Target Users

### Primary Users

**1. Clinical Data Manager (CDM)**

*Profile:* Sarah, a CDM at a mid-size CRO, manages data oversight for 3–6 concurrent Phase II/III trials. She works in CluePoints daily, splitting time between query management, site issue resolution, and protocol deviation tracking.

*Problem experience:* Every morning, Sarah opens CluePoints and spends 10–12 minutes navigating between query management, site risk reports, and the RBQM dashboard to understand what needs attention. She frequently misses signals from modules she visits less frequently. AI-generated query suggestions in the query module go unacted on because she's working in the risk module.

*What success looks like:* Sarah opens CluePoints and within 30 seconds understands her top 5 priorities. She can act on a query, review a site flag, and trigger an AI-assisted data cleaning run — all without leaving the workspace surface. Her day starts with direction, not navigation.

---

**2. Central Monitor**

*Profile:* James, a central monitoring specialist at a sponsor, is responsible for remote site oversight across 8–12 sites on a Phase III trial. He works in CluePoints daily, analyzing centralized statistical signals, site performance trends, and KRI thresholds to identify sites that need intervention without waiting for an on-site visit.

*Problem experience:* James's workflow requires constant cross-referencing between the RBQM module, site-level signal reports, and query status. When a site crosses a KRI threshold, he needs to understand the full context — query history, prior flags, enrollment trends — before deciding on action. Currently he pieces this together from three separate views. He also struggles to track which sites he has already reviewed vs. which are new since his last session.

*What success looks like:* James logs in and sees a site-prioritized view ranked by risk signal severity. For each flagged site, context is already assembled: KRI breach detail, query backlog, and AI-generated site narrative. He can escalate, assign a follow-up action, or trigger an AI agent to draft a site contact — without leaving the workspace.

---

**3. Medical Reviewer / Safety Officer**

*Profile:* Dr. Priya, a medical reviewer at a sponsor, reviews safety-relevant data flags and protocol deviations. She interacts with CluePoints reactively — triggered by escalations or study milestones — rather than daily.

*Problem experience:* When escalated to CluePoints, Dr. Priya has difficulty quickly locating the specific safety flag, the supporting data context, and the history of actions taken. She often calls the CDM to reconstruct context that should be findable in the system.

*What success looks like:* Dr. Priya receives a workspace notification, logs in, and sees the safety flag with full context: the data record, the AI-generated narrative summary, the history of prior reviews, and a set of recommended actions. She can review and act in a single session without external coordination.

---

**4. Study Manager**

*Profile:* Elena, a study manager at a CRO, owns end-to-end delivery of a Phase II/III trial across 20+ sites and a cross-functional team of CDMs, central monitors, and data managers. She is accountable for study timelines, risk escalation decisions, and team performance.

*Problem experience:* Elena has no aggregated view of her study's health in CluePoints. She must ask her CDMs to prepare status summaries, manually pull site-level reports, and triangulate team workload from outside the system. Risk escalations often reach her late because there is no workspace surface that shows her what is building before it becomes critical.

*What success looks like:* Elena opens her workspace and sees her study health at a glance: site risk distribution, open query aging, team action queue, and escalation items requiring her decision. She can spot an emerging site cluster issue and assign it to the central monitor without a meeting or email. AI-generated study summaries give her what she needs for stakeholder updates without manual report-pulling.

---

**5. Risk Lead**

*Profile:* David, a risk lead at a sponsor, owns the risk-based monitoring strategy for a portfolio of trials. He defines KRI/KQI thresholds, reviews risk plan adherence, and approves risk tier changes for sites and studies. He interacts with CluePoints primarily at a governance and oversight level — not query-by-query.

*Problem experience:* David cannot see the state of his risk plans from a single location. KRI threshold breaches are only visible if he navigates into individual study risk modules. Risk plan adherence — whether CDMs and central monitors are acting on signals within SLA — is invisible to him without running reports. He finds out about systemic issues through escalation, not through proactive signal.

*What success looks like:* David's workspace shows a risk governance view: KRI breach counts by study, threshold adherence rates, sites with unresolved risk escalations older than SLA, and AI-flagged patterns that suggest a risk plan adjustment is warranted. He can review and approve risk tier changes directly from the workspace, with full audit trail.

---

**6. Program Manager**

*Profile:* Nadia, a program manager at a sponsor, oversees a portfolio of 4–6 trials within a therapeutic area. She is responsible for portfolio-level reporting to senior leadership, resource allocation across studies, and identifying cross-study risks or interdependencies. She uses CluePoints as one of several tools but needs it to give her a fast, reliable pulse on portfolio health.

*Problem experience:* Nadia has no portfolio view in CluePoints. She relies on study managers to provide status updates and manually assembles a portfolio picture. When leadership asks about data quality across the program, she cannot answer from the platform — she synthesizes from emails and spreadsheets. She is aware CluePoints holds the signal she needs but cannot surface it at her level of abstraction.

*What success looks like:* Nadia's workspace shows a program-level view: study health tiles for each trial, cross-study risk trends, milestone status, and flagged items requiring her attention or escalation approval. AI-generated program summaries are ready for her weekly leadership report. She can drill from portfolio to study to site in three clicks when she needs detail.

### Secondary Users

**Platform Administrator:** Configures role definitions, workspace layouts, and AI agent permissions per organization. Does not use the workspace operationally but is responsible for the role-mapping infrastructure that makes it work.

### Future Personas (Planned — Not in Current Scope)

The following personas are identified for inclusion in a future iteration of this brief once their workspace requirements are more fully defined:

- **Biostatistician** — statistical monitoring plan ownership, anomaly signal review, and cross-study pattern analysis
- **CRA (Clinical Research Associate)** — on-site and remote monitoring, visit report management, and site relationship context

### User Journeys

**CDM — Daily Triage Flow:**

1. *Login:* Workspace loads with personalized feed — "3 queries require response today, 1 site flagged for anomalous enrollment pattern, AI found 2 potential data cleaning opportunities."
2. *Prioritize:* CDM scans the ranked feed, identifies the site flag as highest priority.
3. *Act:* Opens site context inline, reviews supporting data, assigns a query to the site — all from the workspace surface.
4. *Delegate to AI:* Triggers an AI agent to draft responses for the 2 lower-priority queries.
5. *Monitor:* AI agent status appears in the workspace activity feed. CDM reviews drafts when ready.
6. *Close loop:* Approves agent-drafted responses; items leave the active feed. Day's priority work is complete in under 45 minutes.

**Central Monitor — Site Risk Review Flow:**

1. *Login:* Workspace shows site-prioritized view — sites ranked by risk signal severity, with KRI breach indicators and days-since-last-review.
2. *Assess top site:* Opens site card inline — KRI breach detail, query backlog summary, enrollment trend, AI-generated site narrative already assembled.
3. *Decide:* Determines site needs a targeted follow-up communication. Triggers AI agent to draft a site contact note from the workspace.
4. *Move to next:* Reviews second-priority site, marks it as "reviewed — no action" from the feed.
5. *Handoff:* Escalates one site to Study Manager with one click; escalation surfaces in Study Manager's workspace feed.

**Study Manager — Weekly Study Health Review:**

1. *Login:* Workspace opens to study health view — site risk distribution, open query aging chart, team action queue, and items awaiting her decision.
2. *Spot pattern:* Notices 3 sites in the same country cluster are all showing elevated query aging. Identifies it as a potential site coordinator training issue.
3. *Act:* Creates a risk note tagged to the cluster, assigns investigation to central monitor from workspace.
4. *Review escalations:* Two items from CDMs are in her decision queue — reviews both and approves one, returns one with comments.
5. *Export summary:* AI-generated study status summary is ready; she reviews and sends to program manager from workspace.

**Risk Lead — KRI Governance Review (Weekly):**

1. *Login:* Workspace shows risk governance view — KRI breach count by study, SLA adherence rate for breach resolution, sites with open escalations past due.
2. *Identify concern:* One study shows a pattern of recurrent KRI breaches on the same indicator — suggests the threshold is miscalibrated or a systemic site issue.
3. *Review context:* Drills into the study's risk plan from the workspace; sees breach history and CDM response log.
4. *Approve adjustment:* Approves a risk tier change recommended by the study manager. Action is logged with audit trail.
5. *Flag for program:* Surfaces a cross-study pattern observation to Program Manager via workspace escalation.

**Program Manager — Portfolio Pulse (Bi-Weekly):**

1. *Login:* Workspace shows program health tiles for each active trial — RAG status, milestone health, open escalations.
2. *Identify outlier:* One study tile is amber — opens it to see the underlying signals (site risk concentration, enrollment lag).
3. *Drill down:* Study manager's last status summary is linked from the tile; reviews without navigating to a separate module.
4. *Escalate or hold:* Decides the risk is being managed; notes it for leadership report.
5. *Prepare update:* AI-generated program summary drafted and ready. Reviews, edits one line, and exports for the weekly leadership briefing.

---

## Success Metrics

### User Success Metrics

| Metric | Target | Measurement Method |
|--------|--------|-------------------|
| Time-to-first-action after login | < 2 minutes (vs. 10–15 min baseline) | Session event logging |
| % of daily priority actions completed from Workspace without module navigation | > 60% within 6 months | Navigation event tracking |
| AI agent task initiation rate from Workspace surface | > 40% of agent interactions initiated from Workspace | Agent invocation source attribution |
| User-reported "context clarity on login" satisfaction | > 4.2 / 5.0 | In-product pulse survey |
| Cross-module signal discovery rate (signals seen vs. signals generated) | > 80% discovery within 24h of signal creation | Signal event log analysis |

### Business Objectives

- **Platform stickiness:** Increase daily active usage rate among existing licensed users (target: +20% DAU within 6 months of launch).
- **AI feature adoption:** Workspace as the primary driver of AI agent adoption — users who engage with AI through Workspace should show 2x higher agent task completion rates than those who access agents through module entry points.
- **Retention signal:** Reduce churn risk for accounts where CDM power users were citing "platform complexity" as friction — target 15% reduction in complexity-attributed churn signals.
- **Expansion enabler:** Workspace serves as the primary surface for demonstrating new AI capabilities during renewal and upsell conversations — measurable as workspace feature demo inclusion in AE renewal decks.

### Key Performance Indicators

**Engagement**
- Workspace as session entry point: 90%+ of sessions begin on Workspace (not module landing) within 3 months post-launch
- Active feed interaction: 70%+ of users interact with at least one workspace feed item per session

**Efficiency**
- Session time-to-productive-action: Reduce median from 12 minutes to under 3 minutes
- Query response rate: 15% improvement in on-time query response rates among CDM users

**AI Adoption**
- Agent invocations from Workspace: 500+ agent tasks initiated from Workspace surface within first 60 days
- Agent task approval rate: > 75% of AI-drafted actions approved without modification (quality signal)

**Satisfaction**
- NPS delta: +10 NPS points for users who use Workspace daily vs. users who do not
- Support ticket reduction: 20% reduction in "where do I find X" support tickets post-launch

---

## MVP Scope

### Core Features

**1. Role-Aware Workspace Feed**
- Personalized, prioritized feed of actionable items based on user role (CDM, Central Monitor, Medical Reviewer, Study Manager, Risk Lead, Program Manager)
- Items sourced from: query management, RBQM risk signals, site flags, protocol deviations, KRI breaches, escalation queue
- Clinical prioritization logic: safety signals > risk signals > administrative items
- "New since last visit" grouping for infrequent users (Medical Reviewer, Risk Lead, Program Manager)

**2. Contextual Study Cards**
- My Studies panel: cards for each study the user is assigned to
- Each card shows: current risk score, open query count, last activity, top alert
- One-click navigation into study-specific module views from card

**3. Inline Action Capability**
- Respond to / close queries directly from feed without module navigation
- Assign queries to team members from feed
- Mark items as reviewed / acknowledged

**4. AI Agent Surface**
- Agent status panel: shows active and recently completed AI agent tasks
- Trigger AI agents from workspace: "Find data cleaning opportunities for Study X", "Draft query responses for overdue queries"
- Agent output review and approval inline (no module navigation required for approval)

**5. Workspace Notifications**
- Real-time alert surface for escalations, overdue items, new safety signals
- Configurable notification preferences per user

### Out of Scope for MVP

- **Cross-program rollup views** (multi-program aggregation for Program Managers beyond their assigned portfolio) — post-MVP
- **Custom workspace layout configuration** (drag-and-drop widget arrangement) — post-MVP
- **Workspace-native report building** — users navigate to reporting module for custom reports; Workspace shows curated summaries only
- **Mobile-optimized Workspace** — desktop-first for MVP; mobile responsive pass in follow-on sprint
- **Third-party data source integration** in feed (EDC, CTMS direct feeds) — phased via data integration roadmap
- **Team-level workspace views** (seeing team member workloads) — post-MVP

### MVP Success Criteria

The MVP is considered successful when:
- 80% of active CluePoints users are entering sessions via Workspace within 60 days of launch
- Median time-to-first-productive-action is under 3 minutes (down from ~12 min baseline)
- At least 300 AI agent tasks initiated from Workspace surface in the first 30 days
- Zero P1/P2 data integrity issues related to inline actions taken from Workspace (queries closed, items assigned)
- User satisfaction score for Workspace > 4.0/5.0 in first post-launch survey

**Go / no-go signal for V2 investment:** If 60%+ of weekly active users are returning to Workspace as their primary session start point at 90 days, proceed with full V2 scope (portfolio views, custom layout, mobile).

### Future Vision

**Phase 2 (3–6 months post-MVP):**
- Portfolio Workspace for study managers with cross-study risk aggregation
- Custom workspace layouts — users configure their feed priorities and panel arrangement
- Proactive AI: workspace surfaces AI-initiated suggestions ("I noticed Study X query resolution rate dropped — want me to flag this to the site?")
- Team workload visibility — CDMs see their team's open items and can rebalance assignments

**Phase 3 (6–12 months):**
- Conversational AI interface in Workspace — users can ask natural language questions ("What changed in Study X since last week?") and get structured answers
- External data connectors — EDC, CTMS, and eSource feeds surfaced in workspace signals
- Regulatory-ready audit trail of all workspace actions (for 21 CFR Part 11 / ICH E6 compliance)
- Workspace as SDK — partner integrations can surface cards and agent actions into the CluePoints Workspace

**Long-term (12–24 months):**
- Workspace as the control plane for autonomous clinical monitoring agents — agents operate semi-independently with Workspace as the human review and approval surface
- Cross-platform workspace (mobile, tablet) for on-site monitoring and real-time oversight
- Multi-tenant workspace for sponsors managing multiple CRO relationships from a single surface

---

*Document generated: 2026-02-22*
*Workflow: create-product-brief (BMad Method v6.0.1)*
*Input: brainstorming-session-2026-02-20.md*
