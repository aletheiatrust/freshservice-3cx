---
layout: default
title: "Department & Workflow Assessment"
parent: "Reports & Audits"
nav_order: 2
---


# Department Usage & Cross-Department Workflow Assessment
**Aletheia Academies Trust — Freshservice**
**Date:** 10 June 2026
**Status:** DRAFT — Awaiting Approval Before Any Changes

---

## 1. Four-Workspace Overview

Freshservice has four active workspaces. Only IT Support has any service catalogue structure. The other three receive tickets exclusively via email with no categorisation, routing, SLAs, or self-service.

| Workspace | ID | Template | Catalogue | Primary ticket source | Est. volume |
|---|---|---|---|---|---|
| IT Support | WS2 | IT template | 8 categories, 25 items | Mixed portal + email | High |
| People & Culture | WS9 | All-purpose | **EMPTY** | Email only | Medium |
| Finance | WS10 | Blank | **EMPTY** | Email only | Medium |
| Marketing & Communications | WS11 | Blank | **EMPTY** | Email only (+ external) | Low (very new) |

### Key Observations by Workspace

**People & Culture (HR)**
Active since November 2025. Handling complex multi-party cases (e.g. Safer Recruitment) via email threads with multiple CC'd stakeholders. No structured workflows. Cases like safer recruitment require coordination between HR, school heads, and central admin — currently managed entirely through email replies.

**Finance**
Active since January 2026. Receiving ad-hoc financial queries from schools (e.g. "Eye test money") via email. No categorisation, no approval workflows, no SLA tracking.

**Marketing & Communications**
Active less than one week. Currently receiving a mix of internal requests and external marketing emails. The team (led by Hannah) manually reviews all incoming mail. No catalogue, no structure yet. This workspace is a blank canvas.

---

## 2. Cross-Department Process Audit

### 2.1 New Staff Onboarding

**Current state:** The hiring school triggers the process. There is no standardised form, template, or workflow. Each school handles it differently. IT, HR, Finance and Media are notified separately (or not at all) via ad-hoc emails.

**What should happen across departments:**

| Department | Actions required | Current reality |
|---|---|---|
| Hiring school | Notify trust of new appointment, provide details | Email — inconsistent detail |
| People & Culture | Issue contract, DBS check, safer recruitment, references | Manual, email-based |
| IT | Create AD account, email, set up device, issue ID card | Notified late or inconsistently |
| Finance | Set up on payroll, assign cost centre | Separate communication |
| Marketing & Comms | Add to trust communications, intranet profile | Often forgotten entirely |

**Risk rating: MEDIUM** — New staff are sometimes onboarded without all systems being ready on day one. IT and Finance may receive duplicate or conflicting information from different school contacts.

### 2.2 Staff Leavers

**Current state:** IT finds out late or by accident. There is no standardised notification process from HR or schools. No existing forms or templates.

**What this means in practice:**
- Staff email accounts remain active after departure
- AD accounts are not disabled on the last day of employment
- Devices may not be collected
- Payroll may continue beyond the last working day
- Access to school systems (MIS, CCTV, finance software) is not revoked

**Risk rating: HIGH — Safeguarding and GDPR concern**

In a school trust context, a former staff member with active system access is a serious safeguarding risk. This should be the first cross-department workflow implemented.

**What should happen across departments:**

| Department | Actions required | Deadline |
|---|---|---|
| Hiring school / HR | Notify of leaving date and reason | As soon as confirmed |
| People & Culture | Process termination, issue P45, final pay info to Finance | Last working day |
| IT | Disable AD account, email, revoke all system access, arrange device collection, cancel ID card | **Last working day (end of day)** |
| Finance | Process final salary, stop standing orders, recover any outstanding equipment costs | On confirmation |
| Marketing & Comms | Remove from trust communications lists, update intranet | Within 1 week |

---

## 3. Proposed Workflow Design

### 3.1 Staff Leaver Workflow (PRIORITY 1)

**Trigger:** School business manager or headteacher submits a "Staff Leaver" service request on the portal.

**Proposed service request fields:**
- Staff member name
- School
- Job role / department
- Last working day (date picker)
- Reason for leaving (dropdown: Resignation / Retirement / End of contract / Other)
- Does the member of staff have a trust device? (Yes/No)
- Does the member of staff have an ID card? (Yes/No)
- Any other access concerns? (free text)

**What happens automatically on submission:**

```
Parent ticket (raised by school) — visible to all departments
│
├── Child ticket → IT Support
│   Tasks: Disable AD account, email, revoke MIS access,
│           revoke CCTV access, revoke finance system access,
│           collect device, cancel ID card
│   SLA: Complete by end of last working day
│
├── Child ticket → People & Culture
│   Tasks: Confirm final pay info, process P45,
│           update HR records, notify payroll
│   SLA: 2 working days before last day
│
├── Child ticket → Finance
│   Tasks: Process final salary, stop recurring payments,
│           log any equipment recovery costs
│   SLA: Last working day
│
└── Child ticket → Marketing & Comms
    Tasks: Remove from trust mailing lists,
            update intranet/website if applicable
    SLA: Within 5 working days of last day
```

**Escalation rule:** If IT child ticket is not completed by end of last working day, escalate automatically to IT manager (Luke Dobson).

---

### 3.2 New Staff Onboarding Workflow (PRIORITY 2)

**Trigger:** School business manager or headteacher submits a "New Staff Member" service request on the portal. Must be submitted **at least 5 working days before start date**.

**Proposed service request fields:**
- First name / Last name
- Personal email (for pre-joining communications)
- School
- Job role / department
- Employment type (Full-time / Part-time / Supply / Maternity cover)
- Contract type (Permanent / Fixed-term / Zero hours)
- Start date (date picker — must be ≥5 working days from today)
- Line manager
- Does the role require a trust device? (Yes/No)
- Does the role require an ID card? (Yes/No + card type: auto-populated from school's card type)
- DBS already on the Update Service? (Yes/No)
- Preferred username format (or auto-generate?)

**What happens automatically on submission:**

```
Parent ticket (raised by school)
│
├── Child ticket → People & Culture
│   Tasks: Issue contract, initiate DBS/safer recruitment checks,
│           collect references, set up on HR system
│   SLA: 3 working days of receiving request
│   Dependency: Finance child ticket paused until HR confirms contract signed
│
├── Child ticket → IT Support
│   Tasks: Create AD account, set up email, provision device (if needed),
│           arrange ID card, add to relevant Teams/Groups
│   SLA: Account ready for day 1. Device ready for day 1 if requested.
│   Dependency: Can begin as soon as request received for account setup
│
├── Child ticket → Finance
│   Tasks: Add to payroll, assign cost centre, set up expense access if applicable
│   SLA: Before first pay run after start date
│   Dependency: Waits for HR to confirm contract signed
│
└── Child ticket → Marketing & Comms
    Tasks: Add to trust comms lists, create intranet profile if applicable
    SLA: First working week of employment
    Dependency: None — can begin immediately
```

---

## 4. Brand Profile (In Progress)

### 4.1 Colours Identified from Aletheia Website

The following colours were extracted from the trust website (aletheiatrust.org.uk):

| Colour | Hex | Role (inferred) |
|---|---|---|
| Deep navy | `#1e4379` | Likely primary brand colour |
| Navy variant | `#194979` | Header/navigation |
| Dark navy | `#164698` | Link/accent |
| Crimson red | `#e22a20` | Accent / call-to-action |
| Red variant | `#be1823` | Secondary accent |
| Dark green | `#18562c` | Possibly school-specific |
| Forest green | `#31745b` | Possibly school-specific |
| Dark grey | `#333333` | Body text |
| White | `#ffffff` | Backgrounds |
| Light grey | `#f5f5f5` | Section backgrounds |

> **Action required:** Confirm primary brand colours (navy + crimson) and whether greens are trust-wide or school-specific.

### 4.2 Logo
Described as: teal/navy crown and cross triangle motif with "Aletheia Academies Trust" wordmark. Available at `/public/aletheia-logo.png` in trust systems.

### 4.3 Portal Theme Recommendations (Pending Approval)

For the Freshservice portal redesign, the proposed approach is:
- **Primary colour:** Deep navy (`#1e4379`) — header, navigation, primary buttons
- **Accent colour:** Crimson (`#e22a20`) — CTAs, highlights, active states
- **Background:** White with light grey (`#f5f5f5`) section breaks
- **Text:** Dark grey (`#333333`) for body, white on dark backgrounds
- **Font:** Pending — need to identify what font the website uses

---

## 5. Updated Risk Register

| Risk | Likelihood | Impact | Severity | Mitigation |
|---|---|---|---|---|
| Former staff accounts remain active post-departure | **High** | **Critical** | **CRITICAL** | Implement leaver workflow immediately |
| New staff not fully set up on day 1 | High | High | High | Implement onboarding workflow |
| Empty service catalogue categories damage self-service trust | High | Medium | High | Populate or remove immediately |
| KB article audit blocked | High | Medium | Medium | Request API scope change |
| Marketing workspace receiving spam | Low | Low | Low | Hannah reviewing manually — monitor |

---

## 6. Questions Still Outstanding

1. **What is the current leaver process for Finance?** Do schools notify Finance separately, or does payroll run until told otherwise?
2. **Who should be the escalation point if a leaver IT ticket is not completed by end of last working day?**
3. **Are there any cases where a leaver should NOT have accounts disabled immediately** (e.g. garden leave, handover period)?
4. **For the portal redesign** — can you share the exact Aletheia hex codes and font from any official brand document?
5. **Should the four workspaces appear as separate sections on the portal**, or should users see one unified portal with requests routed behind the scenes?

---

*No changes have been made to Freshservice. All designs require explicit approval before implementation.*
