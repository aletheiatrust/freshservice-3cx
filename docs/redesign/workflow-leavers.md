---
layout: default
title: "Staff Leaver Workflow Design"
parent: "Design & Architecture"
nav_order: 3
---


# Staff Leaver Workflow — Design Specification
**Status:** DRAFT — Awaiting Approval
**Priority:** CRITICAL (safeguarding & GDPR risk)
**Date:** 10 June 2026

---

## Problem Statement

IT currently finds out about staff leavers **late or by accident**. The only semi-automated mechanism is Arbor contract expiry — but this only covers Arbor-linked accounts. The following account types fall through completely:

- **Governors** (no Arbor record)
- **Associate staff / volunteers** (may not be on Arbor)
- **Central trust staff** (not school-based)
- **Contractors and supply staff** on long-term placements
- **Roles shared across schools** (e.g. peripatetic music teachers)

In a school trust, an active account belonging to a former staff member is a **safeguarding and GDPR risk**. This is the highest priority workflow to implement.

---

## Exception: Internal Transfers

If a staff member is **moving to another Aletheia school**, accounts are **not disabled** — they are transferred/updated. The leaver workflow must capture this distinction at submission.

---

## Workflow Design

### Trigger
A school business manager or headteacher submits the **"Staff Leaver"** service request on the portal.

The form must be submitted **as soon as a leaving date is confirmed** — ideally at least 5 working days before the last day, to allow access revocation to be prepared.

---

### Service Request Form Fields

| Field | Type | Required | Notes |
|---|---|---|---|
| Staff member full name | Text | Yes | |
| School | Dropdown | Yes | Auto-populated from requester's department |
| Job role / title | Text | Yes | |
| Employment type | Dropdown | Yes | Teaching / Support / Governor / Contractor / Central trust |
| Last working day | Date picker | Yes | Cannot be in the past |
| Reason for leaving | Dropdown | Yes | Resignation / Retirement / End of contract / Dismissal / Transfer to another Aletheia school / Other |
| **Is this an internal transfer to another Aletheia school?** | Yes/No | Yes | If Yes → different child tickets triggered (see Transfer path below) |
| Does the member of staff have a trust-issued device? | Yes/No | Yes | |
| Does the member of staff have an ID card? | Yes/No | Yes | |
| Does the member of staff have a Paxton/MiFare/Salto/other access fob? | Yes/No | Yes | Building access |
| Is this person a Governor? | Yes/No | Yes | Flags non-Arbor account |
| Are there any other accounts or systems not covered by Arbor? | Text | No | Free text — e.g. named logins, CCTV admin, finance software |
| Additional notes | Text | No | |

---

### Standard Leaver Path (not a transfer)

On submission, the parent ticket is created and **four child tickets are automatically generated** and assigned to the relevant agent groups:

```
PARENT: Staff Leaver — [Name] — [School] — Last day: [Date]
(raised by school, visible to all involved departments)
│
├── CHILD 1 → IT Support (INC - relevant Hub group)
│   Priority: HIGH
│   SLA: ALL tasks completed by end of last working day
│   
│   Checklist:
│   □ Disable Microsoft 365 / Active Directory account
│   □ Revoke email access and set out-of-office / redirect
│   □ Remove from all Teams, SharePoint sites, and shared mailboxes
│   □ Disable MIS (Arbor) account if applicable
│   □ Revoke CCTV system access if applicable
│   □ Revoke finance system access if applicable
│   □ Revoke Sign In App access if applicable
│   □ Revoke any other named system access (see notes field)
│   □ Arrange device collection (if device issued)
│   □ Deactivate ID card (if card issued)
│   □ Deactivate building access fob (if issued)
│   □ Confirm all actions completed and record date/time
│   
│   ⚠ GOVERNOR FLAG: If "Is this person a Governor?" = Yes
│      → Raise a separate IT support ticket for GovernorHub account removal
│      → Do NOT delay or block the main leaver ticket — process in parallel
│   
│   Escalation: If ticket not resolved by 17:00 on last working day
│               → Auto-escalate to IT Manager (Luke Dobson)
│
├── CHILD 2 → People & Culture
│   Priority: MEDIUM
│   SLA: 2 working days before last working day
│   
│   Checklist:
│   □ Confirm termination date on HR system
│   □ Process P45
│   □ Send final pay information to Finance (via payroll portal)
│   □ Collect any HR documentation from leaver
│   □ Confirm reference policy with line manager
│   □ Update personnel record status to "Leaver"
│
├── CHILD 3 → Finance
│   Priority: MEDIUM
│   SLA: Last working day
│   
│   Checklist:
│   □ Confirm final salary payment date and amount
│   □ Stop any recurring expense allowances or travel claims
│   □ Process equipment cost recovery if device not returned (liaise with IT)
│   □ Update budget records
│
└── CHILD 4 → Marketing & Communications
    Priority: LOW
    SLA: Within 5 working days of last working day
    
    Checklist:
    □ Remove from trust-wide mailing lists and distribution groups
    □ Remove from staff directory / intranet profile if applicable
    □ Update any public-facing content that references this person
```

---

### Internal Transfer Path (Aletheia school to Aletheia school)

If "Is this an internal transfer?" = Yes:

```
PARENT: Staff Transfer — [Name] — [From School] → [To School] — Transfer date: [Date]
│
└── CHILD 1 → IT Support only
    
    Checklist:
    □ Update AD account — change department, school OU, and email if required
    □ Update Arbor record for new school
    □ Update Teams memberships — remove from old school groups, add to new
    □ Update SharePoint access — remove old school access, add new school access
    □ Update ID card if school-specific
    □ Update building access fob if required
    □ Notify new school IT contact that account is ready
    
    Note: Account is NOT disabled. No Finance or People & Culture child tickets
    required unless the transfer involves a contract change (a separate HR process).
```

---

## Automation Rules (to be configured in Freshservice)

| Trigger | Action |
|---|---|
| Leaver ticket submitted | Create 4 child tickets (or 1 for transfers), notify all assignees |
| Last working day - 3 days | Send reminder to IT if child ticket not yet In Progress |
| Last working day 17:00 | If IT child ticket status ≠ Resolved → escalate to Luke Dobson |
| All child tickets resolved | Auto-close parent ticket, send confirmation to requester |
| Child ticket overdue | Notify group leader + observer (Luke Dobson) |

---

## Reporting

A weekly leaver dashboard should show:
- Leavers processed this month (by school, by type)
- IT tickets completed on time vs overdue
- Accounts still active beyond last working day (critical metric)
- Transfers processed

---

## Risks Mitigated

| Risk | Before | After |
|---|---|---|
| Active accounts after departure | IT finds out late, accounts persist | All accounts disabled by end of last day, with auto-escalation |
| Governor accounts missed | Not on Arbor, no process | Explicit governor flag on form triggers manual check |
| Non-Arbor accounts missed | No visibility | Free text field for named systems, IT checklist covers all |
| Finance pays beyond last day | Separate unlinked process | Child ticket to Finance created automatically |
| Comms lists not updated | Forgotten entirely | Child ticket to Marketing ensures it happens |

---

## Questions Before Implementation

1. Should the leaver form be visible to **all school staff** on the portal, or restricted to headteachers and school business managers only?
2. Who at the school should receive the confirmation email when all child tickets are closed?
3. For the governor flag — is there a separate governor management system beyond email distribution lists?
4. Should leavers be able to submit their own offboarding requests, or is this always school-initiated?
