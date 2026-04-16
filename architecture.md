# Epics, Features & User Stories — CaseFlow

| | |
|---|---|
| **Author** | Abdul Sammad Talha |
| **Version** | 1.2 |
| **Date** | April 2025 |
| **Total Epics** | 3 |
| **Total Features** | 8 |
| **Total User Stories** | 28 |

---

## Story Format

```
As a [persona],
I want [goal],
So that [benefit].

Acceptance Criteria:
- Given / When / Then (for key stories)
- Checklist format (for standard stories)
```

**Estimation:** T-shirt sizing — XS / S / M / L / XL  
**Priority:** MoSCoW — M / S / C / W

---

---

# EPIC 1 — Unified Case Timeline

> **Epic Goal:** Any agent who opens a case should be able to see the complete, chronological story of that case — every channel, every event, every artefact — without switching to another tool.

---

## Feature 1.1 — Multi-Channel Event Aggregation

### US-001 — View unified case timeline

**Priority:** M | **Size:** L

```
As a support agent (Sana),
I want to see all events related to a case — from email, chat, WhatsApp, Slack, Jira, and phone — in a single chronological timeline,
So that I can understand the full history of a case without opening multiple applications.
```

**Acceptance Criteria:**
- Given a case with linked events on 4 channels, when I open the case in CaseFlow, then all events appear in the timeline in correct chronological order
- Given two events at the same minute, they are ordered by sub-minute timestamp
- Given a channel event with no summary available, a default label is shown (e.g., "Slack message — click to view")
- Each event displays: channel icon, timestamp, actor, summary, and artefact link

---

### US-002 — View channel-specific event details

**Priority:** M | **Size:** S

```
As a support agent,
I want to click on any timeline event to see the full content of that communication,
So that I can read the complete message, transcript, or document without leaving CaseFlow.
```

**Acceptance Criteria:**
- [ ] Clicking a chat event opens the full transcript in a side panel
- [ ] Clicking a WhatsApp photo event opens the full-resolution image in a modal
- [ ] Clicking a Jira event shows ticket status, assignee, and latest comment
- [ ] Clicking a Slack event shows the full thread in context

---

### US-003 — Filter timeline by channel

**Priority:** S | **Size:** S

```
As a support agent,
I want to filter the case timeline by one or more channels (e.g., "show only WhatsApp and email"),
So that I can focus on the communications relevant to my current task.
```

**Acceptance Criteria:**
- [ ] Channel filter pills are available above the timeline
- [ ] Selecting a filter immediately updates the timeline (no page reload)
- [ ] Multiple filters can be active simultaneously
- [ ] "Clear filters" button restores full timeline

---

### US-004 — View media attachments inline

**Priority:** M | **Size:** M

```
As a support agent,
I want to view photos and documents shared by the customer (e.g., via WhatsApp) directly in the case timeline,
So that I have the visual evidence available when making resolution decisions.
```

**Acceptance Criteria:**
- [ ] Photos display as thumbnails in the timeline event row
- [ ] Clicking a thumbnail opens a full-resolution viewer
- [ ] Source channel, sender, and timestamp are shown below each photo
- [ ] PDF documents open in an in-app viewer or download prompt

---

## Feature 1.2 — Case Linking

### US-005 — Manually link a communication to a case

**Priority:** M | **Size:** M

```
As a support agent,
I want to search for and manually link a communication (e.g., an email, a Slack message) to an open case,
So that I can consolidate related communications that weren't automatically detected.
```

**Acceptance Criteria:**
- Given I search by order ID or customer email, when I select a result, then it is added to the case timeline as a new event
- Given a communication is already linked to another case, I receive a warning before linking
- [ ] Manual link action is recorded in the audit trail

---

### US-006 — Review and confirm AI-suggested case links

**Priority:** S | **Size:** M

```
As a support agent,
I want to see AI-suggested links when the system detects a related communication on another channel,
So that I don't miss relevant information that wasn't manually connected.
```

**Acceptance Criteria:**
- [ ] Suggested link appears as a banner: "We found a related Slack thread about Order #45821 — Add to case?"
- [ ] Suggestion shows confidence score and reason (e.g., "Matched: same order ID")
- [ ] Agent can confirm or dismiss with a single click
- [ ] Dismissed suggestions do not reappear for the same item

---

### US-007 — View case linking history

**Priority:** C | **Size:** XS

```
As a support team lead,
I want to see a log of all manually linked and auto-linked events for a case,
So that I can audit how the case was assembled.
```

**Acceptance Criteria:**
- [ ] Case history panel shows: event type (manual / auto-suggested / confirmed), actor, timestamp

---

---

# EPIC 2 — AI Case Intelligence

> **Epic Goal:** Agents should be able to ask any question about a case in plain language and receive a sourced, accurate answer in under 5 seconds — reducing cognitive load and the risk of missing critical information.

---

## Feature 2.1 — Conversational AI Chat Interface

### US-008 — Ask a plain-language question about a case

**Priority:** M | **Size:** XL

```
As a support agent (Sana),
I want to type a plain-language question about the case I'm viewing and receive an accurate, cited answer,
So that I can get case intelligence instantly without reading through every event manually.
```

**Acceptance Criteria:**
- Given I ask "What photos has the customer provided?", then the AI responds with a summary of each photo event, citing the WhatsApp event, date, and sender
- Given I ask a question whose answer is not in the case data, then the AI responds "I couldn't find information about this in the current case data" — it does not guess or hallucinate
- Given a valid question, the AI responds within 5 seconds
- Every response includes at least one source citation in the format: [Channel · Date · Actor]

---

### US-009 — Ask follow-up questions in the same session

**Priority:** S | **Size:** M

```
As a support agent,
I want to ask follow-up questions that reference my previous question without repeating context,
So that I can have a natural conversation with the AI rather than rephrasing every query.
```

**Acceptance Criteria:**
- [ ] "And when did they say that?" correctly refers to the subject of the previous question
- [ ] Session context persists for the duration of the case view session
- [ ] Navigating away and returning starts a new session (clearly indicated)

---

### US-010 — Copy an AI response

**Priority:** S | **Size:** XS

```
As a support agent,
I want to copy an AI-generated answer to my clipboard,
So that I can paste key case details into a Zendesk note, Slack message, or email.
```

**Acceptance Criteria:**
- [ ] Copy icon available on every AI response
- [ ] Copied text includes source citations

---

## Feature 2.2 — Case Summary

### US-011 — Generate a one-click case summary

**Priority:** M | **Size:** L

```
As a support agent,
I want to generate a one-click AI case summary,
So that I can quickly understand a case I've never seen before, or prepare a handoff note.
```

**Acceptance Criteria:**
- Given I click "Summarise Case", then a summary is generated within 8 seconds containing:
  - Issue type and description
  - Customer sentiment trend
  - Key events in chronological order (max 5 bullets)
  - Current status
  - Outstanding actions
  - Recommended next step
- Summary is labelled "AI-generated — verify before sharing"
- Summary is copyable

---

### US-012 — Generate a handoff note

**Priority:** S | **Size:** M

```
As a support agent,
I want to generate a formatted handoff note for a colleague taking over a case,
So that the incoming agent has full context without reading the entire timeline.
```

**Acceptance Criteria:**
- [ ] Handoff note includes: case ID, customer name, issue summary, what has been done, what is pending, suggested next action
- [ ] Note is formatted for copy-paste into Zendesk internal note or Slack
- [ ] Agent can edit the note before saving or sharing

---

## Feature 2.3 — Missing Artefact Detection

### US-013 — See missing artefact flags on case header

**Priority:** M | **Size:** L

```
As a support agent,
I want to see a clear flag on the case view when required evidence or confirmations are missing,
So that I know what to request before calling or emailing the customer.
```

**Acceptance Criteria:**
- Given a damage claim case with no customer photos linked, then a red flag displays: "⚠ Missing: Customer photo evidence (required for damage claims)"
- Given all required artefacts are present, the case header shows a green "✓ All required evidence present" indicator
- Flags update automatically when new events are linked to the case
- Clicking a flag shows which requirement rule triggered it

---

### US-014 — View missing artefacts for all team cases

**Priority:** S | **Size:** M

```
As a support team lead (Bilal),
I want to see a list of all cases with missing artefact flags from the team dashboard,
So that I can proactively identify and unblock cases before they breach SLA.
```

**Acceptance Criteria:**
- [ ] Dashboard card: "Cases with missing artefacts: [N]" links to a filtered case list
- [ ] List shows: case ID, case type, missing artefact name, age of case, assigned agent

---

## Feature 2.4 — AI Draft Responses

### US-015 — Request a draft resolution email

**Priority:** S | **Size:** L

```
As a support agent,
I want to ask the AI to draft a resolution email based on the case data,
So that I can send a professional, accurate response without writing it from scratch.
```

**Acceptance Criteria:**
- [ ] Agent types: "Draft a refund approval email" → AI produces a draft email containing: customer name, order ID, resolution type, next steps
- [ ] Draft is pre-filled with actual case data, not placeholder text
- [ ] Draft is clearly labelled "Draft — review before sending"
- [ ] Agent can edit the draft in an inline editor before copying

---

### US-016 — Request a draft internal escalation note

**Priority:** C | **Size:** M

```
As a support agent,
I want to ask the AI to draft an internal escalation note for my team lead,
So that I can clearly communicate the case situation without spending time writing it up.
```

**Acceptance Criteria:**
- [ ] Draft includes: case summary, reason for escalation, urgency, and suggested action
- [ ] Note is formatted for internal use (concise, factual, no customer-facing language)

---

---

# EPIC 3 — Case Management & Operations

> **Epic Goal:** Agents and team leads should be able to manage case lifecycle, track SLA health, and monitor team operations — all within CaseFlow.

---

## Feature 3.1 — SLA Management

### US-017 — View SLA countdown on every case

**Priority:** M | **Size:** M

```
As a support agent,
I want to see an SLA countdown timer on every case I open,
So that I know how much time I have before a response or resolution is due.
```

**Acceptance Criteria:**
- [ ] Timer shows time remaining in hours and minutes
- [ ] Timer turns amber at 25% time remaining
- [ ] Timer turns red at 10% time remaining
- [ ] Paused/elapsed state shown clearly when SLA is breached

---

### US-018 — Receive SLA breach alerts (Team Lead)

**Priority:** M | **Size:** M

```
As a support team lead,
I want to receive an in-app notification when a case is approaching SLA breach (at 25% time remaining),
So that I can reassign or intervene before the deadline is missed.
```

**Acceptance Criteria:**
- [ ] Notification appears in the notification panel: "Case #4421 — SLA breach in 45 minutes — Assigned to: Sana"
- [ ] Notification links directly to the case
- [ ] Notification is dismissible and logged as "acknowledged"

---

## Feature 3.2 — Case Status & Notes

### US-019 — Update case status

**Priority:** M | **Size:** S

```
As a support agent,
I want to update the status of a case (Open / In Progress / Pending Customer / Resolved / Closed),
So that the team has accurate visibility of where each case stands.
```

**Acceptance Criteria:**
- [ ] Status dropdown available on the case header
- [ ] Every status change is recorded in the timeline as: "[Agent name] changed status to [New Status] · [Timestamp]"
- [ ] Resolved and Closed statuses require a resolution code to be selected

---

### US-020 — Add internal notes

**Priority:** M | **Size:** S

```
As a support agent,
I want to add internal notes to a case that are visible only to the support team,
So that I can document investigation steps, agent-to-agent instructions, or decisions without exposing them to the customer.
```

**Acceptance Criteria:**
- [ ] Internal note field available on the case view
- [ ] Notes display with an "Internal" badge and are visually distinct from customer communications
- [ ] Notes are excluded from any customer-facing case exports or AI draft responses

---

## Feature 3.3 — Team Dashboard

### US-021 — View team case overview (Team Lead)

**Priority:** S | **Size:** L

```
As a support team lead (Bilal),
I want a real-time dashboard showing all open cases, their statuses, SLA health, and key risk flags,
So that I can manage team workload and proactively prevent SLA breaches and escalations.
```

**Acceptance Criteria:**
- [ ] Dashboard shows: total open cases, breakdown by status, SLA health (% cases healthy/at risk/breached)
- [ ] A "Needs Attention" section surfaces: cases with missing artefacts, cases nearing SLA breach, unassigned cases
- [ ] Dashboard refreshes automatically every 5 minutes (or on manual refresh)
- [ ] Each case row links directly to the full case view

---

### US-022 — Filter dashboard by agent or case type

**Priority:** C | **Size:** S

```
As a support team lead,
I want to filter the dashboard by assigned agent or case type,
So that I can review workload for a specific agent or monitor a specific type of dispute.
```

**Acceptance Criteria:**
- [ ] Filter options: agent (multi-select), case type (multi-select), date range
- [ ] Filters apply without page reload
- [ ] Active filters are clearly labelled

---

## Feature 3.4 — Case Search & Access

### US-023 — Search for a case

**Priority:** M | **Size:** M

```
As a support agent,
I want to search for any case by order ID, customer name, email, or case ID,
So that I can quickly find the case I need without browsing a list.
```

**Acceptance Criteria:**
- [ ] Global search available from any screen
- [ ] Results appear within 1 second for exact matches
- [ ] Results show: case ID, customer name, case type, status, last updated
- [ ] Partial matches are supported

---

### US-024 — View recently accessed cases

**Priority:** S | **Size:** XS

```
As a support agent,
I want to see a list of cases I recently accessed,
So that I can quickly return to cases I was working on without searching.
```

**Acceptance Criteria:**
- [ ] "Recent cases" list shows last 10 accessed cases on the home screen
- [ ] Each item shows: case ID, customer name, status, last accessed time

---

### US-025 — Assign or reassign a case

**Priority:** M | **Size:** S

```
As a support team lead,
I want to assign or reassign any case to an agent,
So that I can balance workload and ensure no case goes unattended.
```

**Acceptance Criteria:**
- [ ] Agent dropdown available on the case header
- [ ] Reassignment recorded in the case timeline with actor and timestamp
- [ ] Assigned agent receives an in-app notification on reassignment

---

## Feature 3.5 — Agent Preferences

### US-026 — Set case type notification preferences

**Priority:** C | **Size:** S

```
As a support agent,
I want to choose which case types and channels trigger in-app notifications for me,
So that I receive relevant alerts without being overwhelmed by noise.
```

**Acceptance Criteria:**
- [ ] Notification preferences accessible from user settings
- [ ] Per-channel and per-case-type toggle available
- [ ] Changes take effect immediately without re-login

---

### US-027 — Toggle timeline view density

**Priority:** C | **Size:** XS

```
As a support agent,
I want to switch between a compact timeline view (event summaries only) and a detailed view (full event content),
So that I can choose the right level of detail for my current task.
```

---

### US-028 — Export case timeline as PDF

**Priority:** C | **Size:** M

```
As a support team lead,
I want to export a case timeline as a PDF,
So that I can share a complete case record with legal, compliance, or external parties.
```

**Acceptance Criteria:**
- [ ] Export includes: case header, full chronological timeline, internal notes (toggle), AI-generated summary (optional)
- [ ] PDF is generated within 10 seconds for cases with up to 200 events
- [ ] Export is recorded in the case audit log with actor and timestamp
