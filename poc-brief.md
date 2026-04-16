# Product Requirements Document — CaseFlow

| | |
|---|---|
| **Product** | CaseFlow — Multi-Channel Case Orchestration Platform |
| **Author** | Abdul Sammad Talha |
| **Version** | 1.2 |
| **Date** | April 2025 |
| **Status** | Draft — PoC Validation |

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Problem Background](#2-problem-background)
3. [Market Context](#3-market-context)
4. [Product Vision & Strategy](#4-product-vision--strategy)
5. [Target Users](#5-target-users)
6. [Key Use Cases](#6-key-use-cases)
7. [Feature Overview](#7-feature-overview)
8. [Requirements Summary](#8-requirements-summary)
9. [Success Metrics](#9-success-metrics)
10. [Risks & Mitigations](#10-risks--mitigations)
11. [Timeline & Milestones](#11-timeline--milestones)
12. [Open Questions](#12-open-questions)

---

## 1. Executive Summary

CaseFlow is an AI-powered multi-channel case orchestration platform for e-commerce support teams. It solves the single most painful problem in complex case management: **the story of a case is scattered across channels that don't talk to each other.**

When a customer reports a damaged order via live chat, follows up on WhatsApp with photos, triggers a Slack escalation, generates a Jira ticket, and eventually receives resolution via email — that case has a complete story. But no agent can read it in one place. CaseFlow changes that.

At its core, CaseFlow does three things:

1. **Converges** all communications — customer-facing and internal — into a single, chronological, sourced case timeline
2. **Intelligently links** related interactions across channels using AI, even when they weren't manually connected
3. **Answers questions** about any case in plain language: *"What evidence has the customer provided?"* *"What's missing before we can approve the refund?"* *"What did the warehouse team say on Slack?"*

The PoC targets mid-market e-commerce teams (10–100 agents) handling 500+ complex cases per month.

---

## 2. Problem Background

### 2.1 The Multi-Channel Reality

Modern e-commerce support spans an average of **8–12 active communication channels**. The channels fall into two groups:

**Customer-facing:** Live chat, email, WhatsApp/SMS, phone, social media DMs  
**Internal:** Slack, Microsoft Teams, Jira, internal CRM notes, warehouse management system updates

For simple cases (order status, basic returns), this isn't a problem — a single-channel interaction resolves in minutes. But **complex cases** — damaged items, missing high-value orders, fraud disputes, chargeback investigations, multi-party return disputes — consistently span multiple channels across multiple days.

### 2.2 The Current State Pain

A field research exercise mapping the journey of 10 complex e-commerce cases (anonymised) revealed the following:

| Metric | Finding |
|---|---|
| Average channels touched per complex case | 5.3 |
| Average time an agent spends reconstructing case context | 22 minutes |
| Cases where a second agent had to re-ask the customer for information already provided | 7 out of 10 |
| Cases where a Slack thread containing critical case information was not visible to the resolving agent | 6 out of 10 |
| Cases where missing evidence was only discovered during the resolution call | 4 out of 10 |

### 2.3 The Cost

- Agents toggle between applications ~1,200 times per day, losing ~5 working weeks per year to context switching
- 77% of customers cite repeating themselves as their most frustrating support experience
- Complex cases that span 3+ channels have 34% lower CSAT than single-channel cases
- Average handling time for L2+ cases is 2.8× higher than L1 cases — but only 40% of that time is spent on actual resolution work

---

## 3. Market Context

### 3.1 Competitive Landscape

| Platform | Strengths | CaseFlow Gap |
|---|---|---|
| **Zendesk** | Enterprise omnichannel, 1,500+ integrations | Ticket-centric; no internal channel convergence; no AI case interrogation |
| **Gorgias** | Deep Shopify integration, e-commerce native | Limited integrations; no unified internal+external timeline |
| **Gladly** | Unified customer conversation timeline | No internal channels; no AI interrogation; broad B2C, not e-commerce native |
| **Kustomer** | CRM-native unified timeline | No Slack/Jira convergence; AI focuses on automation not interrogation |
| **Salesforce Service Cloud** | Enterprise-grade CRM + case management | Complexity and cost; manual case merging; no AI interrogation layer |

### 3.2 The Whitespace

No platform currently bridges **external customer communications** with **internal team communications** about the same case, applies AI to auto-link and contextualise that combined timeline, and exposes it through a natural language interface for agent interrogation.

CaseFlow occupies this whitespace.

---

## 4. Product Vision & Strategy

### 4.1 Vision Statement

> *Every support agent should be able to understand the full story of any case — from any channel, at any moment — in under 30 seconds.*

### 4.2 Strategic Positioning

CaseFlow is not a ticketing system, a CRM, or a customer communication platform. It is an **intelligence layer** that sits above existing tools, reads from them, and presents a coherent, conversational view of case reality.

This means:
- It **does not replace** Zendesk, Slack, or Jira — it **orchestrates** them
- It **does not handle** customer communication directly — agents do, using their existing tools
- It **does not resolve** cases — it **enables** agents to resolve them faster and more confidently

### 4.3 Product Principles

1. **Source transparency always** — every piece of information shown must be attributed to its source channel, timestamp, and actor
2. **Suggest, don't decide** — AI recommendations are clearly labelled as suggestions; the agent always acts
3. **Zero extra channel** — CaseFlow should never become another channel to monitor; it reads from existing ones
4. **Privacy by design** — no customer PII used for AI training; all LLM processing is inference-only against anonymised case data

---

## 5. Target Users

See [Project Charter — Personas](project-charter.md#5-user-personas) for full persona profiles.

**Primary:** Sana — L2 Support Agent (daily active user)  
**Secondary:** Bilal — Support Team Lead (daily oversight user)  
**Tertiary:** Omar — Support Ops Manager (weekly metrics user)

---

## 6. Key Use Cases

### UC-01: Complex Damage Claim — Complete Case Reconstruction

**Actor:** L2 Support Agent (Sana)  
**Trigger:** Agent opens a case that was initiated 48 hours ago by a different agent and now requires resolution

**Current experience:**
1. Open Zendesk ticket — read partial history
2. Search email for customer correspondence
3. Scroll through Slack to find the escalation thread
4. Check Jira to see if a warehouse ticket was raised
5. Check WhatsApp Business to find the customer's photos
6. Call customer — realise photos didn't load, ask customer to resend

**CaseFlow experience:**
1. Open CaseFlow case view
2. See complete timeline: *"Chat · Mon 10:14 · Customer reported damage · [Transcript]"*, *"WhatsApp · Mon 10:47 · Customer sent 3 photos · [Photos]"*, *"Slack · Mon 11:02 · Sana → #returns: 'High-value item, escalating to warehouse' · [Thread]"*, *"Jira · Mon 11:05 · WH-4421 created · [Link]"*
3. Ask AI: *"Is there anything missing before I can approve the refund?"*
4. AI responds: *"Warehouse confirmation from Jira ticket WH-4421 is still pending. Customer has provided 3 photos (WhatsApp, Mon 10:47). No fraud flag on account. You have all customer-side evidence; waiting on internal sign-off."*
5. Resolve in 4 minutes

---

### UC-02: Case Handoff — Agent Absence

**Actor:** L2 Support Agent covering for an absent colleague  
**Trigger:** Agent needs to handle a case she has never seen before

**CaseFlow experience:**
1. Open case, see AI-generated summary: *"3-day-old damaged item dispute. Customer Ayesha Khan provided photos on WhatsApp. Warehouse confirmed batch defect on Jira. Awaiting resolution offer approval from team lead. Customer has contacted 3 times — patience running low (sentiment: frustrated)."*
2. Agent understands full context in 45 seconds
3. Resolves with confidence

---

### UC-03: Proactive Gap Detection

**Actor:** Support Team Lead (Bilal)  
**Trigger:** Morning case review

**CaseFlow experience:**
1. Opens team dashboard
2. Sees 3 cases flagged: *"Missing: customer photo evidence (WhatsApp)"*, *"Missing: warehouse confirmation (Jira)"*, *"SLA breach in 2 hours — no agent assigned"*
3. Re-assigns and nudges agents before SLA breaches

---

## 7. Feature Overview

### Feature 1 — Unified Case Timeline

A single chronological view of every interaction across all connected channels, for one case. Each event shows: channel icon, timestamp, actor (customer / agent / system), summary, and a link to the full artefact.

**What it solves:** Eliminates the need to switch between 8 tabs to reconstruct case history.

---

### Feature 2 — AI Case Chat Interface

A conversational chat panel within the case view. Agents type questions in plain language and receive answers grounded in the actual case data, with citations.

Example questions:
- *"What has the customer said about the damage?"*
- *"What's the current status of the Jira ticket?"*
- *"Has the warehouse team responded?"*
- *"What's missing before I can close this case?"*
- *"Summarise this case for my team lead"*
- *"Draft a resolution email based on what we've agreed"*

**What it solves:** Removes the cognitive burden of synthesising multi-channel information manually.

---

### Feature 3 — Smart Case Linking

AI-powered detection of related conversations across channels that belong to the same case but haven't been manually linked. Uses order ID, customer identifier, product SKU, and semantic similarity to auto-suggest links.

Example: An email mentioning "order #45821" and a Slack thread about "the blue jacket return from yesterday" are auto-linked when the system detects they reference the same order.

**What it solves:** Prevents case fragmentation where the same incident generates parallel unlinked threads.

---

### Feature 4 — Missing Artefact Detection

Automatic analysis of what evidence, confirmations, or approvals are expected for a given case type and what is currently present vs. absent.

Case type rules (configurable):
- Damage claim → requires: customer photos, carrier confirmation OR warehouse inspection, approval from team lead
- High-value refund (>£200) → requires: fraud check pass, proof of return or warehouse receipt
- Chargeback dispute → requires: delivery confirmation, signed order record, communication history export

**What it solves:** Agents discover missing evidence before customer calls, not during them.

---

### Feature 5 — Case Summary Generation

One-click AI-generated case summary covering: issue type, customer sentiment trend, timeline of key events, current status, outstanding actions, and recommended next step.

Designed for: handoffs, escalations, and management reviews.

---

### Feature 6 — SLA Monitoring & Alerts

Real-time SLA countdown per case with team lead notifications for cases approaching breach. SLA rules configurable by case type and priority.

---

### Feature 7 — Team Dashboard

Overview for team leads showing: open cases by status, SLA health, cases flagged for missing artefacts, cases with high customer sentiment risk (negative trend), and agent workload distribution.

---

## 8. Requirements Summary

See full detail in:
- [Functional Requirements](functional-requirements.md)
- [Non-Functional Requirements](non-functional-requirements.md)

**22 Functional Requirements** across 5 categories: Case Orchestration, AI Intelligence, Channel Integration, Case Management, and Reporting.

**12 Non-Functional Requirements** covering performance, scalability, security, availability, usability, and compliance.

---

## 9. Success Metrics

### PoC Success Criteria

| Metric | Target |
|---|---|
| Time to reconstruct case context | ≤5 minutes (vs. 22-minute baseline) |
| AI case chat accuracy (agent-rated) | ≥85% of responses rated "helpful" or "accurate" |
| Missing artefact detection precision | ≥90% — flag is correct when raised |
| Agent net promoter score (post-pilot) | ≥+30 |
| Cases where agent had to ask customer to repeat info | ≤10% (vs. 70% baseline) |

### Production Success Criteria (Post-PoC)

| Metric | Target |
|---|---|
| Average handling time (complex cases) | ≥20% reduction |
| First contact resolution rate | ≥15% improvement |
| CSAT for multi-channel cases | ≥10 point improvement |
| Agent context-switching time | ≥50% reduction |
| SLA breach rate | ≥30% reduction |

---

## 10. Risks & Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| LLM produces inaccurate case summaries | High | RAG-only responses; every claim cited to source; human review before action |
| Channel API rate limits causing delays | Medium | Caching layer; async fetch on case open; graceful degradation messaging |
| Agent distrust of AI recommendations | Medium | Transparent sourcing; "suggested" labelling; agent always decides |
| Data privacy / GDPR non-compliance | High | No training on customer data; data residency controls; DPA-compliant API usage |
| Scope creep to full ticketing system | Medium | Strict "intelligence layer only" positioning; no communication sending features in PoC |

---

## 11. Timeline & Milestones

| Phase | Duration | Deliverables |
|---|---|---|
| **Discovery & Documentation** | 2 weeks | Charter, PRD, FR, NFR, User Stories |
| **Design** | 1 week | Wireframes, Architecture |
| **PoC Build — Core** | 3 weeks | Case timeline, AI chat, Zendesk + Slack integration |
| **PoC Build — Intelligence** | 2 weeks | Missing artefact detection, case summary, smart linking |
| **Pilot Testing** | 1 week | 5 agents, 50 test cases, feedback collection |
| **PoC Review & Sign-off** | 1 week | Pilot results, go/no-go for Phase 1 build |

**Total PoC Timeline: 10 weeks**

---

## 12. Open Questions

| # | Question | Owner | Due |
|---|---|---|---|
| 1 | What is the maximum data retention period for case communications under GDPR? | Legal / DPO | Week 2 |
| 2 | Which telephony provider is in use — does it support call transcript export via API? | Engineering | Week 1 |
| 3 | Does the existing Slack workspace have Enterprise Grid (required for cross-channel message API access)? | IT | Week 1 |
| 4 | What is the acceptable latency for AI chat responses before agents lose confidence in the tool? | UX Research | Week 3 |
| 5 | Should case linking suggestions require manual approval, or should they be auto-applied below a confidence threshold? | Product / Team Lead | Week 2 |
| 6 | What case types should be in scope for missing artefact detection rules in PoC? | Support Ops | Week 2 |
