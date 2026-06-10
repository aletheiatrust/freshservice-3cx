---
layout: default
title: "Prioritised Plan"
parent: "Implementation Guides"
nav_order: 2
---


# Prioritised Implementation Plan
**Aletheia Academies Trust — Freshservice & 3CX**
**Date:** 10 June 2026
**Status:** DRAFT — Awaiting Approval

---

## Guiding Principle

Deliver safety first, then structure, then experience. Nothing that requires approval is touched until sign-off is received on each phase.

---

## Phase 0 — Immediate (No approval needed, zero risk)
**Estimated time: 2 hours**

These are typo fixes and data corrections. No workflow or portal changes.

| # | Action | Owner |
|---|---|---|
| 0.1 | Fix KB category typo: "eSafety, Polices & Security" → "eSafety, Policies & Security" | IT admin |
| 0.2 | Complete Gravesend department record (type, head, domains) | IT admin |
| 0.3 | Complete Rainham Mark Grammar record (head, domains) | IT admin |
| 0.4 | Complete Whitehill record (head, domains) | IT admin |
| 0.5 | Complete Saint Georges - Primary record (domains) | IT admin |
| 0.6 | Complete Knole Academy record (head, domains) | IT admin |
| 0.7 | Correct "Plan" ID card type on Sedleys to correct value | IT admin |

---

## Phase 1 — CRITICAL: Staff Leaver Workflow
**Estimated time: 1 day**
**Requires approval:** Yes — workflow design (report 02)

This addresses an active safeguarding and GDPR risk. Highest priority of the entire project.

| # | Action | Detail |
|---|---|---|
| 1.1 | Create "Staff Leaver" service request form | Fields per workflow-leavers.md |
| 1.2 | Create "Staff Transfer (Internal)" service request form | Lighter form for Aletheia-to-Aletheia moves |
| 1.3 | Configure child ticket automation — standard leaver | Auto-creates tickets for IT, People & Culture, Finance, Marketing |
| 1.4 | Configure child ticket automation — transfer path | IT-only child ticket |
| 1.5 | Add IT leaver checklist tasks | Includes: M365, Arbor, GovernorHub, CCTV, building access, device, ID card |
| 1.6 | Configure SLA: IT child ticket due end of last working day | Hard deadline |
| 1.7 | Configure auto-escalation: IT ticket not resolved by 17:00 on last day → escalate to Luke Dobson | Auto-notification |
| 1.8 | Configure auto-close parent when all children resolved | + send confirmation to requester |
| 1.9 | Place "Staff Leaver" and "Staff Transfer" in quick-access tiles on portal | Visible to all staff |
| 1.10 | Test: Submit a test leaver request, confirm all child tickets generate correctly | Full end-to-end test |

---

## Phase 2 — Service Catalogue Restructure
**Estimated time: 1–2 days**
**Requires approval:** Yes — per Phase 2 changes

| # | Action | Detail |
|---|---|---|
| 2.1 | Consolidate 16 Google Classroom items → 1 item with school dropdown | Biggest single structural improvement |
| 2.2 | Create "Password Reset / Account Locked" service item in User Accounts | Most common IT request, currently has no catalogue entry |
| 2.3 | Create "New User Account" item in User Accounts | For new starters not covered by onboarding workflow |
| 2.4 | Create "Account Leaver" item in User Accounts | Backup for ad-hoc leavers not submitted via workflow |
| 2.5 | Create "New Microsoft Teams" item in Microsoft Teams | |
| 2.6 | Create "Add Member to Team" item in Microsoft Teams | |
| 2.7 | Create "New Distribution Group" item in Email Groups | |
| 2.8 | Create "Add/Remove Member from Group" item in Email Groups | |
| 2.9 | Add "Printing Credit Request" item to Printing Credit | |
| 2.10 | Rename "IT Services" to "Security & Access" | More descriptive |
| 2.11 | Move "Staff EV Charging Account Setup" to a more appropriate category | Possibly HR Management or new Facilities category |
| 2.12 | Rename "Copying Code" to "Photocopier PIN / Follow-Me Code" | |
| 2.13 | Audit "Google Drive Migration" — archive if project is complete | Confirm with user first |
| 2.14 | Review "Fusion" (catering) and "Pupil Progress" KB categories — archive if outdated | Confirm with user |

---

## Phase 3 — Knowledge Base Restructure
**Estimated time: 2–3 days (content work)**
**Requires approval:** Yes — category restructure

| # | Action |
|---|---|
| 3.1 | Resolve API permission issue to enable article-level audit (or conduct manual audit via portal) |
| 3.2 | Rename "Microsoft Office" → "Microsoft 365" |
| 3.3 | Add "Microsoft Teams" knowledge base category |
| 3.4 | Add "People & Culture (HR)" knowledge base category |
| 3.5 | Add "Finance" knowledge base category |
| 3.6 | Add "Marketing & Communications" knowledge base category |
| 3.7 | Review "Hardware" vs "Microsoft Surface" — merge or restructure |
| 3.8 | Review "Software" category — break into specific software names |
| 3.9 | Archive or update "Fusion" articles (catering system — check relevance) |
| 3.10 | Archive or update "Pupil Progress" articles (mostly unused system) |
| 3.11 | Seed HR, Finance, and Marketing categories with initial articles |
| 3.12 | Identify top 5 articles to feature on redesigned portal homepage |

---

## Phase 4 — Portal Redesign
**Estimated time: 1 day**
**Requires approval:** Yes — design spec (portal-design-spec.md)

| # | Action |
|---|---|
| 4.1 | Upload Aletheia logo to portal settings |
| 4.2 | Set primary colour to `#1e4379` in portal theme |
| 4.3 | Apply custom CSS: typography (Montserrat/Open Sans), card styles, button styles |
| 4.4 | Build homepage custom HTML: hero section with search bar |
| 4.5 | Build quick-access tiles section (6 tiles) |
| 4.6 | Build department cards section (4 cards) |
| 4.7 | Configure knowledge base homepage highlights (5 articles) |
| 4.8 | Test on mobile, tablet, desktop |
| 4.9 | Accessibility check — contrast, tab order, screen reader |

---

## Phase 5 — New Staff Onboarding Workflow
**Estimated time: 1 day**
**Requires approval:** Yes

| # | Action |
|---|---|
| 5.1 | Create "New Staff Member" service request form |
| 5.2 | Configure child tickets: People & Culture, IT, Finance, Marketing |
| 5.3 | Set dependency logic: Finance child pauses until HR confirms contract signed |
| 5.4 | Set minimum lead time: 5 working days before start date |
| 5.5 | Test end-to-end |

---

## Phase 6 — 3CX Live Chat Integration
**Estimated time: 4–6 hours**
**Requires approval:** Yes + 3CX admin access

| # | Action |
|---|---|
| 6.1 | Enable 3CX live chat and confirm licence/feature availability |
| 6.2 | Configure IT support queue in 3CX for web chat |
| 6.3 | Set business hours: 08:00–17:00 Mon–Fri (term time) |
| 6.4 | Configure offline behaviour: "Leave a message" → Freshservice ticket |
| 6.5 | Embed 3CX chat widget on Freshservice portal (JS snippet in custom HTML) |
| 6.6 | Attempt 3CX CRM connector → Freshservice (native integration) |
| 6.7 | If native fails: configure Power Automate flow for chat → ticket creation |
| 6.8 | Test: initiate chat, confirm ticket created, confirm transcript attached |

---

## Phase 7 — SharePoint Integration
**Estimated time: 1 day**
**Requires approval:** Yes + SharePoint admin access

| # | Action |
|---|---|
| 7.1 | Identify trust hub SharePoint URL and key pages |
| 7.2 | Phase 7a: Embed Freshservice portal on trust hub intranet page (iFrame, 30 min) |
| 7.3 | Phase 7b: Add 3CX chat widget to trust hub SharePoint pages |
| 7.4 | Phase 7c: Install and configure Freshservice native SharePoint connector (replaces iFrame) |
| 7.5 | Add IT Support page to each school SharePoint site (embed or link) |
| 7.6 | Test authenticated flow: log into SharePoint → click support → verify no second login needed |

---

## Phase 8 — People & Culture, Finance, Marketing Catalogue Build
**Estimated time: 2–3 days**
**Requires approval:** Yes + input from each department head

| # | Action |
|---|---|
| 8.1 | Workshop with People & Culture team: identify top 5–8 request types for catalogue |
| 8.2 | Build People & Culture service catalogue (e.g. Contract query, Reference request, Absence query) |
| 8.3 | Workshop with Finance team: identify top request types |
| 8.4 | Build Finance service catalogue (e.g. Purchase approval, Budget query, Expense claim) |
| 8.5 | Workshop with Marketing team: identify request types |
| 8.6 | Build Marketing service catalogue (e.g. Design request, Press enquiry, Social media, Newsletter) |
| 8.7 | Configure routing rules for each workspace |
| 8.8 | Set SLA policies for each workspace |

---

## Summary Timeline

| Week | Focus |
|---|---|
| Week 1 | Phase 0 (data fixes) + Phase 1 (leaver workflow) |
| Week 2 | Phase 2 (catalogue restructure) + Phase 3 (KB restructure) |
| Week 3 | Phase 4 (portal redesign) + Phase 5 (onboarding workflow) |
| Week 4 | Phase 6 (3CX) + Phase 7 (SharePoint) |
| Week 5+ | Phase 8 (dept catalogues — requires dept input sessions) |

---

## Approvals Required

| Phase | What you're approving |
|---|---|
| Phase 1 | Leaver and transfer workflow design (fields, child tickets, escalation rules) |
| Phase 2 | Catalogue item list, category renames, items to archive |
| Phase 3 | KB category structure, articles to archive |
| Phase 4 | Portal design (colours, layout, tiles, copy) |
| Phase 5 | Onboarding workflow design |
| Phase 6 | 3CX live chat scope (hours, routing, ticket creation method) |
| Phase 7 | SharePoint pages to embed on, integration approach |
| Phase 8 | Per-department service catalogue (dept heads to sign off their own) |
