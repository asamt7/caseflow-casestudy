# Non-Functional Requirements — CaseFlow

| | |
|---|---|
| **Author** | Abdul Sammad Talha |
| **Version** | 1.0 |
| **Date** | April 2025 |
| **Total Requirements** | 12 |

---

> **PoC Note:** NFRs marked with `[PoC]` have relaxed targets appropriate for prototype validation. Production targets are defined for post-PoC roadmap planning.

---

## NFR-PERF — Performance

### NFR-PERF-001 — Case Timeline Load Time

**Requirement:** The case timeline shall load and render all linked events within **2 seconds** for cases containing up to 100 events across 6 channels.

| Context | Target |
|---|---|
| PoC | ≤5 seconds (10 concurrent users, test data) |
| Production | ≤2 seconds (P95) at 500 concurrent users |

**Measurement:** Synthetic load test using Locust; timed from case URL navigation to full timeline render.  
**Acceptance:** P95 latency ≤ stated target across 100 test runs.

---

### NFR-PERF-002 — AI Chat Response Latency

**Requirement:** The AI case chat interface shall return a complete response within **5 seconds** for standard case interrogation queries.

| Context | Target |
|---|---|
| PoC | ≤8 seconds (single user, test case) |
| Production | ≤5 seconds (P90) under normal load |

**Measurement:** Client-side timing from query submission to last token rendered.  
**Acceptance:** 90% of queries in a pilot session respond within the target window.  
**Note:** Responses exceeding 3 seconds shall display a typing/thinking indicator to prevent perceived unresponsiveness.

---

### NFR-PERF-003 — Channel Event Ingestion Latency

**Requirement:** A new event on any connected channel (e.g., customer WhatsApp message) shall appear on the case timeline within **60 seconds** of its creation.

| Channel | Target |
|---|---|
| Zendesk (webhook) | ≤15 seconds |
| Slack (event API) | ≤15 seconds |
| WhatsApp (Twilio webhook) | ≤60 seconds |
| Jira (webhook) | ≤60 seconds |
| Email (polling) | ≤5 minutes |

**Acceptance:** 95% of events across each channel meet their respective latency targets during a 1-hour integration test.

---

## NFR-SCAL — Scalability

### NFR-SCAL-001 — Concurrent Users

**Requirement:** The system shall support the following concurrent user loads without degradation in performance beyond the stated NFR-PERF targets:

| Context | Target |
|---|---|
| PoC | 10 concurrent users |
| Phase 1 Production | 100 concurrent users |
| Phase 2 Production | 500 concurrent users |

**Architecture note:** Horizontal scaling via containerised deployment (Docker + Kubernetes) is required for production targets.

---

### NFR-SCAL-002 — Case Volume

**Requirement:** The system shall support a case data store of up to **500,000 cases** without query performance degradation, with individual cases containing up to **500 linked events** across channels.

**Measurement:** Database query benchmarks at 10%, 50%, and 100% of stated case volume.

---

## NFR-SEC — Security

### NFR-SEC-001 — Data Encryption

**Requirement:** All customer communication data shall be encrypted:
- **At rest:** AES-256 encryption for all stored case data, artefacts, and AI-generated summaries
- **In transit:** TLS 1.3 for all API communications and user-facing connections

**Verification:** Security audit of infrastructure configuration prior to any production deployment.

---

### NFR-SEC-002 — Authentication & Authorisation

**Requirement:** The system shall enforce role-based access control (RBAC) with a minimum of three roles:

| Role | Permissions |
|---|---|
| **Agent** | View and interact with assigned cases; add internal notes; use AI chat |
| **Team Lead** | All Agent permissions + view all team cases + access dashboard + manage case assignments |
| **Admin** | All Team Lead permissions + manage integrations + configure case type rules + manage users |

**Acceptance:** Attempting to access a resource outside role permissions returns HTTP 403. No privilege escalation possible via API manipulation.

---

### NFR-SEC-003 — AI Data Handling

**Requirement:** Customer communication data processed by the AI layer shall:
1. Never be used as training data for any LLM model
2. Be processed via inference-only API calls with no persistent storage at the LLM provider
3. Be anonymised at the field level (customer PII masked) before being passed to external LLM APIs

**Verification:** Data flow audit confirming PII masking at the API boundary. Contractual DPA with all AI API providers confirming no training data retention.

---

### NFR-SEC-004 — Audit Logging

**Requirement:** The system shall maintain an immutable audit log recording: user ID, action performed, case ID, timestamp, and IP address for all case access events, data exports, and permission changes.

**Retention:** Audit logs retained for minimum 12 months.  
**Access:** Audit logs accessible only to Admin role; cannot be deleted by any user role.

---

## NFR-AVAIL — Availability

### NFR-AVAIL-001 — Uptime

**Requirement:** The production system shall maintain **99.5% uptime** measured monthly, excluding scheduled maintenance windows communicated ≥48 hours in advance.

| Context | Target |
|---|---|
| PoC | Best-effort; no SLA |
| Production | 99.5% monthly uptime |

**Measurement:** External uptime monitoring (e.g., Pingdom) with 1-minute check intervals.

---

### NFR-AVAIL-002 — Graceful Degradation

**Requirement:** If a channel integration (e.g., Slack API) becomes unavailable, the system shall:
1. Continue to display all previously fetched events from that channel
2. Display a clear indicator: *"Slack — last synced 14 minutes ago. Live data temporarily unavailable."*
3. Not fail the entire case view or AI chat interface

**Acceptance:** Simulated channel API failure results in degraded-but-functional case view, not an error state.

---

## NFR-USE — Usability

### NFR-USE-001 — Onboarding Time

**Requirement:** A support agent with no prior CaseFlow training shall be able to:
- Load a case and read the full timeline — within **2 minutes** of first access
- Ask the AI chat a case question and act on the response — within **5 minutes** of first access

**Measurement:** Usability test with 5 agents who have not seen the tool. Time-to-task measured by observer.  
**Acceptance:** 4 out of 5 agents meet both targets.

---

### NFR-USE-002 — Accessibility

**Requirement:** The web interface shall conform to **WCAG 2.1 Level AA** standards, including:
- Keyboard navigability for all core workflows
- Minimum colour contrast ratio of 4.5:1 for all text
- Screen reader compatibility for the case timeline and AI chat interface

---

## NFR-COMP — Compliance

### NFR-COMP-001 — Data Privacy

**Requirement:** The system shall support GDPR compliance obligations including:
- **Right to erasure:** Ability to delete all case data associated with a specific customer within 72 hours of a verified deletion request
- **Data portability:** Ability to export all case data for a specific customer in a machine-readable format (JSON)
- **Data residency:** All customer data stored within the EU (or customer's selected region) by default

**Acceptance:** Erasure workflow tested end-to-end. Export function tested for completeness. Infrastructure deployment verified to correct region.
