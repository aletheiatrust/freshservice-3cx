---
layout: default
title: "SharePoint & 3CX Architecture"
parent: "Design & Architecture"
nav_order: 4
---


# Integration Architecture — SharePoint + 3CX + Freshservice
**Aletheia Academies Trust**
**Date:** 10 June 2026
**Status:** DRAFT — Awaiting Approval

---

## Overview

The goal is a **unified support experience** across three platforms:

```
┌─────────────────────────────────────────────────────────────────┐
│                    STAFF EXPERIENCE                             │
│                                                                 │
│  SharePoint Intranet              Freshservice Portal           │
│  (daily work hub)                 (support destination)         │
│       │                                  │                      │
│       │  ← Search surfaces KB articles   │                      │
│       │  ← Widget raises tickets inline  │                      │
│       │  ← 3CX chat available on page    │                      │
│       │                                  │                      │
│       └──────────────┬───────────────────┘                      │
│                      │                                          │
│              3CX Live Chat                                       │
│              (real-time IT support)                             │
│                      │                                          │
│              Creates Freshservice ticket                        │
│              automatically from chat                            │
└─────────────────────────────────────────────────────────────────┘
```

**Key enabler:** Microsoft 365 SSO is already active on Freshservice. Staff are already authenticated — no second login required for any of these integrations.

---

## Integration 1: SharePoint → Freshservice (Embedded Portal)

### Approach: iFrame Web Part + SSO Pass-Through

Since SSO is already configured via Microsoft 365, an authenticated SharePoint user is also an authenticated Freshservice user. The portal can be embedded in SharePoint pages without a second login.

### Option A — iFrame Embed (Simplest, Lowest effort)

Embed the Freshservice portal directly within a SharePoint page using the **Embed web part**.

```
SharePoint Page (Intranet)
├── Page header
├── News/announcements
├── [SUPPORT SECTION]
│   ├── Embed Web Part
│   │   └── src="https://support.aletheiatrust.org"
│   │       width: 100%, height: 600px
│   │       (Staff are already logged in via SSO)
└── Other intranet content
```

**Pros:** Zero development, works immediately, SSO handles auth.
**Cons:** iFrame feel — the portal sits in a box, doesn't feel native.
**Effort:** 30 minutes to configure.

### Option B — Freshservice SharePoint Connector (Recommended)

Freshservice has a native Microsoft Teams and SharePoint integration. Configure the Freshservice app/connector for SharePoint which surfaces:
- A "Raise a ticket" button inline on any SharePoint page
- Knowledge article search in a side panel
- Ticket status widget ("Your open tickets: 2")

This is native-feeling, not an iframe.

**Pros:** Native SharePoint experience, KB search inline, ticket widget.
**Cons:** Requires Freshservice marketplace app installation and SharePoint admin permissions.
**Effort:** 2–4 hours to configure and test.

### Option C — Custom SharePoint Web Part (Most integrated, most effort)

A custom SPFx (SharePoint Framework) web part that:
- Calls the Freshservice API directly
- Renders the most common service requests as buttons
- Surfaces the top 3 KB articles relevant to the current SharePoint page context
- Shows the user's open ticket count

**Pros:** Fully native, context-aware (e.g. on a school's SharePoint page, shows school-specific requests).
**Cons:** Requires developer time, ongoing maintenance.
**Effort:** 2–3 days development.

### Recommended Approach

**Phase 1:** Option A (iFrame) on the trust intranet hub — gets it live immediately.
**Phase 2:** Option B (native connector) to replace the iFrame once configured.
**Phase 3:** Option C on individual school sites for school-specific experience.

### Where to embed on SharePoint

**Trust hub intranet:**
- Main intranet homepage → "Support" tile linking to embedded portal
- A dedicated "IT Support" page with the full portal embedded
- Knowledge base search widget in the top navigation

**Individual school sites:**
- "Get Help" section on each school's SharePoint home
- Common requests relevant to that school surfaced as quick links
- Same 3CX chat widget embedded (see Integration 2)

---

## Integration 2: 3CX Live Chat → Freshservice

### 3CX Live Chat Widget

3CX self-hosted (v18/v20) includes a web chat widget that can be embedded on any website via a JavaScript snippet. The widget creates a chat queue in 3CX and routes to available IT agents.

**Widget embed snippet (goes in page `<head>` or `<body>`):**
```html
<!-- 3CX Live Chat Widget -->
<script>
window.__lc = window.__lc || {};
window.__lc.license = "YOUR_3CX_LIVECHAT_ID";
// Configuration options:
window.__lc.params = {
  name: 'Aletheia IT Support',
  department: 'IT',
  businessHours: true
};
</script>
<script src="https://[YOUR-3CX-SERVER]/livechat/chat.js" async></script>
```

This snippet is added to:
1. **Freshservice portal** — via Custom HTML/JavaScript in portal settings
2. **SharePoint pages** — via SharePoint Embed web part or SPFx script injection
3. (Optional) Individual school websites

### 3CX → Freshservice Ticket Creation

When a chat session ends (or at agent discretion), a Freshservice ticket should be created automatically from the conversation. Two methods:

**Method A: 3CX CRM Integration (Native) — CONFIRMED COMPATIBLE**
3CX v20 Update 8 (self-hosted, confirmed) has a built-in CRM connector that supports Freshservice. This allows:
- Agents to see requester's existing tickets during chat (caller lookup)
- Creating a new Freshservice ticket from within the 3CX interface
- Logging the chat transcript to the ticket

Configuration path: 3CX Management Console → CRM Integration → Freshservice → enter API key and domain.

**Method B: Power Automate Flow (Fallback)**
If the native CRM connector isn't available on the current 3CX version:
- 3CX sends a webhook/email when a chat ends
- Power Automate catches it and creates a Freshservice ticket via API
- Less seamless but achieves the same outcome

**Recommended:** Method A (native connector) — attempt first. Fall back to Power Automate if the self-hosted version doesn't support it.

### 3CX Chat Routing

| Scenario | Routing |
|---|---|
| Within IT business hours | Routes to available IT agent |
| Outside business hours | Shows "Leave a message" form → creates Freshservice ticket |
| All IT agents busy | Queue with estimated wait time displayed |
| Unanswered after 3 min | Auto-creates Freshservice ticket with transcript |

### Business Hours Configuration

IT support live chat: **08:00–17:00, Monday–Friday** (school term time).
Outside hours: offline message → ticket creation → next-day response SLA.

> **Action:** Confirm IT live chat hours. Should this extend to 08:00–16:00 in school holidays?

---

## Integration 3: Microsoft 365 / Teams

Since staff are already on Microsoft 365, the Freshservice Teams app provides additional touchpoints:

- **Freshservice bot in Teams** — Staff can raise tickets by messaging the bot
- **Ticket notifications in Teams** — Updates sent to staff as Teams messages (not just email)
- **IT agent notifications** — New tickets appear in a Teams channel for triage

This does not replace the portal but provides an additional channel for staff who spend their day in Teams.

**Configuration:** Freshservice Marketplace → Microsoft Teams app → authenticate with Microsoft 365 tenant.

---

## Full Integration Architecture Diagram

```
STAFF TOUCHPOINTS
─────────────────────────────────────────────────────────────
                    │                │               │
           SharePoint            Teams App        Direct Portal
           Intranet              (optional)    support.aletheiatrust.org
                    │                │               │
                    └────────────────┴───────────────┘
                                     │
                    ┌────────────────▼───────────────┐
                    │     FRESHSERVICE (4 workspaces) │
                    │  IT │ People & Culture │ Finance│
                    │       │ Marketing & Comms       │
                    └────────────────┬───────────────┘
                                     │
                    ┌────────────────▼───────────────┐
                    │     AUTOMATIONS & WORKFLOWS     │
                    │  • Leaver workflow (child tickets│
                    │  • Onboarding workflow          │
                    │  • Routing rules per workspace  │
                    │  • SLA policies                 │
                    └────────────────┬───────────────┘
                                     │
                    3CX LIVE CHAT ───┘
                    (self-hosted, embedded on portal
                     + SharePoint via JS widget)
                    Creates tickets from chat transcripts
```

---

## Authentication Flow (SSO Already Active)

```
Staff member → Opens SharePoint intranet
             → Already logged in (M365 SSO)
             → Clicks "IT Support" on intranet
             → Freshservice portal loads (iFrame or native)
             → Already authenticated (SSO pass-through)
             → No second login required ✓
```

---

## Implementation Sequence

| Phase | Work | Effort | Dependency |
|---|---|---|---|
| 1 | Embed Freshservice portal on SharePoint trust hub (iFrame) | 30 min | None |
| 2 | Add 3CX chat widget to Freshservice portal (JS snippet) | 1 hour | 3CX live chat configured |
| 3 | Add 3CX chat widget to SharePoint trust hub | 30 min | Phase 2 complete |
| 4 | Configure 3CX → Freshservice CRM integration (ticket creation) | 2–4 hours | 3CX admin access |
| 5 | Install Freshservice native SharePoint/Teams connector | 2–4 hours | SharePoint admin access |
| 6 | Add support widgets to individual school SharePoint sites | 1–2 days | Phases 1–3 complete |

---

## Information Needed to Proceed

To implement integrations 1–2:

| Item | Needed for |
|---|---|
| 3CX management console URL and admin access | Enabling live chat, configuring CRM connector |
| 3CX live chat licence / feature status | Confirming chat widget is available on current plan |
| 3CX version number | Determining CRM connector compatibility |
| SharePoint admin access (or SharePoint admin contact) | Embedding portal and chat widget |
| Trust hub SharePoint URL | Knowing where to embed |
| School SharePoint site URLs | Phase 6 rollout |

---

## What This Looks Like for a Staff Member

**Before (current experience):**
1. Staff has IT problem
2. Emails IT@aletheiatrust.org.uk from memory
3. Gets a ticket number by email
4. No visibility of progress unless they ask

**After (integrated experience):**
1. Staff opens SharePoint intranet (already open, they're on it all day)
2. Sees "IT Support" in the navigation or homepage
3. Either:
   - Clicks → searches KB → finds self-help article (deflects ticket entirely)
   - Clicks → raises service request from the embedded portal (30 seconds, structured)
   - Clicks 💬 Live Chat → real-time chat with IT agent (immediately resolved)
4. Ticket updates arrive in Teams (not buried in email)
5. All request history visible on portal (staff can check status without emailing IT)
