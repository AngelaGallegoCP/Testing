---
date: 2026-02-23
author: Root
parent: feature-brief-study-manager-workspace-2026-02-23.md
status: pending stakeholder input
---

# Stakeholder Questions: Study Manager Workspace
## Two design-blocking questions before PRD authoring can proceed

---

These two questions came out of the Study Manager workspace feature brief. Both have multiple plausible answers and each answer leads to a materially different workspace design. We need stakeholder input before we write functional requirements.

Estimated conversation time: 20–30 minutes.

---

## Question 1: Org Model — CRO-side or Sponsor-side Study Manager?

### What we're asking

When Elena (our Study Manager persona) logs into CluePoints, is she:

**(A)** A **CRO employee** running the study on behalf of a sponsor — her "team" is other CRO staff (CDMs, central monitors), and the sponsor is an external oversight party above her

**(B)** A **sponsor employee** who owns the study internally — the CRO is a vendor she oversees, not a team she manages

**(C)** Both — CluePoints needs to support both configurations depending on the customer

### Why this matters for the workspace

| Design element | CRO-side SM | Sponsor-side SM |
|----------------|-------------|-----------------|
| "My team" in workload view | CRO CDMs, CRO central monitors | Sponsor-side oversight staff + CRO contacts |
| Escalation routing | Up to sponsor-side risk lead / PM | Up to internal risk lead / PM |
| Data access model | Scoped to studies where their CRO is engaged | Scoped to their study portfolio |
| Team workload visibility | They see CRO staff workload | May or may not see CRO staff workload (depends on contract) |
| Risk plan authority | Executes risk plan defined by sponsor | Owns the risk plan |

### What we need to know

1. Which org model do the majority of current CluePoints customers use?
2. Is there a dominant model we should design for first, with the other as a later configuration option?
3. If both must be supported at launch, is the workspace structurally the same but with different data scoping — or are they functionally different enough to require separate workspace designs?

### What "Option C" implies for engineering

If both must coexist: the workspace needs an org-model configuration at the tenant or study level that tells it which version of "my team" to show, which escalation paths to expose, and what data the SM can see. This is buildable but adds meaningful complexity to the permissions model.

---

## Question 2: Is the Study Manager Ever the Risk Owner?

### What we're asking

In the RBQM (Risk-Based Quality Management) model CluePoints supports, someone owns the risk plan for a study — they define KRI thresholds, review adherence, and approve risk tier changes. We have a **Risk Lead** persona (David) who does this in our current model.

The question is: in some customer organizations, does the **Study Manager also play the Risk Lead role** — i.e., there is no separate Risk Lead, and Elena both runs the study AND owns the risk plan?

**(A)** No — Risk Lead and Study Manager are always distinct roles in organizations that use CluePoints

**(B)** Sometimes — smaller organizations or smaller studies may not have a dedicated risk lead; the SM absorbs that responsibility

**(C)** Often — the "Risk Lead" in our persona model is more of a function than a job title; many SMs effectively do this work

### Why this matters for the workspace

The Study Manager workspace brief currently has a hard boundary: **risk governance belongs to the Risk Lead workspace**, and the SM can only escalate to it, not operate within it.

If the SM is sometimes the risk owner, that boundary breaks:

| Scenario | Workspace implication |
|----------|-----------------------|
| Always distinct (A) | Current design holds — SM escalates to Risk Lead, Risk Lead has governance panel |
| Sometimes the same (B) | SM workspace needs a "risk owner mode" — a panel or view that surfaces KRI thresholds, adherence, and tier change approvals when no separate Risk Lead is assigned |
| Often the same (C) | The Risk Lead workspace may not be a separate persona at all — it may be a role that gets layered onto the SM workspace conditionally |

### What we need to know

1. In the customer organizations you know best, is there always a dedicated risk lead distinct from the study manager?
2. If not, what happens to risk governance tasks — does the SM do them, does a program manager absorb them, or are they unowned?
3. For MVP: should we design the workspace assuming the roles are always distinct, then layer on "SM-as-risk-owner" support in a later release? Or is this a day-one requirement?

### What "Option C" implies for the overall workspace architecture

If the Risk Lead and Study Manager can be the same person, the workspace architecture simplifies at the top (one fewer persona workspace) but gets more complex for the SM (their workspace conditionally expands to include risk governance). The PRD would need to define this as a role-composition model rather than two separate fixed personas.

---

## Recommended decision format

For each question, we need:

1. A clear answer to which scenario applies (A, B, or C above)
2. If "C" (both/all): which scenario is the **primary design target** for MVP, and which is a later release
3. Any known customer examples that anchor the answer

---

## What happens after these questions are answered

- Q1 answered → can finalize the data access model and team workload panel design
- Q2 answered → can finalize whether Risk Lead is a separate workspace or a conditional role within SM workspace
- Both answered → PRD authoring can begin for the Study Manager workspace

---

*Created: 2026-02-23*
*Blocking: PRD authoring for Study Manager workspace*
*Stakeholder: [to be filled]*
