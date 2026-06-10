---
layout: default
title: "Initial Assessment"
parent: "Reports & Audits"
nav_order: 1
---


# Freshservice Platform Assessment Report
**Aletheia Academies Trust**
**Date:** 10 June 2026
**Prepared by:** AI Consultant (via API audit + manual review)
**Status:** DRAFT — Awaiting Approval Before Any Changes

---

## Executive Summary

The Freshservice instance has a solid structural foundation but shows signs of organic growth without a guiding information architecture strategy. The most significant issues are: 16 duplicate service items that should be one consolidated item; 4 empty service categories; a knowledge base that is entirely IT-focused with no provision for Finance, HR or Media & Communications; and department records for newer schools that are incomplete.

The portal theme has been flagged separately by the service owner for review.

**Urgency rating of key workstreams:**

| Workstream | Priority | Effort |
|---|---|---|
| Service catalogue consolidation (Google Classrooms) | High | Low |
| Empty service category cleanup | High | Low |
| Knowledge base restructure | High | Medium |
| Incomplete department records | Medium | Low |
| Portal theme & UX redesign | Medium | High |
| Finance / HR / Media onboarding to Freshservice | Medium | High |
| SharePoint integration | Low | High |
| 3CX Live Chat integration | Low | High |

---

## 1. Department Audit

### 1.1 Schools Registered (20 departments)

| School | Type | Head | Domains Configured | ID Card Type |
|---|---|---|---|---|
| Aletheia (Trust) | Trust | Luke Dobson | aletheiatrust.org.uk, aaat.uk, decustrust.com | — |
| Alkerden | All Through | Laura Carey | alkerdenacademy.co.uk | — |
| Cliffe Woods | Primary | Karen Connolly | cliffewoods.medway.sch.uk | Paxton |
| Ditton | Primary | Graham Ward | ditton-jun.kent.sch.uk | Plain - Blank |
| Gravesend | — | **None** | **None** | — |
| Gravesend Grammar | Secondary | Malcolm Moaby | gravesendgrammar.com | — |
| Halling | Primary | Lisa Taylor | halling.medway.sch.uk | Paxton |
| Holy Trinity Gravesend | Primary | Aaron Jones | holytrinity-gravesend.kent.sch.uk | MiFare |
| Horton Kirby | Primary | Glenn Pollard | hortonkirby.kent.sch.uk | Paxton |
| Knole Academy | Secondary | **None** | **None** | Plain - Blank |
| Rainham Mark Grammar | Secondary | **None** | **None** | — |
| Rosherville | Primary | Justine Roddan | rosherville.kent.sch.uk | Plain - Blank |
| Saint Georges | All Through | Simon Murphy | saintgeorgescofe.kent.sch.uk | Salto |
| Saint Georges - Primary | Primary | Helen Taylor | **None** | — |
| Sedleys | Primary | Tina Handley | sedleys.kent.sch.uk | Plan |
| Shorne | Primary | Tara Hewett | shorne.kent.sch.uk | Paxton |
| St Botolphs | Primary | Amy Chitty | st-botolphs.kent.sch.uk | Plain - Blank |
| Stone St Marys | Primary | Jane Rolfe | stone.kent.sch.uk | Plain - Blank |
| Sutton-At-Hone | Primary | Karen Trowell | sutton-at-hone.kent.sch.uk | **Missing** |
| Whitehill | Primary | **None** | **None** | — |

### 1.2 Findings

**F-D1 — Five departments have incomplete records**
Gravesend, Rainham Mark Grammar (added June 2026), Whitehill, Saint Georges - Primary, and Knole Academy are missing one or more of: head user, email domains, school type. Freshservice uses domains for automatic requester assignment — missing domains means users from those schools cannot be auto-assigned to the correct department.

**F-D2 — Saint Georges has two department records**
"Saint Georges" and "Saint Georges - Primary" exist as separate departments. It is unclear if this is intentional (different teams at an all-through school) or a data quality issue.

**F-D3 — Gravesend department has no details at all**
Created April 2026 with zero configuration. This is likely a new school joining the trust.

**F-D4 — Rainham Mark Grammar School just added (1 June 2026)**
Brand new. No configuration. Will need full onboarding.

**F-D5 — ID Card types are inconsistent across schools**
Schools use Paxton, MiFare, Salto, Plain - Blank, and "Plan" (possibly a typo). This is correct if schools genuinely use different systems, but "Plan" on Sedleys looks like a data entry error.

### 1.3 Recommendations

| Ref | Action | Priority |
|---|---|---|
| R-D1 | Complete department records for all 5 incomplete departments | High |
| R-D2 | Clarify and resolve the Saint Georges dual-department situation | Medium |
| R-D3 | Correct "Plan" ID card type on Sedleys to correct value | Low |
| R-D4 | Create onboarding checklist for new schools (Rainham Mark, Gravesend) | Medium |

---

## 2. Service Catalogue Audit

### 2.1 Categories (8 total)

| # | Category | Description | Items | Assessment |
|---|---|---|---|---|
| 1 | ID Cards | Cards, lanyards, holders, offsite passes | 2 | OK |
| 2 | Printing Credit | Request additional print credit | **0** | EMPTY — needs items or deletion |
| 3 | User Accounts | Items relating to user accounts | **0** | EMPTY — critical gap |
| 4 | Microsoft Teams | Items relating to Microsoft Teams | **0** | EMPTY — critical gap |
| 5 | Email Groups | Email groups | **0** | EMPTY — critical gap |
| 6 | IT Services | Block/unblock email and websites | 6 | Mixed — needs review |
| 7 | Google / Teams Classes | Add users to classrooms | 16 | MAJOR ISSUE — see F-SC2 |
| 8 | HR Management | HR-related requests | 1 | Very thin |

### 2.2 Service Items (25 total)

| Item | Category | Visibility | Issue |
|---|---|---|---|
| Google Classroom × 16 schools | Google/Teams Classes | Staff | DUPLICATE — should be 1 item |
| Staff ID Card | ID Cards | Staff | OK |
| Student ID Card | ID Cards | Staff | OK |
| Email Whitelisting | IT Services | Staff | OK |
| CCTV Footage | IT Services | Staff | OK — 48h SLA set |
| Sign in App - Mobile App | IT Services | Staff | Possibly wrong category |
| Staff EV Charging Account Setup | IT Services | Staff | Wrong category |
| Copying Code | IT Services | Staff | Unclear — what is this? |
| Google Drive Migration | IT Services | Staff | Is this still live? |
| Employee Onboarding - MS Active Directory | HR Management | Staff | OK — but lone item |

### 2.3 Findings

**F-SC1 — 4 out of 8 categories have zero service items**
"Printing Credit", "User Accounts", "Microsoft Teams" and "Email Groups" all exist as categories but contain no requestable items. Users who land on the service catalogue see empty categories, which destroys confidence in self-service. Either populate these categories or remove them immediately.

**F-SC2 — 16 identical Google Classroom items (one per school)**
This is the biggest structural problem in the catalogue. Every school has its own service item for Google Classroom requests, all doing the same thing. The recommended fix is to consolidate into a single "Add to Google Classroom" item with a school dropdown field. Benefits:
- Catalogue drops from 25 items to 10
- Single item to maintain
- New schools added via a dropdown field change, not a new item

**F-SC3 — "IT Services" is a catch-all miscellaneous category**
It currently contains: EV charging, CCTV, email whitelisting, photocopier codes, Google Drive migration, and Sign In App setup. These span at least 3 logical categories. The category name is too generic.

**F-SC4 — Staff EV Charging is in IT Services**
This is a facilities/HR request, not an IT one. It is either in the wrong category or the wrong team is fulfilling it.

**F-SC5 — "Copying Code" is ambiguous**
The item name does not explain what it does. Is this requesting a photocopier PIN? A follow-me print code? An access code? The name will confuse users.

**F-SC6 — "Google Drive Migration" — status unclear**
Was this a project item left in the catalogue? If migration is complete, this item should be archived. If ongoing, it needs a better description.

**F-SC7 — HR Management has one item**
One onboarding item for a whole HR category is very thin. Is HR actively using Freshservice, or was this category created speculatively?

**F-SC8 — No items for core daily requests**
User Accounts is empty. The most common IT requests in any school (password resets, new user setup, account unlock) have no service catalogue entry. Users likely raise these as unstructured email/phone tickets.

### 2.4 Recommendations

| Ref | Action | Priority | Effort |
|---|---|---|---|
| R-SC1 | Consolidate 16 Google Classroom items into 1 with school dropdown | High | Low |
| R-SC2 | Populate "User Accounts" with: New User, Leaver, Password Reset, Account Unlock | High | Medium |
| R-SC3 | Populate "Microsoft Teams" with: New Team, Add Member, Guest Access | High | Medium |
| R-SC4 | Populate "Email Groups" with: New Group, Add/Remove Member | High | Low |
| R-SC5 | Populate "Printing Credit" with: Request Credit item | High | Low |
| R-SC6 | Rename "IT Services" to something specific (e.g. "Security & Access") and move misplaced items | Medium | Low |
| R-SC7 | Move EV Charging to HR/Facilities category | Medium | Low |
| R-SC8 | Rename "Copying Code" to "Photocopier PIN / Follow-Me Code" | Medium | Low |
| R-SC9 | Audit "Google Drive Migration" — archive if project is complete | Medium | Low |
| R-SC10 | Review HR Management with HR team — expand or remove the category | Medium | Medium |

---

## 3. Knowledge Base Audit

### 3.1 Categories (16 total)

| Category | Workspace | Notes |
|---|---|---|
| Default Category | WS1 | kbase@ email catch-all — standard FS default |
| Apple | WS2 | OK |
| Arbor | WS2 | MIS system — OK |
| eSafety, Polices & Security | WS2 | **TYPO: "Polices" → "Policies"** |
| Google | WS2 | OK |
| Fusion | WS2 | What system is this? |
| Microsoft Surface | WS2 | Hardware-specific category |
| Hardware | WS2 | General hardware — overlaps with Surface? |
| Interactive Boards | WS2 | OK |
| Microsoft Office | WS2 | OK |
| Phone System | WS2 | OK (3CX content likely here) |
| Photocopiers & Printers | WS2 | OK |
| Pupil Progress | WS2 | What system is this? |
| School Cloud | WS2 | Parent-teacher meeting platform — OK |
| Sign In App | WS2 | OK |
| Software | WS2 | Very generic — catch-all? |

> **Note:** Knowledge base article content could not be retrieved via API (403 — likely a permissions scope issue). Article count and individual article assessment requires admin portal review or API key scope adjustment.

### 3.2 Findings

**F-KB1 — Typo in category name: "eSafety, Polices & Security"**
"Polices" should be "Policies." This is visible to all users on the portal.

**F-KB2 — Knowledge base is 100% IT-focused**
There are no categories for Finance, HR, or Media & Communications. If the brief is to extend Freshservice to all 4 departments, the knowledge base needs restructuring to accommodate non-IT content.

**F-KB3 — "Fusion" — unknown system**
A knowledge base category exists for "Fusion" but it is not clear what system this refers to. Needs clarification to assess relevance.

**F-KB4 — "Pupil Progress" — unknown system**
Same issue. Is this a specific product name? If the system has changed, the category may be outdated.

**F-KB5 — "Microsoft Surface" and "Hardware" overlap**
Microsoft Surface is a hardware category. Having both a generic Hardware category and a Surface-specific one suggests inconsistent categorisation. Surface articles may be split across both.

**F-KB6 — "Software" is too broad**
A catch-all "Software" category will become a dumping ground. Articles about specific software should live in their own category (as the others do).

**F-KB7 — No category for Microsoft 365 as a whole**
There is "Microsoft Office" but Microsoft 365 now encompasses Teams, OneDrive, SharePoint, Outlook, Intune — all of which likely need articles. The category name is outdated.

**F-KB8 — No Teams category in the knowledge base**
The service catalogue has a Teams category. The knowledge base does not. There is no home for Teams how-to guides.

### 3.3 Recommendations

| Ref | Action | Priority |
|---|---|---|
| R-KB1 | Fix typo: rename "eSafety, Polices & Security" → "eSafety, Policies & Security" | High |
| R-KB2 | Clarify what "Fusion" refers to — update or archive | Medium |
| R-KB3 | Clarify what "Pupil Progress" refers to — update or archive | Medium |
| R-KB4 | Rename "Microsoft Office" → "Microsoft 365" | Medium |
| R-KB5 | Add "Microsoft Teams" category to knowledge base | Medium |
| R-KB6 | Merge "Microsoft Surface" into "Hardware" OR split Hardware into device types | Low |
| R-KB7 | Add categories for Finance, HR, and Media & Communications support | Medium |
| R-KB8 | Review "Software" category — likely needs breaking down | Low |
| R-KB9 | Request API scope adjustment to enable article-level audit | High |

---

## 4. Agent & Group Structure Audit

### 4.1 Groups (9 total)

| Group | Type | Members | Auto-assign | Notes |
|---|---|---|---|---|
| INC - 2nd Line | Incident | 2 | Yes | Escalation group — 1h SLA |
| INC - Alkerden Hub | Incident | 2 | Yes | 15m SLA |
| INC - Gravesend Grammar Hub | Incident | 2 | Yes | 15m SLA |
| INC - Knole Hub | Incident | 2 | Yes | 15m SLA |
| INC - Primary School Hub | Incident | 2 | Yes | 4h SLA — covers all primaries |
| INC - St George's Hub | Incident | 1 | Yes | 15m SLA — only 1 member |
| INV - Assets | Inventory | 0 | No | Observer-only, no members |
| PR - Problems | Problem | 2 | Yes | All agents observe |
| Z - Awaiting Assignment | Holding | 0 | No | Parking group |

### 4.2 Findings

**F-AG1 — INC - St George's Hub has only 1 member**
A hub with a single technician has no resilience. Absence or leave leaves the hub unstaffed.

**F-AG2 — Primary School Hub covers all primaries with only 2 members**
The Primary School Hub serves the largest number of schools with a 4-hour SLA (vs 15 minutes for secondary hubs). This suggests either a resource constraint or a deliberate tiered support model.

**F-AG3 — "Z - Awaiting Assignment" suggests a triage gap**
A named parking group for unassigned tickets indicates that tickets are sometimes raised without routing. This should be investigated — automated routing rules may be missing or failing.

**F-AG4 — No groups for Finance, HR or Media & Communications**
If these departments are to use Freshservice, agent groups will be needed for them.

### 4.3 Recommendations

| Ref | Action | Priority |
|---|---|---|
| R-AG1 | Add a second member to St George's Hub or merge with Primary Hub temporarily | High |
| R-AG2 | Review routing rules — identify why tickets land in "Z - Awaiting Assignment" | Medium |
| R-AG3 | Plan agent groups for Finance, HR, Media teams when they onboard | Medium |

---

## 5. Portal Theme & UX (Initial Assessment)

### 5.1 Status
The portal theme could not be assessed via API. A visual audit of https://support.aletheiatrust.org is required and is flagged for the next phase.

The service owner has specifically requested the theme be reviewed.

### 5.2 Preliminary Observations (based on structure)
- The portal URL uses the trust's custom domain — good.
- The workspace structure (WS1 = internal/agents, WS2 = user-facing) appears correctly separated.
- Self-service adoption is likely low given the empty categories and lack of structured user account request items.

### 5.3 Questions for Portal Design Phase
Before redesigning the portal theme and layout:
1. Does the portal currently use Aletheia branding (logo, colours)?
2. Are there brand guidelines (hex codes, fonts) to follow?
3. Should the portal serve all 4 departments from one interface, or should departments have separate portals/sections?
4. Is there a target for self-service deflection (% of tickets resolved without agent contact)?

---

## 6. Integration Opportunities (Initial Scoping)

### 6.1 SharePoint Online
No SharePoint integration currently exists. Opportunities include:
- Embedding the Freshservice portal widget within SharePoint intranet pages
- Surfacing knowledge base articles via SharePoint search
- Using SharePoint as the primary staff intranet with Freshservice as the support layer

### 6.2 3CX Live Chat
No 3CX integration currently exists. 3CX supports live chat widgets that can be embedded on web pages. Opportunities include:
- Embedding 3CX live chat on the Freshservice portal for real-time support
- Routing 3CX chats to create Freshservice tickets automatically
- Embedding 3CX on SharePoint intranet pages

### 6.3 Questions for Integration Phase
1. Which SharePoint sites exist and which teams manage them?
2. Is the SharePoint intranet currently used as the primary staff landing page?
3. What is the 3CX deployment — cloud-hosted or on-premises?
4. Should 3CX live chat be available 24/7 or only during school hours?

---

## 7. Risks

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Empty categories damage user confidence in self-service | High | High | Populate or remove immediately |
| Incomplete department domains prevent correct ticket routing | Medium | High | Complete records before advertising portal |
| KB article audit blocked by API permissions | High | Medium | Request scope change or audit manually |
| St George's Hub single technician — service gap on absence | Medium | High | Add second member or cover plan |
| Google Classroom items — new schools added as separate items again | High | Low | Consolidate now before more schools join |

---

## 8. Proposed Actions — Phased Plan

### Phase 1 — Quick Wins (1–2 days, no risk, reversible)
These require zero user impact and can be done immediately upon approval.

- [ ] Fix "eSafety, Polices & Security" typo
- [ ] Complete department records for 5 incomplete schools
- [ ] Remove or clearly label empty service catalogue categories
- [ ] Rename "Copying Code" to descriptive name
- [ ] Rename "Microsoft Office" KB category to "Microsoft 365"
- [ ] Archive "Google Drive Migration" if project is complete

### Phase 2 — Catalogue Restructure (3–5 days)
- [ ] Consolidate 16 Google Classroom items into 1 with school dropdown
- [ ] Populate User Accounts category (New User, Leaver, Password Reset, Account Unlock)
- [ ] Populate Microsoft Teams category
- [ ] Populate Email Groups category
- [ ] Add Printing Credit request item
- [ ] Restructure "IT Services" into a better-named category

### Phase 3 — Knowledge Base Audit (1 week)
- [ ] Resolve API permissions to enable article-level audit
- [ ] Audit all articles for accuracy, duplication, and relevance
- [ ] Create category structure for Finance, HR, Media & Communications
- [ ] Add Microsoft Teams knowledge base category

### Phase 4 — Portal Redesign
- [ ] Visual audit of current portal
- [ ] Design proposal with Aletheia branding
- [ ] Review portal structure (single vs department-separated)
- [ ] Implement approved design

### Phase 5 — Department Onboarding (Finance, HR, Media)
- [ ] Stakeholder conversations with each department
- [ ] Define service catalogue items per department
- [ ] Create agent groups
- [ ] Knowledge base seeding

### Phase 6 — Integrations (SharePoint + 3CX)
- [ ] SharePoint architecture design
- [ ] 3CX integration design
- [ ] Pilot rollout
- [ ] Full deployment

---

## 9. Outstanding Questions for Service Owner

These need answers before Phase 1 can begin:

1. **Saint Georges dual department** — is "Saint Georges" (All Through) and "Saint Georges - Primary" intentional or a data error?
2. **Fusion system** — what is this? Is it still in use?
3. **Pupil Progress system** — same question.
4. **Finance, HR, Media** — are these departments currently raising tickets via Freshservice at all, or is onboarding them a new initiative?
5. **"Google Drive Migration"** — is this item still live?
6. **"Copying Code"** — what does this item do?
7. **Portal theme** — what are the current Aletheia brand colours and fonts?
8. **3CX deployment** — cloud or on-prem? What version?
9. **SharePoint** — which team manages it and which sites exist?

---

*Report prepared from API audit data. No changes have been made to the Freshservice instance. All recommendations require explicit approval before implementation.*
