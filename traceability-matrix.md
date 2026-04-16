# PoC Brief — CaseFlow

| | |
|---|---|
| **Author** | Abdul Sammad Talha |
| **Version** | 1.0 |
| **Date** | April 2025 |
| **PoC Duration** | 8 Weeks |
| **Goal** | Validate core value proposition with synthetic data before full build |

---

## 1. PoC Objective

Demonstrate that an AI-powered unified case timeline, combined with a plain-language chat interface, meaningfully reduces the time and effort required for a support agent to understand and act on a complex e-commerce case.

**PoC is a success if:**
1. An agent can reconstruct a 6-channel case history in under 5 minutes (vs. 22-minute baseline)
2. The AI chat interface answers case questions accurately (≥85% agent-rated accuracy)
3. Missing artefact detection flags the right gaps with ≥90% precision
4. At least 4 out of 5 pilot agents rate the tool as "more useful than my current setup"

---

## 2. PoC Scope

### In Scope
- Unified case timeline (4 channels: Zendesk, Slack, WhatsApp, Jira)
- AI case chat interface with RAG-grounded responses and source citations
- One-click case summary generation
- Missing artefact detection for 3 case types (Damaged Item, Missing Order, Return Dispute)
- Basic case status management
- Web-based UI (desktop only for PoC)
- Synthetic test data (no live customer data)

### Out of Scope for PoC
- Email integration
- Phone/transcript integration
- Real-time SLA alerts
- Team lead dashboard
- Case export / PDF generation
- Mobile responsive layout
- Production security hardening
- Performance optimisation (targets relaxed for PoC — see NFRs)

---

## 3. PoC Build Plan

### Week 1–2: Foundation

**Goal:** Project setup, data models, and synthetic test data ready

Tasks:
- [ ] Initialise repo: React frontend + FastAPI backend + Docker Compose
- [ ] Define PostgreSQL schema: `cases`, `case_events`, `channels`, `users`
- [ ] Set up ChromaDB and embedding pipeline
- [ ] Create 10 synthetic test cases with realistic multi-channel events
- [ ] Build basic case list and case detail page (no AI yet)
- [ ] Implement JWT auth with 3 test users (agent, team lead, admin)

**Deliverable:** App runs locally; test cases load correctly.

---

### Week 3–4: Channel Integration (Simulated)

**Goal:** All 4 channels feeding events into the case timeline

Tasks:
- [ ] Build event normaliser (maps raw webhook payload → CaseEvent schema)
- [ ] Simulate Zendesk: mock webhook endpoint, process ticket events
- [ ] Simulate Slack: mock webhook endpoint, process thread messages
- [ ] Simulate WhatsApp: mock webhook endpoint, process messages + media
- [ ] Simulate Jira: mock webhook endpoint, process ticket status changes
- [ ] Render unified timeline in correct chronological order with channel icons
- [ ] Add channel filter pills

**Deliverable:** 10 test cases each with 4+ timeline events from 4 channels.

---

### Week 5–6: AI Intelligence Layer

**Goal:** AI chat and case summary working end-to-end

Tasks:
- [ ] Implement embedding pipeline: chunk case events → embed → store in Chroma
- [ ] Build RAG retrieval: query → embed → vector search (filtered by case_id) → top-k chunks
- [ ] Build LangGraph agent graph: retrieve → build context → call Claude Sonnet → format response
- [ ] Implement source citation extraction and JSON formatting
- [ ] Build AI chat UI panel (split view with timeline)
- [ ] Implement one-click case summary (structured 6-part output)
- [ ] Add "Draft reply" quick action
- [ ] Implement PII masking before LLM API calls

**Deliverable:** Agent can ask questions about any test case and receive cited answers.

---

### Week 7: Missing Artefact Detection

**Goal:** System flags gaps in evidence based on case type rules

Tasks:
- [ ] Build configurable artefact rule engine (JSON config per case type)
- [ ] Implement rule evaluation against case events on each timeline load
- [ ] Build missing artefact banner UI component
- [ ] Test against all 10 test cases (including cases with intentional gaps)
- [ ] Build plain-language "What to do" guidance per missing artefact

**Deliverable:** Damage claim test case correctly flags missing warehouse confirmation.

---

### Week 8: Pilot, Testing & Review

**Goal:** Real agents test the PoC; feedback collected; go/no-go decision

Tasks:
- [ ] Onboard 5 pilot agents with 10-minute walkthrough
- [ ] Each agent works through 5 assigned test cases using CaseFlow
- [ ] Collect feedback via structured survey (5 questions, 1–5 scale)
- [ ] Record time-to-reconstruct-context for each case
- [ ] Document bugs, usability issues, and improvement requests
- [ ] Compile PoC results report
- [ ] Present go/no-go recommendation to stakeholders

**Deliverable:** PoC results report with pilot data and Phase 1 recommendation.

---

## 4. AI Tooling Decisions

### Why LangGraph?

LangGraph enables stateful, conditional agent workflows — essential for CaseFlow where the AI pipeline has branching logic:
- Different retrieval strategies for different query types (factual vs. summary vs. gap detection)
- Context accumulation across follow-up questions
- Fallback handling when retrieved context is insufficient

### Why Claude Sonnet?

- Strong instruction following — reliably produces structured JSON with citations
- Low hallucination rate when constrained to provided context
- Handles long context windows well (important for cases with many events)
- Anthropic's commercial API terms explicitly permit inference on customer support data (no training retention)

### Why ChromaDB for PoC?

- Zero infrastructure: runs embedded in the Python process
- Python-native: no additional service to manage
- Supports metadata filtering by `case_id` — retrieval is always scoped to the current case
- Migration to Pinecone Serverless at production is a 2-day effort (same API shape)

### Embedding Strategy

Each `CaseEvent` is chunked into 2 pieces:
1. **Metadata chunk:** `channel | timestamp | actor_type | actor_name`
2. **Content chunk:** `event_summary + first 500 chars of raw_content`

Both chunks are stored with metadata: `{ case_id, event_id, channel, timestamp }` enabling filtered retrieval.

---

## 5. Test Data Design

10 synthetic test cases covering the target case types:

| Case ID | Type | Channels | Complexity | Gaps |
|---|---|---|---|---|
| TC-001 | Damaged Item | Chat, WA, Slack, Jira | High | Missing warehouse conf. |
| TC-002 | Missing Order | Email, Chat, Jira | Medium | None — fully complete |
| TC-003 | Wrong Item | Chat, WA, Email | Low | Missing return confirmation |
| TC-004 | Return Dispute | Email, Slack, Jira | High | Missing courier tracking |
| TC-005 | Damaged Item | Chat, WA, Slack | Medium | None — resolved |
| TC-006 | Chargeback | Email, Phone, Jira | High | Missing signed order record |
| TC-007 | Missing Order | Chat, Email | Low | None — awaiting courier |
| TC-008 | Wrong Item | WA, Slack, Jira | Medium | Missing customer approval |
| TC-009 | Return Dispute | Email, Chat, Slack | High | Multiple gaps |
| TC-010 | Damaged Item | Chat, WA, Email, Slack, Jira | Very High | None — all present |

Each case includes: realistic customer names (anonymised), realistic event content, varied sentiment trends (positive → frustrated, neutral throughout, frustrated → resolved).

---

## 6. PoC Success Measurement

### Quantitative Metrics

| Metric | Measurement Method | Target |
|---|---|---|
| Time-to-context | Stopwatch: case open → agent states "I understand the full situation" | ≤5 minutes |
| AI accuracy | Post-session survey: "The AI answers were accurate" (1–5) | ≥4.0 average |
| False positive rate (artefact flags) | Manual review of all flags across 10 cases | ≤10% false positives |
| Agent productivity score | "This would save me time vs. my current tools" (1–5) | ≥4.0 average |

### Qualitative Feedback (Survey Questions)

1. How easy was it to understand the full case history using CaseFlow? (1–5)
2. How accurate were the AI chat responses? (1–5)
3. How useful was the missing artefact detection? (1–5)
4. How likely are you to use CaseFlow in your daily work? (1–5)
5. What is the one thing you would most like to change or add?

---

## 7. Risks During PoC

| Risk | Likelihood | Mitigation |
|---|---|---|
| LLM response quality below expectations | Medium | Tune system prompt; add few-shot examples; adjust retrieval parameters |
| Synthetic data feels unrealistic to pilots | Low | Involve one pilot agent in test data design (Week 1) |
| PoC scope expands during build | Medium | Weekly scope check; strict "Week 8 is testing, not building" rule |
| API rate limits during pilot testing | Low | PoC uses cached responses for repeated test case queries |

---

## 8. Phase 1 Roadmap (Post-PoC)

If PoC succeeds, Phase 1 build prioritises:

1. **Real channel integrations** — Live Zendesk, Slack, WhatsApp, Jira APIs
2. **Email integration** — Gmail/Outlook IMAP ingestion
3. **Team lead dashboard** — SLA monitoring, team workload view
4. **SLA alert system** — Real-time notifications at 25% / 10% remaining
5. **Production security** — AES-256 at rest, PII masking audit, RBAC hardening
6. **Performance optimisation** — Caching layer, async event ingestion, P95 latency targets

Estimated Phase 1 timeline: **12 weeks** with a 2-engineer + 1 BA team.
