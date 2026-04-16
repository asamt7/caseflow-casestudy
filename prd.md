# Project Charter — CaseFlow

| | |
|---|---|
| **Project Name** | CaseFlow — Multi-Channel Case Orchestration Platform |
| **Author** | Abdul Sammad Talha |
| **Role** | Business Analyst · Product Owner · Product Manager |
| **Version** | 1.0 |
| **Date** | April 2025 |
| **Status** | PoC Phase |

---

## 1. Problem Statement

E-commerce support teams managing complex cases — damaged items, missing orders, return disputes, chargeback investigations — routinely work across 6–10 different communication channels simultaneously. A single case may involve:

- A live chat transcript where the issue was first reported
- WhatsApp messages with product damage photos
- An internal Slack thread where the agent escalated to the warehouse team
- A Jira ticket tracking the investigation
- Email threads exchanging resolution offers with the customer
- A phone call transcript where the customer followed up

No existing tool brings all of this together. Agents spend **3+ hours per day** manually switching between platforms, re-reading context, and reconstructing case histories. Customers — **77% of them** — report the most frustrating part of e-commerce support is having to repeat themselves when they reach a new agent or channel.

The result: slower resolution times, higher operational costs, lower CSAT scores, and agent burnout.

---

## 2. Product Vision

> *"For any support agent handling a complex e-commerce case, CaseFlow is the single source of truth — a unified, AI-powered case intelligence layer that converges every channel into one timeline and answers any question about the case in plain language."*

---

## 3. Objectives

| # | Objective | Success Metric |
|---|---|---|
| 1 | Reduce agent context-switching time | ≥50% reduction in time spent gathering case context |
| 2 | Unify all case communications in one view | 100% of linked channel events visible in case timeline |
| 3 | Enable AI-assisted case interrogation | Agent can answer any case question in <30 seconds |
| 4 | Improve first-contact resolution | FCR rate improvement of ≥15% vs. baseline |
| 5 | Reduce average handling time | AHT reduction of ≥20% for complex cases (L2+) |
| 6 | Improve CSAT for complex cases | CSAT improvement of ≥10 points for cases spanning 3+ channels |

---

## 4. Scope

### In Scope (PoC)
- Case timeline view aggregating: email, live chat, WhatsApp, Slack, Jira, phone (transcript)
- AI chat interface for case interrogation
- Missing artefact detection and flagging
- Case summary generation
- Next-action recommendations
- Manual case linking across channels
- Integration with Zendesk (primary ticketing system)

### Out of Scope (PoC)
- Autonomous AI resolution (AI suggests, agent acts)
- Customer-facing portal
- Payment/refund processing
- Real-time agent co-browsing
- Mobile native app
- Integration with 3PL warehouse management systems (Phase 2)

---

## 5. User Personas

### Persona 1 — The Frontline Agent (Primary)

**Name:** Sana  
**Role:** L2 Customer Support Agent, E-commerce  
**Experience:** 2 years in support, handles 40–60 cases/day  

**Daily Reality:**
- Has 8 browser tabs open: Zendesk, Gmail, Slack, WhatsApp Business, Jira, Shopify admin, carrier portal, internal wiki
- Spends ~3 hours/day switching between tools to gather context on complex cases
- Frequently has to ask colleagues "can you remind me what happened with this case?" because the thread is buried in Slack
- Gets frustrated when customers call and ask for an update she has to piece together on the fly

**Goals:**
- See everything about a case in one place
- Know immediately what's missing before getting on a customer call
- Get help drafting resolution emails without starting from scratch every time

**Frustrations:**
- "I feel like I'm a detective piecing together a crime scene, not a support agent"
- "I've apologised to customers for not knowing things I should know because the information is in 4 different places"

---

### Persona 2 — The Support Team Lead (Secondary)

**Name:** Bilal  
**Role:** Support Team Lead, manages 12 agents  
**Experience:** 5 years in CX, 2 in leadership  

**Daily Reality:**
- Reviews escalated cases and makes final resolution decisions
- Needs to quickly understand the full history of a case when it lands on his desk
- Tracks SLA breaches and case backlog across the team
- Coaches agents on resolution quality

**Goals:**
- Instant full-picture overview of any escalated case
- Visibility into which cases are at risk of SLA breach
- Data on which channel combinations create the most friction

**Frustrations:**
- "When a case gets escalated to me, I still have to read 3 Slack threads and 2 email chains to understand what's going on"
- "I can't proactively manage SLA risk because I don't know where cases are until they're already breached"

---

### Persona 3 — The Support Operations Manager (Tertiary)

**Name:** Omar  
**Role:** Support Operations Manager  
**Experience:** 8 years in operations and CX strategy  

**Goals:**
- Reduce operational cost per case resolution
- Use data to justify tooling investments to leadership
- Identify process inefficiencies from cross-channel case patterns

---

## 6. Assumptions

1. The organisation uses Zendesk as the primary ticketing system
2. Internal team communication happens on Slack
3. Customer photo evidence is shared via WhatsApp Business API
4. Engineering/warehouse escalations are tracked in Jira
5. Phone calls are recorded and transcribable via existing telephony setup
6. Agents are technically capable of operating a web-based interface
7. Data privacy and security requirements will be addressed before production deployment

---

## 7. Constraints

| Constraint | Detail |
|---|---|
| **Budget** | PoC must be achievable with API-level integrations and open-source AI tooling |
| **Timeline** | PoC target: 8 weeks from kick-off |
| **Team** | Solo BA/PM; development resource assumed for implementation phase |
| **Data** | No live customer PII to be used in PoC; synthetic/anonymised test data only |

---

## 8. Risks

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| Channel API rate limits restricting real-time data fetch | Medium | Medium | Implement caching layer; batch fetch on case open |
| LLM hallucination producing incorrect case summaries | Medium | High | RAG-grounded responses only; citation of source for every claim |
| Agent adoption resistance to new tool | Low | High | Design around existing Zendesk workflow; minimise behaviour change |
| Data privacy concerns with AI processing customer communications | High | High | Data residency controls; opt-in per case; no training on customer data |
| Integration complexity with legacy ticketing systems | Medium | Medium | Start with Zendesk REST API; abstract integration layer for extensibility |

---

## 9. Stakeholders

| Stakeholder | Role | Interest Level |
|---|---|---|
| Support Team Lead | Internal champion | High — directly benefits |
| Frontline Agents | End users | High — daily users |
| CTO / Engineering | Technical approval | Medium — architecture sign-off |
| Data Privacy Officer | Compliance | High — AI + customer data |
| Support Ops Manager | ROI justification | High — cost and metrics |
