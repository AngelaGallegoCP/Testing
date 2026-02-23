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

CluePoints users — clinical data managers, biostatisticians, and medical reviewers — currently enter the platform into siloed modules with no unified sense of "where they are" or "what matters now." Each session begins with manual navigation, context reconstruction, and cognitive overhead that delays actual clinical oversight work.

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
- **Role-context mismatch:** A biostatistician and a CDM have fundamentally different priorities; a one-size-fits-all navigation structure forces both into the same default path.
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
4. **Adapts to role:** CDMs see query queues and site-level anomalies; biostatisticians see statistical signal summaries and protocol deviation patterns; medical reviewers see patient safety flags and data narratives.
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

**2. Biostatistician**

*Profile:* Marcus, a senior biostatistician at a sponsor company, is responsible for statistical monitoring plans and reviewing anomaly signals across 2 active trials. He is not in CluePoints every day but relies on it for weekly oversight reviews and escalation decisions.

*Problem experience:* Marcus finds CluePoints hard to "enter cold" — when he logs in after several days away, there's no summary of what has changed since his last visit. He must navigate module by module to reconstruct the current state of each study. Statistical signal summaries require him to run or locate specific reports.

*What success looks like:* Marcus logs in and sees a "since your last visit" summary: new statistical signals, updated risk scores, queries opened or closed. He can drill into what changed without re-running reports. AI-generated pattern summaries give him a starting point for deeper analysis.

---

**3. Medical Reviewer / Safety Officer**

*Profile:* Dr. Priya, a medical reviewer at a sponsor, reviews safety-relevant data flags and protocol deviations. She interacts with CluePoints reactively — triggered by escalations or study milestones — rather than daily.

*Problem experience:* When escalated to CluePoints, Dr. Priya has difficulty quickly locating the specific safety flag, the supporting data context, and the history of actions taken. She often calls the CDM to reconstruct context that should be findable in the system.

*What success looks like:* Dr. Priya receives a workspace notification, logs in, and sees the safety flag with full context: the data record, the AI-generated narrative summary, the history of prior reviews, and a set of recommended actions. She can review and act in a single session without external coordination.

### Secondary Users

**Study Manager / Trial Lead:** Uses the Workspace as a high-level oversight surface — seeing portfolio-level risk status and team workload across studies. Does not need query-level granularity but needs cross-study signal aggregation.

**Platform Administrator:** Configures role definitions, workspace layouts, and AI agent permissions per organization. Does not use the workspace operationally but is responsible for the role-mapping infrastructure that makes it work.

### User Journey

**CDM — Daily Triage Flow:**

1. *Login:* Workspace loads with personalized feed — "3 queries require response today, 1 site flagged for anomalous enrollment pattern, AI found 2 potential data cleaning opportunities."
2. *Prioritize:* CDM scans the ranked feed, identifies the site flag as highest priority.
3. *Act:* Opens site context inline, reviews supporting data, assigns a query to the site — all from the workspace surface.
4. *Delegate to AI:* Triggers an AI agent to draft responses for the 2 lower-priority queries.
5. *Monitor:* AI agent status appears in the workspace activity feed. CDM reviews drafts when ready.
6. *Close loop:* Approves agent-drafted responses; items leave the active feed. Day's priority work is complete in under 45 minutes.

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
- Personalized, prioritized feed of actionable items based on user role (CDM, biostatistician, medical reviewer)
- Items sourced from: query management, RBQM risk signals, site flags, protocol deviations
- Clinical prioritization logic: safety signals > risk signals > administrative items
- "New since last visit" grouping for infrequent users

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

- **Portfolio-level Workspace views** (cross-study rollup for study managers) — post-MVP
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
