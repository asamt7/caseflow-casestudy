# Functional Requirements — CaseFlow

| | |
|---|---|
| **Author** | Abdul Sammad Talha |
| **Version** | 1.1 |
| **Date** | April 2025 |
| **Total Requirements** | 22 |

---

## Priority Key (MoSCoW)

| Code | Meaning |
|---|---|
| **M** | Must Have — PoC is not viable without this |
| **S** | Should Have — High value; include if capacity allows |
| **C** | Could Have — Nice to have; defer if needed |
| **W** | Won't Have (this phase) — Documented for future |

---

## Category 1 — Case Orchestration

| ID | Requirement | Priority | Acceptance Criteria |
|---|---|---|---|
| **FR-ORCH-001** | The system shall create a unified case timeline that aggregates events from all connected channels (email, live chat, WhatsApp, Slack, Jira, phone transcript) in chronological order. | M | Given a case with events on 3+ channels, all events appear on the timeline in correct chronological order within 10 seconds of case load. |
| **FR-ORCH-002** | Each timeline event shall display: channel source (with icon), timestamp, actor name/type (customer / agent / system), a plain-language summary of the event, and a link to the full artefact. | M | Every timeline event shows all 5 attributes. Missing data is displayed as "Not available" rather than blank. |
| **FR-ORCH-003** | The system shall allow agents to manually link a communication from any connected channel to an existing case. | M | Agent can search for an unlinked communication by order ID, customer email, or date range, and add it to a case with a single action. |
| **FR-ORCH-004** | The system shall use AI to auto-suggest cross-channel case links when it detects a shared order ID, customer identifier, or semantic similarity (confidence ≥ 0.85). | S | Auto-suggested link is presented with a confidence score and source rationale. Agent must confirm before the link is applied. |
| **FR-ORCH-005** | The system shall support attaching media artefacts (images, documents, audio files) directly to a case timeline event, with source channel and upload timestamp recorded. | M | Agent can open a photo sent via WhatsApp directly from the timeline event without leaving CaseFlow. |

---

## Category 2 — AI Case Intelligence

| ID | Requirement | Priority | Acceptance Criteria |
|---|---|---|---|
| **FR-AI-001** | The system shall provide a conversational AI chat interface within each case view, allowing agents to ask plain-language questions about the case. | M | Agent types a question and receives a response within 5 seconds. Response is grounded in case data with citations to source events. |
| **FR-AI-002** | Every AI response shall cite the specific channel event(s) that support the answer, including channel name, timestamp, and actor. | M | No AI response is returned without at least one source citation. If no relevant source exists, the AI states "I couldn't find information about this in the current case data." |
| **FR-AI-003** | The system shall generate a one-click case summary covering: issue type, customer sentiment trend, key timeline events, current status, outstanding actions, and recommended next step. | M | Summary generates within 8 seconds. Contains all 6 required components. Summary is clearly labelled "AI-generated — verify before sharing." |
| **FR-AI-004** | The AI chat interface shall support a "draft response" command, producing a suggested resolution email or message for the agent to review and edit before sending. | S | Agent types "draft a refund approval email" and receives a draft populated with case-specific details (order ID, resolution type, customer name). Draft is labelled as a suggestion. |
| **FR-AI-005** | The system shall detect and flag missing artefacts based on configurable case type rules (e.g., damage claim requires: customer photos, carrier confirmation, team lead approval). | M | For a damage claim with no customer photos, the system displays a "Missing: Customer photo evidence" flag on the case header within 30 seconds of case load. |
| **FR-AI-006** | The system shall analyse customer message sentiment across all channels and display a sentiment trend indicator (Positive / Neutral / Frustrated / Escalating) for the case. | S | Sentiment indicator updates within 60 seconds of a new customer message being ingested. Sentiment is calculated across all channels, not just the most recent one. |
| **FR-AI-007** | The system shall support follow-up questions within the AI chat session, maintaining context from previous questions in the same case session. | S | Agent asks "What did the warehouse say?" followed by "And when did they say that?" — the second question correctly refers to the warehouse context from the first answer. |

---

## Category 3 — Channel Integration

| ID | Requirement | Priority | Acceptance Criteria |
|---|---|---|---|
| **FR-INT-001** | The system shall integrate with Zendesk via REST API to ingest ticket data, agent notes, customer messages, and ticket status changes. | M | A Zendesk ticket update is reflected in the CaseFlow case timeline within 60 seconds. |
| **FR-INT-002** | The system shall integrate with Slack to ingest messages from designated support channels and threads that have been linked to a case. | M | A Slack thread linked to a case displays all messages including author, timestamp, and any file attachments in the case timeline. |
| **FR-INT-003** | The system shall integrate with WhatsApp Business API (via Twilio) to ingest customer messages and media attachments. | M | Customer photos sent via WhatsApp are visible in the case timeline within 2 minutes of receipt, thumbnailed with a link to full resolution. |
| **FR-INT-004** | The system shall integrate with Jira to display linked ticket status, assignee, priority, and most recent comment in the case timeline. | M | Jira ticket status change (e.g., "In Progress" → "Done") is reflected in the case timeline within 5 minutes. |
| **FR-INT-005** | The system shall support ingestion of phone call transcripts (plain text or structured JSON) from connected telephony providers. | S | A plain-text call transcript is uploaded or fetched via API, chunked, and searchable via the AI chat interface within 3 minutes of call end. |

---

## Category 4 — Case Management

| ID | Requirement | Priority | Acceptance Criteria |
|---|---|---|---|
| **FR-CM-001** | The system shall display configurable SLA countdown timers per case, based on case type and priority, with visual indicators for healthy / at risk / breached states. | M | SLA timer turns amber at 25% time remaining and red at 10% remaining. Team lead receives an in-app notification at 25% remaining. |
| **FR-CM-002** | The system shall allow agents to add internal case notes visible only to the support team, separate from customer-facing communications. | M | Internal note is added to the timeline with a "Internal" label and is excluded from any customer-facing summary or export. |
| **FR-CM-003** | The system shall support case status management with the following states: Open, In Progress, Pending Customer, Pending Internal, Escalated, Resolved, Closed. | M | Agent can transition a case between any two states. Status change is recorded as a timeline event with actor and timestamp. |

---

## Category 5 — Reporting & Dashboard

| ID | Requirement | Priority | Acceptance Criteria |
|---|---|---|---|
| **FR-REP-001** | The system shall provide a team dashboard displaying: total open cases, cases by status, SLA health overview, cases with missing artefact flags, and top 5 cases by age. | S | Dashboard loads within 3 seconds and reflects data no older than 5 minutes. |
| **FR-REP-002** | The system shall allow team leads to filter the dashboard by agent, case type, date range, and channel. | C | Applying any filter combination updates the dashboard within 2 seconds without a full page reload. |
