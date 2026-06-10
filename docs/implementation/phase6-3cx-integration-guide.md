---
layout: default
title: Phase 6 — 3CX Integration Guide
parent: Implementation
nav_order: 6
---

# Phase 6: 3CX Live Chat Integration — Build Guide
**Date:** 10 June 2026
**Status:** Ready for 3CX admin actioning

3CX Version 20 Update 8, self-hosted. Integration has two components:
1. **Live chat widget** — embedded on the Freshservice portal for staff to start a chat with IT
2. **CRM connector** — links 3CX calls/chats to Freshservice tickets automatically

---

## Part A — Configure the IT Support Live Chat Queue in 3CX

**Login to 3CX Management Console**

### Step 1: Create a Live Chat Queue

**Navigate to:** Call Queues → Add Queue

| Setting | Value |
|---|---|
| Name | IT Support Live Chat |
| Extension | Choose an available extension (e.g. 800) |
| Queue type | Ring All / Round Robin (your preference) |
| Ring timeout | 30 seconds |
| Agents | Add all IT support staff who will handle chats |

### Step 2: Set Business Hours

**Navigate to:** (Queue settings) → Hours of Operation

| Day | Hours |
|---|---|
| Monday–Friday | 08:00–16:30 |
| Saturday | Closed |
| Sunday | Closed |
| School holidays | Configure a separate holiday schedule if required |

**Out-of-hours message:**
```
IT Support is currently offline. Our support hours are Monday to Friday, 8:00am to 4:30pm.

To log a support request, please visit the IT support portal or email IT@aletheiatrust.org.uk
```

### Step 3: Enable Live Chat on the Queue

**Navigate to:** (Queue settings) → Live Chat

- Enable live chat: ✅ On
- Chat channel name: `IT Support`
- Welcome message: `Welcome to Aletheia IT Support. How can we help you today?`
- Offline message: (as above)

Save the queue.

---

## Part B — Get the Live Chat Widget Code

**Navigate to:** 3CX Management Console → Live Chat & Talk → Websites

### Step 1: Add your website

| Setting | Value |
|---|---|
| Website URL | https://support.aletheiatrust.org |
| Name | Aletheia IT Support Portal |

### Step 2: Configure widget appearance

| Setting | Value |
|---|---|
| Widget colour | `#1e4379` (navy — matches portal) |
| Widget position | Bottom right |
| Widget label | IT Support Chat |
| Online text | Chat with IT Support |
| Offline text | Leave a message |
| Show when offline | ✅ Yes (allow offline messages) |

### Step 3: Copy the widget script

3CX will generate a JavaScript snippet similar to:

```html
<script src="https://[your-3cx-domain]/livechat/livechat.js"
  id="tcx-callus-js"
  charset="utf-8"
  data-domain="[your-3cx-domain]"
  data-queue="IT Support Live Chat">
</script>
```

Copy this full snippet — it is needed for Part C.

---

## Part C — Add the Widget to the Freshservice Portal

**Navigate to:** Admin → Portals → Support Portal → Customize Portal → Homepage

Find the live chat placeholder block added in Phase 4 (Part C, Block 3) and replace it with the actual 3CX script copied in Part B:

```html
<!-- 3CX Live Chat Widget — IT Support -->
<!-- Hours: Monday–Friday 08:00–16:30 -->
<script src="https://[your-3cx-domain]/livechat/livechat.js"
  id="tcx-callus-js"
  charset="utf-8"
  data-domain="[your-3cx-domain]"
  data-queue="IT Support Live Chat">
</script>
```

The widget will appear as a floating button in the bottom-right corner of every portal page. The CSS added in Phase 4 already styles it to match the navy brand colour.

---

## Part D — Configure the Freshservice CRM Connector in 3CX

This creates a Freshservice ticket (or links to an existing one) automatically when a call or chat starts in 3CX.

**Navigate to:** 3CX Management Console → CRM Integration → Add Integration

### Step 1: Select Freshservice

Choose **Freshservice** from the CRM connector list.

### Step 2: Enter credentials

| Setting | Value |
|---|---|
| Freshservice domain | aletheiaacademiestrust.freshservice.com |
| API key | (use the same key from .env — or create a dedicated integration key in Freshservice admin) |
| Workspace | IT Support (Workspace 2) |

### Step 3: Configure trigger behaviour

| Setting | Value |
|---|---|
| On incoming call | Look up caller by email/phone → open existing ticket or create new one |
| On chat start | Create a new Freshservice ticket from the chat transcript |
| Ticket type | Incident |
| Default group | INC - 1st Line (or appropriate first-line group) |
| Include chat transcript | ✅ Yes |
| Include call recording link | ✅ Yes (if call recording is enabled) |

### Step 4: Map fields

| 3CX field | Freshservice field |
|---|---|
| Caller name | Requester name |
| Caller email | Requester email |
| Call/chat duration | Note in ticket |
| Agent name | Assigned agent |
| Queue name | Ticket tag: `live-chat` or `phone-call` |

Save the integration.

---

## Part E — Test the Integration

1. **Widget test:** Open the Freshservice portal → confirm the chat button appears bottom-right
2. **Online/offline test:** Check the button shows "Online" between 08:00–16:30 and "Offline" outside those hours
3. **Chat-to-ticket test:**
   - Start a chat via the portal widget
   - An IT agent accepts the chat in 3CX
   - Verify a Freshservice ticket is created automatically with the chat transcript
4. **Phone-to-ticket test:**
   - Make a test call to the IT support extension
   - Verify the caller lookup works and a ticket is created or surfaced

---

## Part F — Staff Communication

Once live, inform staff via:
- Email from headteachers / IT@aletheiatrust.org.uk
- Message on the portal homepage (update the hero text temporarily)
- Note in the next newsletter / staff bulletin

Suggested announcement:
> "IT Support now has live chat available on the support portal. Click the chat button on the bottom right of any page during school hours (8:00am–4:30pm, Monday–Friday) to speak with IT immediately. Outside these hours you can still leave a message and we will respond the next working day."

---

## Summary

| Part | Action | Status |
|---|---|---|
| A — 3CX queue | Create IT Support Live Chat queue, set hours 08:00–16:30 | ⏳ 3CX admin |
| B — Widget code | Configure widget appearance, copy JS snippet | ⏳ 3CX admin |
| C — Portal widget | Paste JS snippet into portal custom HTML | ⏳ Portal |
| D — CRM connector | Configure Freshservice integration in 3CX | ⏳ 3CX admin |
| E — Test | Widget, online/offline, chat-to-ticket, phone-to-ticket | ⏳ Test |
| F — Announce | Staff communication | ⏳ After go-live |
