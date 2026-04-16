# Wireframes — CaseFlow

| | |
|---|---|
| **Author** | Abdul Sammad Talha |
| **Version** | 1.1 |
| **Date** | April 2025 |
| **Format** | Text-based wireframes with annotations |

> These wireframes define layout, content hierarchy, and interaction behaviour for each screen. They are tool-agnostic and intended for Figma/Balsamiq translation.

---

## Screen Index

1. [Login Screen](#1-login-screen)
2. [Home — Agent Dashboard](#2-home--agent-dashboard)
3. [Case View — Unified Timeline](#3-case-view--unified-timeline)
4. [Case View — AI Chat Panel](#4-case-view--ai-chat-panel)
5. [Case View — Missing Artefacts](#5-case-view--missing-artefacts)
6. [Case Summary Modal](#6-case-summary-modal)
7. [Team Lead Dashboard](#7-team-lead-dashboard)
8. [Case Search & Results](#8-case-search--results)
9. [Channel Integration Settings](#9-channel-integration-settings)
10. [Mobile Compact View (Responsive)](#10-mobile-compact-view-responsive)

---

## 1. Login Screen

```
┌─────────────────────────────────────────────────────────┐
│                                                         │
│                    [CaseFlow Logo]                      │
│            Multi-Channel Case Orchestration             │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │  Work Email                                      │   │
│  │  ─────────────────────────────────────────────  │   │
│  │  [your.name@company.com                      ]  │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│  ┌─────────────────────────────────────────────────┐   │
│  │  Password                                        │   │
│  │  ─────────────────────────────────────────────  │   │
│  │  [••••••••••••                               ]  │   │
│  └─────────────────────────────────────────────────┘   │
│                                                         │
│            [    Sign In with SSO     ]                  │
│                      ── or ──                           │
│            [         Sign In         ]                  │
│                                                         │
│                   Forgot password?                      │
│                                                         │
└─────────────────────────────────────────────────────────┘
```

**Annotations:**
- Primary action: SSO login (recommended); email/password as fallback
- No "Create account" — accounts provisioned by Admin only
- Error state: inline below password field — "Invalid credentials. Try again."
- Successful login → redirect to Home Dashboard

---

## 2. Home — Agent Dashboard

```
┌──────────────────────────────────────────────────────────────────────┐
│  [CF] CaseFlow          🔍 Search cases...        🔔 (3)   [SA] ▾  │
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  👋 Good morning, Sana                                               │
│                                                                      │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌───────────┐  │
│  │  MY CASES   │  │  MISSING    │  │  SLA AT     │  │  RESOLVED │  │
│  │             │  │  ARTEFACTS  │  │  RISK       │  │  TODAY    │  │
│  │    14       │  │     3       │  │     2       │  │    8      │  │
│  │   Open      │  │  cases      │  │   cases     │  │  cases    │  │
│  └─────────────┘  └─────────────┘  └─────────────┘  └───────────┘  │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  MY CASES                                      [+ New Case]         │
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  ┌──────┬─────────────────────┬──────────────┬────────┬──────────┐  │
│  │ ID   │ Customer            │ Type         │ Status │ SLA      │  │
│  ├──────┼─────────────────────┼──────────────┼────────┼──────────┤  │
│  │ 4421 │ Ayesha Khan         │ Damaged Item │ ● Open │ 2h 14m ⚠ │  │
│  │ 4398 │ Usman Tariq         │ Missing Order│ ● Prog │ 8h 02m   │  │
│  │ 4387 │ Sara Malik          │ Wrong Item   │ ● Pend │ 1d 2h    │  │
│  │ 4371 │ Farhan Ahmed        │ Return Dispt │ ● Esc  │ 3h 41m ⚠ │  │
│  │ 4355 │ Layla Zuberi        │ Chargeback   │ ● Open │ 5h 20m   │  │
│  └──────┴─────────────────────┴──────────────┴────────┴──────────┘  │
│                                          [Show all 14 cases →]      │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  RECENT CASES                                                        │
│  ─────────────────────────────────────────────────────────────────  │
│  #4421 · Ayesha Khan · Damaged Item · Viewed 12 min ago             │
│  #4315 · Bilal Chaudhry · Return · Viewed 1 hour ago                │
│  #4290 · Nida Raza · Missing Order · Viewed yesterday               │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- Nav bar: persistent across all screens. [CF] = logo/home, search = global, 🔔 = notifications with badge, [SA] = avatar/menu (profile, settings, sign out)
- Status indicators: ● Open (blue), ● In Progress (amber), ● Pending (grey), ● Escalated (red)
- SLA column: ⚠ amber at 25% remaining, 🔴 red at 10% remaining
- Summary cards are clickable — click "3 Missing Artefacts" → filtered case list
- "+ New Case" creates a blank case shell

---

## 3. Case View — Unified Timeline

```
┌──────────────────────────────────────────────────────────────────────┐
│  [CF]    🔍                                          🔔   [SA] ▾   │
├──────────────────────────────────────────────────────────────────────┤
│  ← Back to My Cases                                                  │
│                                                                      │
│  Case #4421 — Damaged Item                            [⋮ Actions]   │
│  Ayesha Khan · ayesha.khan@email.com · Order #ORD-88214             │
│  Assigned: Sana A.     Status: [● Open ▾]     SLA: 2h 14m ⚠       │
│                                                                      │
│  ⚠ MISSING ARTEFACTS  ▸ Warehouse confirmation (Jira) not yet linked│
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  TIMELINE                    Filter: [All ▾] [Email][Chat][WA][Jira]│
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  MON 14 APR                                                          │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ 💬 Live Chat · 10:14 AM · Customer                            │  │
│  │ "Hi, I received my order but the screen is cracked."          │  │
│  │ [View full transcript →]                                      │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ 💬 Live Chat · 10:17 AM · Agent (Sana A.)                     │  │
│  │ "I'm sorry to hear that. Could you please send photos?"       │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ 📱 WhatsApp · 10:47 AM · Customer                             │  │
│  │ Sent 3 photos — [🖼] [🖼] [🖼]  ← click to expand            │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ 🔧 Slack · 11:02 AM · Sana A. → #returns-team                 │  │
│  │ "High value item - screen cracked on arrival. Escalating."    │  │
│  │ [View thread →]                                               │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ 🎯 Jira · 11:05 AM · System                                   │  │
│  │ Ticket WH-4421 created — "Batch defect check: SKU-8821"       │  │
│  │ Status: In Progress · Assignee: Warehouse QA                  │  │
│  │ [View ticket →]                                               │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ 📧 Email · 2:30 PM · Agent (Sana A.) → Customer               │  │
│  │ "We're investigating and will update you within 24h"          │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  TUE 15 APR                                                          │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ 📧 Email · 9:12 AM · Customer                                  │  │
│  │ "Any update? This is urgent."  [Sentiment: 😤 Frustrated]     │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│           ─── You are up to date ───                                 │
│                                                                      │
│  [+ Add internal note]            [🔗 Link a communication]         │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
                                                    [🤖 Ask AI  ▸]
```

**Annotations:**
- Missing artefact banner: amber, collapsible, links to the missing artefact rule
- Channel filter pills: multi-select; selected = filled; deselected = outline
- Each timeline event: left border colour coded by channel (blue=chat, green=WhatsApp, purple=Slack, orange=Jira, grey=email)
- Sentiment indicator on customer messages: 😊 Positive, 😐 Neutral, 😕 Concerned, 😤 Frustrated, 🔴 Escalating
- "🤖 Ask AI" FAB (floating action button): bottom right, always visible on case view, expands to AI chat panel

---

## 4. Case View — AI Chat Panel

```
┌──────────────────────────────────────────────────────────────────────┐
│  [Timeline Panel — 55% width]  │  [AI Chat Panel — 45% width]       │
│                                │                                     │
│  (timeline as shown above,     │  🤖 CaseFlow AI                    │
│   scrollable)                  │  Ask me anything about Case #4421   │
│                                │  ─────────────────────────────────  │
│                                │                                     │
│                                │  ┌────────────────────────────┐    │
│                                │  │ What evidence has the      │    │
│                                │  │ customer provided so far?  │    │
│                                │  └────────────────────────────┘    │
│                                │                                     │
│                                │  ┌────────────────────────────┐    │
│                                │  │ 🤖 The customer has         │    │
│                                │  │ provided:                  │    │
│                                │  │                            │    │
│                                │  │ 1. Verbal report of cracked│    │
│                                │  │    screen via live chat    │    │
│                                │  │    [💬 Chat · Mon 10:14]   │    │
│                                │  │                            │    │
│                                │  │ 2. Three photos of the     │    │
│                                │  │    damaged item sent via   │    │
│                                │  │    WhatsApp                │    │
│                                │  │    [📱 WhatsApp · Mon 10:47]│    │
│                                │  │                            │    │
│                                │  │ ⚠ Warehouse confirmation   │    │
│                                │  │ from Jira (WH-4421) is     │    │
│                                │  │ still pending.             │    │
│                                │  │                            │    │
│                                │  │                    [Copy]  │    │
│                                │  └────────────────────────────┘    │
│                                │                                     │
│                                │  ┌────────────────────────────┐    │
│                                │  │ What is the customer's     │    │
│                                │  │ current sentiment?         │    │
│                                │  └────────────────────────────┘    │
│                                │                                     │
│                                │  ┌────────────────────────────┐    │
│                                │  │ 🤖 Sentiment trend:         │    │
│                                │  │ 😐 Neutral → 😤 Frustrated  │    │
│                                │  │                            │    │
│                                │  │ The customer was neutral   │    │
│                                │  │ in live chat (Mon 10:14)   │    │
│                                │  │ but expressed urgency in   │    │
│                                │  │ a follow-up email (Tue     │    │
│                                │  │ 9:12 AM): "Any update?     │    │
│                                │  │ This is urgent."           │    │
│                                │  │ [📧 Email · Tue 9:12]      │    │
│                                │  │                    [Copy]  │    │
│                                │  └────────────────────────────┘    │
│                                │                                     │
│                                │  ─────────────────────────────────  │
│                                │  Quick actions:                    │
│                                │  [📋 Summarise]  [✍ Draft reply]   │
│                                │  [📤 Handoff note]                 │
│                                │  ─────────────────────────────────  │
│                                │                                     │
│                                │  ┌────────────────────────────┐    │
│                                │  │ Ask about Case #4421...  ↵ │    │
│                                │  └────────────────────────────┘    │
│                                │                                     │
└──────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- Split-panel layout: timeline remains visible while using AI chat
- Agent messages: right-aligned, grey background
- AI messages: left-aligned, white card with subtle blue left border
- Source citations: inline, styled as clickable pills — clicking scrolls timeline to that event
- "⚠" in AI responses: amber icon for gaps/warnings, distinct from error states
- Quick action buttons: pre-fill the chat input and auto-submit
- Input: multi-line, max 500 chars, Enter to submit (Shift+Enter for new line)

---

## 5. Case View — Missing Artefacts Panel

```
┌──────────────────────────────────────────────────────────────────────┐
│  Case #4421 — Damaged Item                                           │
│                                                                      │
│  ⚠ MISSING ARTEFACTS (1)                              [▴ Collapse]  │
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  Case type: Damaged Item requires:                                   │
│                                                                      │
│  ✅  Customer photo evidence         Found: WhatsApp · Mon 10:47    │
│  ⚠   Warehouse confirmation          Pending: Jira WH-4421 (open)  │
│  ✅  Agent internal note             Found: [Internal Note added]   │
│                                                                      │
│  What to do:                                                         │
│  › Jira ticket WH-4421 is still open. Confirm with the warehouse    │
│    team whether the batch defect investigation is complete.          │
│    [View Jira ticket →]   [Ask AI about this case →]                │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- Panel sits directly below the case header, above the timeline
- ✅ = met (green), ⚠ = pending (amber), ❌ = missing with no in-progress signal (red)
- "What to do" section: AI-generated plain-language guidance for the specific missing artefact
- Collapses into a single banner line when all items are ✅

---

## 6. Case Summary Modal

```
┌─────────────────────────────────────────────────────────────────────┐
│  📋 Case Summary — AI Generated                            [✕ Close]│
│  Case #4421 · Generated Tue 15 Apr 2025 · 11:02 AM                  │
│  ⚠ Review before sharing                                            │
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  ISSUE                                                               │
│  Damaged item — cracked screen on delivery. Order #ORD-88214,       │
│  Product: 10" Tablet (SKU-8821), Value: £349.                       │
│                                                                      │
│  CUSTOMER SENTIMENT                                                  │
│  😤 Trending frustrated — neutral at first contact, expressed       │
│  urgency in follow-up email (Tue 9:12 AM).                          │
│                                                                      │
│  TIMELINE (Key Events)                                               │
│  • Mon 10:14 — Customer reported cracked screen via live chat       │
│  • Mon 10:47 — Customer sent 3 photos via WhatsApp                  │
│  • Mon 11:02 — Escalated to warehouse team via Slack                │
│  • Mon 11:05 — Jira ticket WH-4421 raised (batch defect check)     │
│  • Tue 09:12 — Customer followed up via email, expressing urgency   │
│                                                                      │
│  CURRENT STATUS                                                      │
│  Open. Awaiting warehouse confirmation from Jira WH-4421.           │
│                                                                      │
│  OUTSTANDING ACTIONS                                                 │
│  1. Obtain warehouse confirmation from Jira WH-4421                 │
│  2. Issue resolution offer to customer (refund or replacement)      │
│                                                                      │
│  RECOMMENDED NEXT STEP                                               │
│  Chase Jira WH-4421 for an update. If batch defect confirmed,       │
│  issue full refund with no return required (item value < £500,      │
│  photos documented). Draft resolution email using AI.               │
│                                                                      │
│  [Copy Summary]  [Download PDF]  [Use for Handoff]   [✍ Edit]      │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- Modal overlay: centred, 80% width, scrollable if content exceeds viewport
- "⚠ Review before sharing" — always visible, non-dismissible
- All event references are hyperlinked to corresponding timeline events
- [Edit] — opens inline editor for agent to modify before sharing/exporting
- [Download PDF] — generates PDF version for external sharing

---

## 7. Team Lead Dashboard

```
┌──────────────────────────────────────────────────────────────────────┐
│  [CF]   🔍 Search                                    🔔 (5)  [BA] ▾│
├──────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  Team Overview — Bilal A.          Filter: [All agents ▾] [Today ▾]│
│                                                                      │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐    │
│  │  OPEN      │  │  SLA       │  │  MISSING   │  │  RESOLVED  │    │
│  │  CASES     │  │  AT RISK   │  │ ARTEFACTS  │  │  TODAY     │    │
│  │    47      │  │    6  ⚠    │  │    4  ⚠    │  │   23       │    │
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘    │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  🚨 NEEDS ATTENTION                                                  │
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  #4421  Damaged Item    Sana A.     ⚠ Missing: Warehouse conf.  2h  │
│  #4371  Return Dispute  Sana A.     🔴 SLA breach in 41 min         │
│  #4290  Chargeback      Unassigned  ⚠ No agent assigned             │
│  #4201  Wrong Item      Tariq B.    ⚠ Missing: Customer photos   5h │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  ALL TEAM CASES                   Search: [_________] [Export CSV]  │
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  Agent        Open  In Progress  Pending  Resolved  SLA Health      │
│  ─────────────────────────────────────────────────────────────────  │
│  Sana A.        8       4          2         8      ████████░░ 80%  │
│  Tariq B.       5       3          1         7      ██████████ 100% │
│  Nida R.        6       2          3         5      █████████░  90% │
│  Zara K.        4       1          0         3      ██████░░░░  60% │
│  Unassigned     3                                   ─              │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  CASE TYPE BREAKDOWN (Today)                                         │
│                                                                      │
│  Damaged Item    ██████████ 12                                       │
│  Missing Order   ████████   9                                        │
│  Wrong Item      ██████     7                                        │
│  Return Dispute  ████       5                                        │
│  Chargeback      ███        3                                        │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- Role-restricted: only visible to Team Lead and Admin roles
- "Needs Attention" section: auto-populated by system rules (SLA risk, missing artefacts, unassigned)
- SLA Health bar: percentage of that agent's open cases currently within SLA
- Clicking any case row → opens full case view
- Clicking "Unassigned" count → filtered list of unassigned cases with bulk-assign option

---

## 8. Case Search & Results

```
┌──────────────────────────────────────────────────────────────────────┐
│  [CF]                                                                │
│                                                                      │
│  🔍  damaged tablet ayesha                                 [✕ Clear]│
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  5 results                                                           │
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ #4421 · Damaged Item          ● Open          SLA: 2h 14m ⚠  │  │
│  │ Ayesha Khan · Order #ORD-88214 · Assigned: Sana A.            │  │
│  │ Last update: 9 minutes ago · 6 timeline events                │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │ #4178 · Damaged Item          ● Resolved      Closed 2d ago   │  │
│  │ Ayesha Khan · Order #ORD-74101 · Resolved by: Tariq B.        │  │
│  │ Last update: 2 days ago · 4 timeline events                   │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  Filter results:  [Status ▾]  [Case Type ▾]  [Agent ▾]  [Date ▾]  │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- Global search: matches order ID, customer name, email, case ID, case type
- Instant results as user types (debounced 300ms)
- Each result card: clickable, opens full case view
- Filter row: persists below results, doesn't collapse

---

## 9. Channel Integration Settings

```
┌──────────────────────────────────────────────────────────────────────┐
│  Settings — Channel Integrations                       [← Back]     │
│                                                                      │
│  Connect your support channels so CaseFlow can pull                  │
│  communications into unified case timelines.                        │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│                                                                      │
│  💬 Zendesk                                  ✅ Connected           │
│  Last sync: 2 minutes ago                    [Configure] [Disconnect]│
│  Pulling: tickets, agent notes, customer messages                   │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  🔧 Slack                                    ✅ Connected           │
│  Workspace: company-support.slack.com        [Configure] [Disconnect]│
│  Channels: #returns-team, #escalations, #warehouse-ops              │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  📱 WhatsApp Business (Twilio)               ✅ Connected           │
│  Number: +44 7700 900 XXX                    [Configure] [Disconnect]│
│  Pulling: messages, media attachments                               │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  🎯 Jira                                     ✅ Connected           │
│  Project: SUPPORT · WH · RETURNS             [Configure] [Disconnect]│
│  Pulling: ticket status, assignee, comments                         │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  📧 Email (Gmail / Outlook)                  ⚠ Not connected        │
│  Connect your support inbox to pull email threads into timelines.   │
│                                        [+ Connect Email]            │
│                                                                      │
│  ─────────────────────────────────────────────────────────────────  │
│  📞 Phone / Transcripts                      ⚠ Not connected        │
│  Upload call transcripts manually or connect a telephony API.       │
│                                 [+ Connect Telephony] [Upload file] │
│                                                                      │
└──────────────────────────────────────────────────────────────────────┘
```

**Annotations:**
- Admin-only screen
- Status: ✅ Connected (green), ⚠ Not connected (amber), ❌ Error (red)
- Each connected integration shows last sync timestamp
- "Configure" → modal for channel-specific settings (e.g., which Slack channels to monitor)
- Integration errors surface in the admin notification panel, not on every agent's screen

---

## 10. Mobile Compact View (Responsive)

```
┌──────────────────────────────┐
│  [CF]          🔍    🔔  [SA]│
├──────────────────────────────┤
│                              │
│  Case #4421                  │
│  Damaged Item  ● Open  2h ⚠  │
│  Ayesha Khan                 │
│  ⚠ Missing: Warehouse conf.  │
│                              │
│  ────────── TIMELINE ──────── │
│                              │
│  💬 Chat · Mon 10:14         │
│  Customer: "screen cracked"  │
│                              │
│  📱 WA · Mon 10:47           │
│  3 photos  [🖼][🖼][🖼]       │
│                              │
│  🔧 Slack · Mon 11:02        │
│  Sana → #returns: escalated  │
│                              │
│  🎯 Jira · Mon 11:05         │
│  WH-4421 · In Progress       │
│                              │
│  📧 Email · Tue 9:12         │
│  "Any update? Urgent."       │
│                              │
│  ──────────────────────────  │
│                              │
│  [📋 Summary]  [🤖 Ask AI]   │
│                              │
└──────────────────────────────┘
```

**Annotations:**
- Responsive layout: single-column stack on screens < 768px
- Timeline events: compact format — icon, channel, time, one-line summary
- Primary actions (Summary, AI Chat) remain accessible as bottom action buttons
- Full event detail accessible via tap → slide-up panel
