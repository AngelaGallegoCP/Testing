---
date: 2026-02-23
author: Root
parent: product-brief-Testing-2026-02-22.md
persona: Medical Reviewer
status: draft
---

# Feature Brief: Medical Reviewer / Safety Officer Workspace
## CluePoints Integrated Platform — User-Centric Workspace

---

## Overview

The Medical Reviewer is a **reactive user**, not a daily operational user. She logs in when escalated to — triggered by a safety flag, a protocol deviation requiring medical judgment, or a data anomaly that requires clinical expertise to interpret. She may go days or weeks between sessions. When she does log in, she arrives with no ambient working knowledge of what has changed since her last visit, no time to reconstruct context from scattered modules, and a professional obligation to make a defensible, auditable clinical decision.

Her workspace has a fundamentally different design challenge from any other role in this system. The CDM has a high-volume queue she processes daily. The Study Manager has a team and a study to run. The Medical Reviewer has a small number of items — potentially zero — but when items exist, each one carries significant stakes and demands complete clinical context before a decision can be made.

This workspace must do two things, and only two things, exceptionally well:

1. **Context assembler** — all information about the flagged item, pre-built and pre-organized, so that Dr. Priya can understand the full picture without navigating to other modules or calling the CDM to reconstruct it verbally.
2. **Decision surface** — a clear, bounded set of available actions for each item type, with structured documentation requirements that satisfy audit trail obligations and, potentially, regulatory mandates.

These two functions are not equal in priority. Context assembly is the primary design challenge. If Dr. Priya cannot understand the item in full within the first few minutes of opening it, the decision surface is irrelevant — she will pick up the phone instead of using the platform. Every design decision in this workspace should be evaluated against this question: *does this help Dr. Priya understand the item faster and more completely?*

This brief defines the specific workspace requirements for the Medical Reviewer persona: what she sees, what she can do, how AI assists her, and how her workspace connects to the rest of the platform.

---

## Persona Recap

**Dr. Priya** — Medical Reviewer / Safety Officer at a sponsor organization, responsible for clinical judgment on safety-relevant data flags, protocol deviations that require medical interpretation, and data anomalies that exceed the authority of operational staff.

**Access pattern:** Reactive and infrequent. Not a daily user. Typically logs in when notified by a CDM or Study Manager that an item requires her review. Sessions may be separated by days or weeks. When she does log in, she expects to complete her review and leave — she has other clinical responsibilities outside the platform.

**Reports to:** Medical Director or Chief Medical Officer (outside CluePoints)

**Receives items from:** CDMs, Central Monitors, and Study Managers who have escalated items beyond their operational authority

**Escalates to:** Safety committee, medical monitor, or external clinical adjudication panels (outside CluePoints)

**Key tensions:**
- Arrives cold to each item — has no ambient context from daily platform use and must reconstruct the clinical picture from scratch each time she logs in
- Expected to make a defensible medical judgment call, but the information supporting that judgment is currently fragmented across query management, RBQM, site records, and patient data systems
- Time-pressured — she has active clinical responsibilities outside the platform and cannot spend an hour reconstructing context before reaching a decision
- High accountability — her decisions carry regulatory and patient safety weight; errors of omission (making a decision without full context) are more dangerous than delays

---

## What the Medical Reviewer Workspace Must Deliver

### 1. My Review Queue

The primary landing panel. This is the first thing Dr. Priya sees on login. Unlike the CDM's query queue — which typically holds dozens to hundreds of open items — this queue is expected to be small. In normal operation: 0–5 items. The design must accommodate both the empty state (which is normal and should feel reassuring, not broken) and the non-empty state (which requires immediate attention signal).

**Required elements per item card:**

| Element | Description |
|---------|-------------|
| Item type | Safety flag / Protocol deviation / Data anomaly — clearly labeled, not buried |
| Study | Study name and protocol number |
| Site | Site identifier and country |
| Patient | Anonymized patient identifier (e.g., subject ID) — see design decision on patient data access below |
| Age since escalated | How long this item has been waiting — shown prominently, in days and hours |
| Escalating party | Name and role of the person who escalated (e.g., "Escalated by James Chen, Central Monitor") |
| New since last login indicator | Whether this item arrived after Dr. Priya's last session |
| Activity-while-away indicator | If any actions have been taken on this item since she last logged in (e.g., "CDM added a data clarification note 3 days ago") |

**Critical behavioral requirement — "New since last login":**

This is the most important signal in the queue for this persona. Unlike the Study Manager (who logs in daily and sees a manageable delta), Dr. Priya may have been away for two weeks. Every item in the queue must show when it was escalated, how long it has been waiting, and what happened to it while she was away. Items that arrived after her last login should be visually distinguished. If an item has a history of activity since escalation, that history must be surfaced at the card level — not buried in a detail view.

**Queue empty state:**

The workspace should display a clear, dated confirmation when the queue is empty: "Your review queue is empty as of [timestamp]. Last checked: [date]." This state should feel clean and deliberate — not like a broken dashboard. The empty state is the normal state for this persona; designing it poorly erodes trust in the platform.

**Notification requirement:**

Dr. Priya will not log in speculatively. She has no reason to open CluePoints unless she knows something needs her attention. An out-of-platform notification (email or platform push notification, per user preference) is required to trigger her login. This notification must include: item type, study name, escalating party, and a direct link to the item in her workspace. Without this notification trigger, the review queue is unreachable in practice.

---

### 2. Item Context Card

When Dr. Priya opens any item from her review queue, a full context card is pre-assembled and ready. She should not need to navigate to another module, run a query, or call anyone to understand the item. This is the central design commitment of this workspace.

**The context card contains four layers:**

**Layer 1 — The underlying data record or data pattern**

The raw clinical data or data signal that triggered the flag. For a safety flag: the adverse event record, the relevant patient history entries, and the data points that crossed the threshold. For a protocol deviation: the specific visit or procedure record, the protocol specification it deviates from, and the documented sequence of events. For a data anomaly: the statistical signal or data pattern, displayed with enough context to be clinically interpretable (not a raw chart with no reference range).

This layer surfaces the ground truth. Dr. Priya must be able to see the actual data, not a summary of the data.

**Layer 2 — AI-generated narrative summary**

A plain-language clinical narrative that explains what was flagged, why it was flagged, and what the relevant context is. This is pre-assembled by AI before Dr. Priya opens the item (see Panel 4 — AI-Generated Context Narrative). It is presented as the second layer, after the raw data, so that Dr. Priya can read the narrative and then verify it against the underlying data if she chooses — not the other way around.

**Layer 3 — Item history**

The complete chronological history of actions taken on this item since it was created:
- When the original signal was generated (system or manual)
- Each query or data clarification that was raised and its resolution
- Each flag or annotation added by CDMs or central monitors
- The escalation event (who escalated, when, and with what rationale)
- Any prior medical reviews of this item (if the item was previously reviewed and returned for additional data, that prior review note must appear here)
- Any actions taken on the item while Dr. Priya was away since her last login

This layer answers the question: "what has already been done, and by whom?" Dr. Priya should never duplicate work that has already been done or be unaware of a relevant prior action.

**Layer 4 — Protocol and study reference**

The specific protocol section or specification against which the item was flagged. If the item is a protocol deviation, the relevant inclusion/exclusion criteria or procedure specification. If the item is a safety flag, the study's safety monitoring plan thresholds. Dr. Priya should be able to read the protocol reference without navigating to a separate document management system.

**Design decision flagged — Patient-level data access:**

The Item Context Card may require Dr. Priya to access patient-level clinical data directly from within her workspace. This is different from every other persona in this system. The CDM, Study Manager, and Risk Lead see aggregated or de-identified signals. The Medical Reviewer may need to see individual adverse event records, patient history, and lab values to make a clinically sound judgment.

This is a **compliance and access control decision**, not a UX decision, and must be resolved before the context card is designed. Options:

- **Option A:** Patient-level data is surfaced directly in the context card within CluePoints, subject to role-based access controls and audit logging. Requires confirming that CluePoints' data access model can support this without violating data governance policies.
- **Option B:** Patient-level data is accessible via a deep link from the context card into the EDC or data management system, opening in a separate authenticated session. CluePoints does not hold or render the data itself.
- **Option C:** Patient-level data is surfaced in a read-only embedded view within the context card, with access logged and audited separately.

This decision affects the architecture of the context card, the data access model, and likely has regulatory implications (21 CFR Part 11, GDPR, ICH E6). It is flagged as Open Question 1 below.

---

### 3. Decision Surface

After reviewing the context card, Dr. Priya reaches the decision surface. This is a bounded, structured set of available actions that correspond to the item type. The decision surface does not offer free-form fields. Every decision requires a structured note — a template that captures the clinical judgment in a format that satisfies audit trail obligations and can be referenced in regulatory review.

**Decision options by item type:**

**Safety Flag:**

| Decision | Structured note fields required |
|----------|----------------------------------|
| Review and clear | Clinical rationale for clearance; confirmation that all relevant data was reviewed; any monitoring recommendation going forward |
| Escalate to safety committee | Reason for escalation; whether this is a new signal or a recurring pattern; recommended urgency for safety committee review |
| Request additional data | What specific data is missing; who is responsible for obtaining it; expected timeline; item returns to CDM/Central Monitor with this request logged |

**Protocol Deviation:**

| Decision | Structured note fields required |
|----------|----------------------------------|
| Classify severity — minor | Severity rationale; assessment of impact on subject safety and data integrity |
| Classify severity — major | Severity rationale; patient safety assessment; whether regulatory reporting obligation is triggered |
| Approve waiver request | Clinical basis for approving the waiver; conditions or monitoring requirements attached to the approval |
| Reject waiver request | Clinical basis for rejection; recommended corrective action; whether the protocol requires formal amendment |

**Data Anomaly:**

| Decision | Structured note fields required |
|----------|----------------------------------|
| Review and clear — expected variation | Clinical explanation of why the anomaly is within acceptable range; data quality note |
| Flag for statistical review | Nature of the anomaly; whether it appears site-specific, patient-specific, or systemic; referred to whom |
| Escalate — potential safety signal | Clinical basis for safety concern; whether a formal safety review process is triggered |

**Structured note requirements:**

All structured notes are templated — fields, not free text boxes. Free text is permitted within fields for clinical judgment language, but the field structure itself is fixed. This ensures that the clinical rationale is captured in a consistent, searchable, and auditable format. Notes are auto-stamped with actor identity, timestamp, and item reference at the time of submission.

Once a decision is submitted, it cannot be edited — only superseded by a subsequent review action, which itself is logged and visible in the item history. This is a hard requirement for audit trail integrity.

---

### 4. AI-Generated Context Narrative

For each item in the review queue, AI pre-assembles a clinical context narrative before Dr. Priya opens the item. This is not a summary she requests — it is ready when she arrives. The goal is to eliminate the 20–40 minutes Dr. Priya currently spends reconstructing context from scattered modules and phone calls.

**The AI narrative includes:**

| Component | Description |
|-----------|-------------|
| Relevant data trend | The signal over time — not just the current flagged value, but the trajectory. For a safety event: how did this patient's relevant parameters trend before and after the event? For a protocol deviation: is this the first occurrence at this site or a pattern? |
| Comparable cases from the same study | If there are other patients, sites, or events in the same study that share characteristics with this flagged item, the AI surfaces them. Dr. Priya needs to know whether she is looking at an isolated event or one instance in a pattern. |
| Protocol specification cross-reference | The exact section of the protocol that this item was flagged against, with the relevant threshold or requirement quoted directly. |
| Prior actions and resolution history | A narrative summary of what has already been done on this item — who did it, what they found, and what they decided. |
| Plain-language summary | A 2–4 sentence clinical summary written for a physician: what happened, why it was flagged, what has been done, and what the open question is. This is the first thing Dr. Priya reads. |

**AI interaction model:**

- The narrative is generated proactively by the system when an item is escalated to Dr. Priya's queue. It is ready when she opens the item — she does not wait for generation.
- Dr. Priya can annotate the narrative with comments. Her annotations are saved and appear in the item history.
- If Dr. Priya identifies an error or gap in the narrative, she can flag it with a comment. The flag is logged in the item history and surfaces to the escalating party.
- Dr. Priya does not edit the AI narrative directly — she annotates it. The AI-generated narrative and her annotations are preserved as distinct records in the audit trail.
- If the AI narrative is incomplete (e.g., insufficient data was available at the time of escalation), a "narrative incomplete" indicator appears on the item card in the review queue, so Dr. Priya knows before she opens the item that she will need to exercise extra care.

**AI scope and limitations:**

The AI narrative is an information assembly tool, not a decision-making tool. It does not recommend decisions. It does not make clinical judgments. It surfaces and organizes the information that Dr. Priya needs to make her own judgment. This distinction must be clear in the interface: the AI narrative is labeled as AI-generated context, not as a recommendation.

---

### 5. Communication Surface

After making a decision, Dr. Priya may need to communicate with one or more parties:

- The escalating party (CDM, Central Monitor, or Study Manager) who submitted the item — to communicate the outcome and any required follow-up actions
- A safety committee or medical monitor (outside the platform) — to escalate an item beyond Dr. Priya's authority
- The site team — in rare cases where the deviation or safety event requires direct communication to the site (this path would typically go through the Study Manager or CDM, not directly from Dr. Priya)

**Communication is structured, not free-form.** Every communication from this workspace is tied to the item, logged in the item history, and written from a template that captures the decision outcome and any required next steps. Dr. Priya does not compose free-form emails from this workspace. The platform generates a structured message based on her decision and provides a field for additional context.

**Communication types:**

| Recipient type | Trigger | Template content |
|----------------|---------|-----------------|
| Escalating party (CDM / SM) | Any decision that requires follow-up action from the operational team | Decision outcome, required next action, assigned deadline, item reference |
| Safety committee referral | "Escalate to safety committee" decision on a safety flag | Structured referral note: item summary, Dr. Priya's clinical observations, urgency level, reference to prior reviews |
| Request for additional data | "Request additional data" decision on any item type | What data is needed, who is responsible, expected return timeline, item reference |

**Communication routing:**

Messages to CDMs and Study Managers are delivered into their workspace feed (Decision Queue or notification). The item in Dr. Priya's queue moves to a "pending additional data" state — visible, but no longer in the primary review queue. When the additional data is returned, the item resurfaces in Dr. Priya's review queue with the new data surfaced in the Item Context Card and the AI narrative updated to reflect it.

External communications (safety committee referrals) are generated as structured documents that can be exported from the platform. The platform does not manage the external communication channel itself — it produces the structured content and logs that it was generated and approved by Dr. Priya at a specific timestamp.

---

## What the Medical Reviewer Workspace Does NOT Do

To maintain focus and avoid scope creep:

- **Does not manage queries operationally** — Dr. Priya does not create, assign, or resolve clinical data queries. That is the CDM's domain. The context card may surface query history as background information, but query management is read-only in this workspace.
- **Does not show team workloads** — Dr. Priya has no team in CluePoints. She is not responsible for managing CDM or central monitor performance. Team workload data is not surfaced in this workspace.
- **Does not approve risk tier changes** — risk tier approvals are the Risk Lead's authority. Even if a safety flag has risk tier implications, Dr. Priya's role is to make the medical judgment; the risk tier decision flows separately to the Risk Lead.
- **Does not produce regulatory submissions** — Dr. Priya's structured decision notes are operational clinical judgment records, not regulatory artifacts. They may be referenced in regulatory review, but the platform does not format or submit them to regulatory authorities. Regulatory submission preparation is a distinct workflow outside this scope.
- **Does not surface portfolio-level or cross-study signals** — Dr. Priya reviews specific items that have been escalated to her. She does not have a study health overview, a site risk dashboard, or a program-level view. Her workspace is item-by-item by design. (See Open Question 5 for nuance on whether a lightweight study-level view is ever warranted.)
- **Does not replace the safety reporting system** — for studies with a formal pharmacovigilance or safety reporting obligation, the platform may need to interface with dedicated safety databases (e.g., Argus, ARISg). This workspace does not replicate that functionality. It generates the clinical judgment record; the safety database integration is a separate concern.

---

## Information Hierarchy

How information flows to and from the Medical Reviewer workspace:

```
External Safety Committee / Medical Monitor
        ↑ (safety committee referrals, structured escalation documents)
        │
┌───────────────────────────────────────────────────────┐
│          MEDICAL REVIEWER WORKSPACE                   │  ← this brief
│                                                       │
│  Governance lane — separate from operational          │
│  monitoring lanes                                     │
│                                                       │
│  Review Queue  │  Item Context Card                   │
│  AI Narrative  │  Decision Surface                    │
│  Communication │  Audit Trail                         │
└───────────────────────────────────────────────────────┘
        ↑ (escalations in)                  ↓ (decisions out)
        │                                   │
CDM Workspace         ←→         Item history (visible to
Central Monitor Workspace              CDM, CM, SM)
Study Manager Workspace                     │
                                            ↓
                                 Escalating party's
                                 workspace (decision
                                 outcome + required
                                 follow-up action)
```

**Key structural point:** The Medical Reviewer workspace sits in a distinct governance lane. It does not sit in the CDM → SM → Risk Lead operational chain. Items enter it via escalation from any operational role (CDM, Central Monitor, Study Manager). Decisions exit it back to the escalating party and into the item's permanent history. The Medical Reviewer workspace does not push to the Risk Lead or Program Manager workspaces directly — if a safety event has portfolio-level implications, that escalation happens through normal operational channels (Study Manager → Program Manager), not through Dr. Priya.

---

## Resolved Design Decisions

### Reactive-First Design — Landing State (RESOLVED 2026-02-23)

**Problem:** Dr. Priya's queue is empty most of the time. A workspace that looks like an empty, broken dashboard every time she logs in will erode trust and adoption. But the workspace also cannot look "fine" when there are urgent items waiting.

**Decision:** The workspace landing state is designed to be clean and explicit about its status:

- **Empty state:** A clear "Your review queue is empty" confirmation, with the last-checked timestamp prominently displayed. The visual treatment is calm and reassuring — not a wall of empty panels. No placeholder content, no fake structure. Just the confirmation, the timestamp, and a low-prominence navigation path for the rare case where Dr. Priya wants to review past completed items.
- **Non-empty state:** The queue is the first thing she sees. Items are listed with full metadata (type, study, age, escalating party). New items since last login are visually distinguished. There is no dashboard clutter competing for her attention — the queue is the workspace when items exist.

**Out-of-platform notification is required as part of this decision:** The empty-state design is only viable if Dr. Priya is reliably notified when items arrive. The notification must include sufficient context (item type, study, escalating party) for her to assess urgency before logging in. Notification delivery method (email / platform push / both) is configurable per user. The platform is responsible for sending the notification at the moment of escalation, not on a scheduled batch.

---

### "New Since Last Login" is a First-Class Signal (RESOLVED 2026-02-23)

**Problem:** Unlike the Study Manager (who logs in daily and has a manageable delta), Dr. Priya may have been away for 5–14 days. Items in her queue are not homogeneous — some may have arrived recently, some may have been waiting for days and have accumulated additional activity in the interim. She needs to understand the state of each item relative to her last session, not just the current state.

**Decision:** Every item card in the review queue must carry three time-oriented signals:

1. **Escalation timestamp** — when the item was originally escalated to her queue (absolute date and time)
2. **Current age** — how long the item has been waiting for her review, displayed as "X days, Y hours" — shown prominently, color-coded by aging threshold
3. **"What happened while you were away" summary** — if any actions were taken on the item since her last login (CDM added data, SM added a note, another reviewer commented), this is surfaced at the card level as a brief, scannable summary. She does not need to open the item to know that something changed.

**Aging thresholds (suggested defaults, configurable per organization):**
- 0–48 hours: neutral (no color)
- 48–96 hours: amber — item is aging, may warrant attention
- 96+ hours: red — item has been waiting significantly; SLA breach may be approaching (see Open Question 3 on SLA fallback)

---

## Open Questions

The following questions remain open before PRD authoring:

| # | Question | Why it matters | Owner |
|---|----------|---------------|-------|
| 1 | Does the Medical Reviewer have direct access to patient-level data from within the workspace (individual adverse event records, patient data listings), or does she navigate to a separate EDC or data module for that? | This is a compliance and access control question, not a UX question. The answer determines the architecture of the Item Context Card, the data residency model, and likely has 21 CFR Part 11 and GDPR implications. If patient data lives in the EDC and CluePoints does not hold it, the context card must use a deep-link model rather than a native data surface. | Product / Legal / Data Architecture |
| 2 | Are there multiple Medical Reviewers assigned to a study, or typically one? If multiple, can they see each other's review queues, or is each queue strictly private? | Affects routing logic (which reviewer gets which item), visibility model (shared vs. private queue), and what happens when a reviewer is unavailable. If queues are private and a reviewer is unreachable, items may become stranded. | Product / Clinical Operations |
| 3 | What happens to an item if Dr. Priya is unreachable for 5+ days — is there a fallback reviewer, and does the platform need to surface an SLA breach to the Study Manager? | If no fallback mechanism exists in the platform, items can age indefinitely with no escalation path. This is a patient safety risk and an operational gap. The platform may need to surface aging items in the Study Manager's Decision Queue as a secondary alert when Dr. Priya's review SLA is breached. | Product / Clinical Operations |
| 4 | Is there a regulatory-mandated format for safety review documentation that the structured decision note templates must conform to? | ICH E6(R2) and 21 CFR Part 11 have requirements for audit trails and electronic signatures. If the structured note templates must conform to a specific regulatory format (e.g., a defined safety review form), the template design is not purely a UX decision — it must be validated against the applicable regulatory requirements. A regulatory affairs consultant should review the template design before PRD authoring. | Regulatory Affairs / Product |
| 5 | Does a Medical Reviewer ever need to see anything about study-level health (site distribution, enrollment, overall risk status), or is the workspace always purely item-by-item? | If Dr. Priya sometimes needs study-level context to interpret a safety flag (e.g., "is this the only site showing this pattern, or is it systemic?"), the AI narrative may be sufficient — or a lightweight study health summary may need to be surfaced within the context card. If study-level context is never relevant to her judgment, the item-by-item design is complete and no study health panel is needed. | Clinical / UX Research |

---

## Acceptance Criteria (MVP)

The Medical Reviewer workspace is considered complete for MVP when:

**Review Queue:**
- [ ] Dr. Priya can log in and see all items currently assigned to her review, with item type, study, site, anonymized patient ID, age since escalated, and escalating party visible on each item card without opening the item
- [ ] Items that arrived after her last login are visually distinguished from items that were already present at her last login
- [ ] Each item card shows any actions taken on the item since her last login ("what happened while you were away") as a scannable summary at the card level
- [ ] Items aged 48–96 hours are displayed with an amber aging indicator; items aged 96+ hours are displayed with a red aging indicator
- [ ] An empty queue state displays a "Your review queue is empty" message with a last-checked timestamp; the empty state does not look broken or incomplete
- [ ] When a new item is escalated to Dr. Priya's queue, an out-of-platform notification (email or push, per user preference) is sent at the moment of escalation, including item type, study name, escalating party, and a direct link to the item

**Item Context Card:**
- [ ] When Dr. Priya opens any item, the full context card is pre-assembled and ready — no loading wait, no navigation required
- [ ] The context card surfaces the underlying data record or data pattern relevant to the flag
- [ ] The context card surfaces the complete chronological history of actions taken on the item, from original signal creation through the current escalation
- [ ] The context card surfaces the relevant protocol specification or safety monitoring threshold that the item was flagged against
- [ ] If prior medical reviews of this item exist (item was previously reviewed and returned), they are visible in the item history within the context card
- [ ] Any actions taken on the item while Dr. Priya was away since her last login are clearly surfaced in the item history

**AI-Generated Context Narrative:**
- [ ] An AI-generated clinical context narrative is ready when Dr. Priya opens any item — it is not generated on demand after opening
- [ ] The narrative includes: relevant data trend, comparable cases from the same study (if any), the protocol specification the item was flagged against, a summary of prior actions, and a plain-language clinical summary
- [ ] Dr. Priya can annotate the narrative with comments; annotations are saved and appear in the item history
- [ ] Dr. Priya can flag an incomplete or inaccurate narrative; the flag is logged and surfaces to the escalating party
- [ ] Items with incomplete AI narratives are marked with an "incomplete" indicator on the item card in the review queue, visible before Dr. Priya opens the item
- [ ] The AI narrative is clearly labeled as AI-generated context, not as a recommendation; no decision language or recommended action appears in the narrative

**Decision Surface:**
- [ ] For each item type (Safety Flag, Protocol Deviation, Data Anomaly), the correct set of decision options is presented — no free-form decision field
- [ ] Each decision option presents a structured note template with the required fields for that decision type; free text is permitted within fields, but the field structure is fixed
- [ ] Submitted decisions are auto-stamped with actor identity (Dr. Priya), timestamp, and item reference
- [ ] Submitted decisions cannot be edited — they can only be superseded by a subsequent review action, which is itself logged and visible in the item history
- [ ] All decisions and structured notes are visible in the item history of the context card, accessible to the escalating party after Dr. Priya submits

**Communication Surface:**
- [ ] After submitting a decision, Dr. Priya can communicate the outcome to the escalating party (CDM, Central Monitor, or Study Manager) via a structured message template tied to the item
- [ ] "Request additional data" decisions generate a structured request message to the escalating party with the required data specified, responsible party, and expected timeline
- [ ] "Escalate to safety committee" decisions generate a structured referral document (exportable) with Dr. Priya's clinical observations, urgency level, and reference to prior reviews
- [ ] All communications are logged in the item history with actor, timestamp, and content
- [ ] Messages to CDMs and Study Managers are delivered into their workspace feed (not only as a platform notification)
- [ ] After sending a "request additional data" communication, the item moves to a "pending" state in Dr. Priya's queue; when data is returned and the item is re-escalated, the item resurfaces in her queue with the new data integrated into the context card and AI narrative

**Audit Trail:**
- [ ] Every action taken in the workspace — opening an item, annotating the AI narrative, submitting a decision, sending a communication — is logged with actor identity, timestamp, and item reference
- [ ] The audit log for any item is complete and readable from the item history panel in the context card
- [ ] Audit log entries cannot be edited or deleted by any workspace user
- [ ] All structured decision notes are included in the audit log in their complete templated form, not as free-text summaries

---

*Document created: 2026-02-23*
*Parent: product-brief-Testing-2026-02-22.md*
*Next step: PRD authoring — Medical Reviewer workspace functional requirements*
