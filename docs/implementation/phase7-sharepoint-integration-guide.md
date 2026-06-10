---
layout: default
title: Phase 7 — SharePoint Integration Guide
parent: Implementation
nav_order: 7
---

# Phase 7: SharePoint Integration — Build Guide
**Date:** 10 June 2026
**Status:** Ready for actioning

SharePoint tenant: saintgeorgescofeschool647.sharepoint.com
Microsoft 365 SSO is already active on Freshservice — this is the key enabler.

The goal is to make the support portal and SharePoint feel connected rather than separate systems. Staff should be able to reach IT support from wherever they are working.

---

## Recommended Approach: Two-Way Embedding

Rather than a single direction link, connect both ways:

| Direction | Method | Benefit |
|---|---|---|
| SharePoint → Freshservice | Embed portal widget on SharePoint intranet | Staff can raise tickets without leaving SharePoint |
| Freshservice → SharePoint | Link to SharePoint from portal header/knowledge base | Staff can find shared documents from the support portal |

---

## Part A — Embed the Freshservice Support Widget on SharePoint

This adds a small "Get IT Support" panel to your SharePoint intranet homepage so staff can raise a ticket or search for help without navigating away.

### Option A1 — Embed Script Web Part (simplest)

SharePoint Online supports an **Embed** web part that accepts JavaScript or iFrame code.

**Navigate to:** SharePoint Admin → Your intranet homepage → Edit page → Add web part → Embed

Paste the following iFrame:

```html
<iframe
  src="https://support.aletheiatrust.org/support/home"
  width="100%"
  height="600"
  frameborder="0"
  style="border-radius:8px; border:1px solid #e0e0e0;"
  title="Aletheia IT Support Portal">
</iframe>
```

> **Note:** Freshservice may block iFrame embedding by default (X-Frame-Options header). If the portal does not load in the iFrame, use Option A2 instead.

### Option A2 — Freshservice Support Widget (recommended if iFrame is blocked)

Freshservice provides a lightweight support widget script that can be embedded on any web page including SharePoint.

**Navigate to:** Freshservice Admin → Portals → Support Portal → Widget

1. Enable the support widget
2. Configure:
   - Widget colour: `#1e4379`
   - Widget title: IT Support
   - Contact form: enabled
   - Knowledge base search: enabled
3. Copy the generated JavaScript snippet
4. In SharePoint: Edit page → Add web part → **Script Editor** (classic) or **Embed** (modern) → paste the script

The widget appears as a floating button or inline panel on the SharePoint page.

---

## Part B — Add SharePoint Links to the Freshservice Portal

Add a quick link to SharePoint from the Freshservice portal so staff can jump to shared documents and resources.

### Option B1 — Header link

**Navigate to:** Admin → Portals → Support Portal → Customize Portal → HTML/Header

Add a navigation link:

```html
<a href="https://saintgeorgescofeschool647.sharepoint.com"
   target="_blank"
   style="color:#ffffff; font-weight:600; margin-left:16px;">
  📁 SharePoint
</a>
```

Insert this into the portal header HTML alongside the existing navigation links.

### Option B2 — Knowledge base article links

In relevant knowledge base articles (e.g. IT policies, GDPR, staff guides), link directly to the relevant SharePoint document library rather than describing where to find a document manually.

Example article addition:
> "The full Acceptable Use Policy is available on SharePoint: [View Policy Document →](https://saintgeorgescofeschool647.sharepoint.com/...)"

This is ongoing work — update articles as part of the Phase 3 content audit.

---

## Part C — Microsoft 365 SSO Pass-Through

Because Freshservice already uses Microsoft 365 SSO, staff who are signed into SharePoint will be automatically signed into the Freshservice portal without a second login prompt. No additional configuration is needed for this — it works by default.

This means the SharePoint → Freshservice link feels seamless to end users.

---

## Part D — SharePoint IT Support Hub Page (Optional Enhancement)

Create a dedicated "IT Support" page on the SharePoint intranet that brings together:

- Embedded Freshservice support widget (Part A)
- Links to the most common service requests (password reset, new account, leaver)
- Links to top knowledge base articles
- IT contact details and support hours
- Link to the full support portal

This becomes the IT support landing page for staff who start their day in SharePoint.

**Navigate to:** SharePoint → Create new page → Use "Blank" template

Suggested page structure:

```
[Aletheia IT Support]

How can we help?
[Search box — Freshservice widget]

Common Requests
[ Password Reset ]  [ New Account ]  [ Report a Problem ]

Support Hours: Monday–Friday 8:00am–4:30pm
Live Chat available on the support portal during these hours

📞 IT@aletheiatrust.org.uk
🌐 support.aletheiatrust.org
```

---

## Part E — Considerations and Limitations

| Item | Note |
|---|---|
| iFrame blocking | Freshservice may set X-Frame-Options: SAMEORIGIN, preventing iFrame embedding. Test first — if blocked, use the widget script (Option A2). |
| SSO scope | SSO works for staff with Microsoft 365 accounts. Supply staff or contractors without trust accounts will still need to log in manually. |
| SharePoint permissions | The SharePoint IT Support Hub page should be accessible to all staff (not restricted to specific groups). |
| Mobile | SharePoint mobile app may not render embedded iFrames. The widget script approach works better on mobile. |

---

## Summary

| Part | Action | Status |
|---|---|---|
| A — Freshservice on SharePoint | Embed widget or iFrame on intranet homepage | ⏳ SharePoint admin |
| B — SharePoint on Freshservice | Header link + KB article links | ⏳ Portal |
| C — SSO | Already working — no action needed | ✅ Done |
| D — IT Support Hub page | Optional SharePoint page | ⏳ Optional |
| E — Test | Verify SSO pass-through, widget loads, links work | ⏳ Test |
