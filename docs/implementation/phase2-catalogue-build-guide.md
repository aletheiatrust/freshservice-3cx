---
layout: default
title: Phase 2 — Catalogue Build Guide
parent: Implementation
nav_order: 2
---

# Phase 2: Service Catalogue Restructure — Build Guide
**Date:** 10 June 2026
**Status:** DRAFT — 4 items pending confirmation (see end of document)

This guide covers all portal changes for Phase 2. Work through each part in order.
Some items require confirmation before actioning — they are marked ⚠️ and listed at the end.

---

## Current Catalogue State (confirmed via API)

| Category | ID | Items |
|---|---|---|
| ID Cards | 53000043588 | Staff ID Card, Student ID Card |
| Printing Credit | 53000047373 | *empty* |
| User Accounts | 53000047503 | *empty* |
| Microsoft Teams | 53000051008 | *empty* |
| Email Groups | 53000051132 | *empty* |
| IT Services | 53000052826 | Email Whitelisting, CCTV Footage, Sign in App, Staff EV Charging, Copying Code, Google Drive Migration |
| Google / Teams Classes | 53000052924 | 17 per-school Google Classroom items |
| HR Management | 53000053289 | Employee Onboarding - MS Active Directory |
| Staff Changes | 53000054716 | *empty — Phase 1 portal build pending* |

---

## Part A — Rename Categories

**Navigate to:** Admin → Service Catalog → (click category name to edit)

### A1 — Rename "IT Services" → "Security & Access"

The current name "IT Services" is too generic — every category is an IT service. "Security & Access" describes what's actually in this category (CCTV, email whitelisting, building access, Sign In App).

| Field | Value |
|---|---|
| Name | Security & Access |

Save.

### A2 — Rename "Google / Teams Classes" → "Classroom Setup"

Broader name to accommodate both Google Classroom and Microsoft Teams classes, and any future LMS requests.

| Field | Value |
|---|---|
| Name | Classroom Setup |

Save.

---

## Part B — Populate Empty Categories

### B1 — User Accounts: Add "Password Reset / Account Locked"

**Navigate to:** Admin → Service Catalog → User Accounts → + New Service Item

This is likely the highest-volume IT request with no current catalogue entry. Staff currently raise a generic incident.

| Field | Value |
|---|---|
| Name | Password Reset / Account Locked |
| Description | Use this form if you have forgotten your password, your account has been locked, or you cannot sign in to your school computer, Microsoft 365, or other Trust system. |
| Visibility | All Users |
| Allow attachments | No |
| Icon | lock or key icon |

**Form fields:**

**Field 1 — Account type**
- Type: Dropdown
- Label: `Which account is affected?`
- Required: ✅ Yes
- Options:
  - School computer / Windows login
  - Microsoft 365 (email, Teams, OneDrive)
  - Arbor MIS
  - Google Workspace
  - Other

**Field 2 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes
- Options: (full school list — same as Staff Leaver form)

**Field 3 — Additional details**
- Type: Paragraph Text
- Label: `Any additional details?`
- Required: ❌ No
- Placeholder: `e.g. error message you are seeing, when the problem started`

**Subject template:**
```
Password Reset: {{requested_for}} — {{custom_field.cf_which_account_is_affected}} — {{custom_field.cf_school}}
```

Save.

---

### B2 — User Accounts: Add "New User Account Request"

For ad-hoc new account requests outside the formal onboarding workflow (supply teachers, temporary contractors, late starters).

| Field | Value |
|---|---|
| Name | New User Account Request |
| Description | Use this form to request a new IT account for a member of staff who is joining or has recently joined. For new permanent staff, submit at least 5 working days before their start date. |
| Visibility | All Users |
| Allow attachments | No |
| Icon | person-plus icon |

**Form fields:**

**Field 1 — Full name**
- Type: Single Line Text
- Label: `Staff member full name`
- Required: ✅ Yes

**Field 2 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes
- Options: (full school list)

**Field 3 — Job role**
- Type: Single Line Text
- Label: `Job role / title`
- Required: ✅ Yes

**Field 4 — Employment type**
- Type: Dropdown
- Label: `Employment type`
- Required: ✅ Yes
- Options: Permanent, Fixed term, Supply, Contractor, Governor, Other

**Field 5 — Start date**
- Type: Date
- Label: `Start date`
- Required: ✅ Yes

**Field 6 — Account types needed**
- Type: Checkbox (multi-select)
- Label: `Which accounts are needed?`
- Required: ✅ Yes
- Options:
  - Microsoft 365 (email + Teams + OneDrive)
  - Active Directory / school computer login
  - Arbor MIS
  - Google Workspace
  - Other (specify below)

**Field 7 — Additional notes**
- Type: Paragraph Text
- Label: `Anything else IT should know?`
- Required: ❌ No

**Subject template:**
```
New Account: {{custom_field.cf_staff_member_full_name}} — {{custom_field.cf_school}} — Start: {{custom_field.cf_start_date}}
```

Save.

---

### B3 — Microsoft Teams: Add "New Microsoft Teams Class or Team"

**Navigate to:** Admin → Service Catalog → Microsoft Teams → + New Service Item

| Field | Value |
|---|---|
| Name | New Microsoft Teams Class or Team |
| Description | Request a new Microsoft Teams class (for teaching) or Teams workspace (for a department, project, or working group). |
| Visibility | All Users |
| Allow attachments | No |

**Form fields:**

**Field 1 — Team type**
- Type: Dropdown
- Label: `Type of Team`
- Required: ✅ Yes
- Options:
  - Class (for teaching — linked to students)
  - Staff team (department, project, or working group)

**Field 2 — Team name**
- Type: Single Line Text
- Label: `Proposed team name`
- Required: ✅ Yes

**Field 3 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes
- Options: (full school list)

**Field 4 — Owner**
- Type: Single Line Text
- Label: `Who should be the team owner?`
- Required: ✅ Yes
- Help text: `The owner can add/remove members and manage settings`

**Field 5 — Initial members**
- Type: Paragraph Text
- Label: `List initial members to add (optional)`
- Required: ❌ No
- Placeholder: `First name, last name — one per line`

**Subject template:**
```
New Teams {{custom_field.cf_type_of_team}}: {{custom_field.cf_proposed_team_name}} — {{custom_field.cf_school}}
```

Save.

---

### B4 — Microsoft Teams: Add "Add/Remove Member from Team"

| Field | Value |
|---|---|
| Name | Add / Remove Member from Team |
| Description | Request to add or remove a member from an existing Microsoft Teams class or team. |
| Visibility | All Users |

**Form fields:**

**Field 1 — Action**
- Type: Dropdown
- Label: `Action required`
- Required: ✅ Yes
- Options: Add member / Remove member

**Field 2 — Team name**
- Type: Single Line Text
- Label: `Team name`
- Required: ✅ Yes

**Field 3 — Member to add/remove**
- Type: Single Line Text
- Label: `Name of person to add or remove`
- Required: ✅ Yes

**Field 4 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes

**Subject template:**
```
Teams Membership: {{custom_field.cf_action_required}} — {{custom_field.cf_team_name}}
```

Save.

---

### B5 — Email Groups: Add "New Distribution Group"

**Navigate to:** Admin → Service Catalog → Email Groups → + New Service Item

| Field | Value |
|---|---|
| Name | New Email Distribution Group |
| Description | Request a new email distribution group or shared mailbox for a team, department, or mailing list. |
| Visibility | All Users |

**Form fields:**

**Field 1 — Group type**
- Type: Dropdown
- Label: `Type of group`
- Required: ✅ Yes
- Options:
  - Distribution group (send-only, no shared inbox)
  - Shared mailbox (send and receive, shared inbox)

**Field 2 — Proposed email address**
- Type: Single Line Text
- Label: `Proposed email address`
- Required: ✅ Yes
- Placeholder: `e.g. office@schoolname.org.uk`

**Field 3 — Display name**
- Type: Single Line Text
- Label: `Display name`
- Required: ✅ Yes
- Placeholder: `e.g. School Name Office`

**Field 4 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes

**Field 5 — Initial members / owners**
- Type: Paragraph Text
- Label: `List initial members and who should be the owner`
- Required: ✅ Yes

**Subject template:**
```
New Email Group: {{custom_field.cf_proposed_email_address}} — {{custom_field.cf_school}}
```

Save.

---

### B6 — Email Groups: Add "Add / Remove Member from Group"

| Field | Value |
|---|---|
| Name | Add / Remove Member from Email Group |
| Description | Request to add or remove a member from an existing email distribution group or shared mailbox. |
| Visibility | All Users |

**Form fields:**

**Field 1 — Action**
- Type: Dropdown
- Label: `Action required`
- Required: ✅ Yes
- Options: Add member / Remove member

**Field 2 — Group email address**
- Type: Single Line Text
- Label: `Email group or shared mailbox address`
- Required: ✅ Yes

**Field 3 — Member name**
- Type: Single Line Text
- Label: `Name of person to add or remove`
- Required: ✅ Yes

**Field 4 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes

**Subject template:**
```
Email Group Membership: {{custom_field.cf_action_required}} — {{custom_field.cf_email_group_or_shared_mailbox_address}}
```

Save.

---

### B7 — Printing Credit: Add "Printing Credit Request"

**Navigate to:** Admin → Service Catalog → Printing Credit → + New Service Item

| Field | Value |
|---|---|
| Name | Printing Credit Request |
| Description | Request additional printing credit for your account. Standard credit allocations are set per term. Requests are reviewed and approved by your school's business manager. |
| Visibility | All Users |

**Form fields:**

**Field 1 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes

**Field 2 — Credit amount**
- Type: Dropdown
- Label: `Credit amount requested`
- Required: ✅ Yes
- Options:
  - 100 pages
  - 250 pages
  - 500 pages
  - Other (specify below)

**Field 3 — Reason**
- Type: Paragraph Text
- Label: `Reason for request`
- Required: ✅ Yes
- Placeholder: `e.g. end-of-year reports, exam resources`

**Field 4 — Other amount**
- Type: Single Line Text
- Label: `If Other — how many pages?`
- Required: ❌ No

**Subject template:**
```
Printing Credit: {{requested_for}} — {{custom_field.cf_school}} — {{custom_field.cf_credit_amount_requested}}
```

Save.

---

## Part C — Consolidate Google Classroom Items

This is the biggest structural change. There are currently **17 per-school items** in the Classroom Setup category. Staff from one school can see all schools' entries, which is confusing.

### Step 1: Create the consolidated item

**Navigate to:** Admin → Service Catalog → Classroom Setup → + New Service Item

| Field | Value |
|---|---|
| Name | Google Classroom Request |
| Description | Request a new Google Classroom for your class or year group. Classrooms are set up by IT and you will be added as the teacher. Submit at least 3 working days before the classroom is needed. |
| Visibility | All Users |
| Allow attachments | No |
| Icon | Google/classroom icon |

**Form fields:**

**Field 1 — School**
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes
- Options: (full school list — same as Staff Leaver)

**Field 2 — Class name**
- Type: Single Line Text
- Label: `Class or group name`
- Required: ✅ Yes
- Placeholder: `e.g. Year 5 Maths, 10B English, Science Club`

**Field 3 — Year group**
- Type: Dropdown
- Label: `Year group`
- Required: ✅ Yes
- Options:
  - Reception
  - Year 1
  - Year 2
  - Year 3
  - Year 4
  - Year 5
  - Year 6
  - Year 7
  - Year 8
  - Year 9
  - Year 10
  - Year 11
  - Year 12
  - Year 13
  - Mixed / All years
  - Not applicable (staff group)

**Field 4 — Date needed by**
- Type: Date
- Label: `Date needed by`
- Required: ✅ Yes

**Field 5 — Teacher email**
- Type: Single Line Text
- Label: `Teacher email address`
- Required: ✅ Yes
- Help text: `The classroom will be created under this email address`

**Field 6 — Co-teachers**
- Type: Paragraph Text
- Label: `Any co-teachers to add? (optional)`
- Required: ❌ No
- Placeholder: `Email addresses, one per line`

**Subject template:**
```
Google Classroom: {{custom_field.cf_class_or_group_name}} — {{custom_field.cf_school}} — {{custom_field.cf_year_group}}
```

Save.

---

### Step 2: Hide the 17 individual school items

Do NOT delete them — this would lose any linked ticket history.

For each of the 17 items listed below, open the item and change **Visibility** to **Agents only**:

1. Saint Georges Google Classroom
2. Ditton Junior Google Classroom
3. Halling Google Classroom
4. Cliffe Woods Google Classroom
5. Shorne Google Classroom
6. Holy Trinity Google Classroom
7. Rosherville Google Classroom
8. St Botolphs Google Classroom
9. Sedleys Google Classroom
10. Stone St Mary's Google Classroom
11. Sutton at Hone Google Classroom
12. Horton Kirby Google Classroom
13. Knole Google Classroom
14. Alkerden Google Classroom
15. Whitehill Google Classroom
16. Gravesend Grammar Google Classroom
17. (Check for any remaining — Rainham Mark may not exist yet)

Staff will no longer see the old items. The new consolidated item is all they see.

---

## Part D — Rename Items

### D1 — Rename "Copying Code" → "Photocopier PIN / Follow-Me Code"

**Navigate to:** Admin → Service Catalog → Security & Access → Copying Code

Change Name to: `Photocopier PIN / Follow-Me Code`

Save.

---

## Part E — Additional Portal Steps (Confirmed)

### E1 — Employee Onboarding - MS Active Directory

Leave in HR Management. Existing workflow automations are built against this item's current category — moving it would break them. No action needed.

---

### E2 — Google Drive Migration

Migration project still in progress — leave this item active in Security & Access. No action needed.

---

### E3 — Staff EV Charging Account Setup

Leave in Security & Access. No action needed.

---

### E4 — Microsoft Teams Classes

The consolidated **Google Classroom Request** form is sufficient. No separate Teams Classes item needed at this stage — if demand emerges it can be added to the Classroom Setup category later.

---

## Summary

| Part | Actions | Status |
|---|---|---|
| A — Rename categories | IT Services → Security & Access; Google/Teams Classes → Classroom Setup | ⏳ Pending portal |
| B — Populate empty categories | 7 new service items across User Accounts, Teams, Email Groups, Printing Credit | ⏳ Pending portal |
| C — Consolidate Google Classroom | 1 new item + hide 17 old items | ⏳ Pending portal |
| D — Rename items | Copying Code → Photocopier PIN / Follow-Me Code | ⏳ Pending portal |
| E — Pending confirmation | 4 items awaiting decisions | ⚠️ Awaiting |
