---
layout: default
title: Phase 5 — Onboarding Workflow Guide
parent: Implementation
nav_order: 5
---

# Phase 5: New Staff Onboarding Workflow — Build Guide
**Date:** 10 June 2026
**Status:** Ready for portal actioning

Mirror of the Phase 1 leaver workflow but for new starters. Triggered by school business managers or headteachers. Submit at least 5 working days before the start date.

---

## Part A — Create the New Staff Member Service Item

**Navigate to:** Admin → Service Catalog → Staff Changes → + New Service Item

| Field | Value |
|---|---|
| Name | New Staff Member |
| Description | Use this form to notify IT, HR, and Finance when a new member of staff is joining. Submit at least 5 working days before their start date to ensure accounts and access are ready on day one. |
| Visibility | All Users |
| Allow attachments | No |
| Icon | person-plus icon |

Click **Save** — do not add form fields yet.

---

## Part B — Add Form Fields

### Field 1 — Staff member full name
- Type: Single Line Text
- Label: `Staff member full name`
- Required: ✅ Yes
- Placeholder: `First name and last name`

---

### Field 2 — School
- Type: Dropdown
- Label: `School`
- Required: ✅ Yes
- Options:
  - Alkerden C of E Academy
  - Cliffe Woods Primary School
  - Ditton C of E Junior School
  - Gravesend Grammar School
  - Halling Primary School
  - Holy Trinity C of E Primary School
  - Horton Kirby C of E Primary School
  - Knole Academy
  - Rosherville C of E Academy
  - Saint Georges C of E School (All Through)
  - Saint Georges C of E School (Primary)
  - Sedleys C of E Primary School
  - Shorne C of E Primary School
  - St Botolphs C of E Primary School
  - Stone St Mary's C of E Primary School
  - Sutton-at-Hone C of E Primary School
  - Whitehill Primary School
  - Central Trust (Aletheia)

---

### Field 3 — Job role / title
- Type: Single Line Text
- Label: `Job role / title`
- Required: ✅ Yes
- Placeholder: `e.g. Class Teacher, Teaching Assistant, Site Manager`

---

### Field 4 — Employment type
- Type: Dropdown
- Label: `Employment type`
- Required: ✅ Yes
- Options:
  - Teaching staff
  - Support staff
  - Governor
  - Contractor
  - Central trust staff
  - Other

---

### Field 5 — Start date
- Type: Date
- Label: `Start date`
- Required: ✅ Yes

---

### Field 6 — Contract type
- Type: Dropdown
- Label: `Contract type`
- Required: ✅ Yes
- Options:
  - Permanent
  - Fixed term
  - Supply / temporary
  - Contractor

---

### Field 7 — Internal transfer flag
- Type: Checkbox (single checkbox)
- Label: `This is an internal transfer from another Aletheia school`
- Required: ❌ No
- Help text: `Tick this if the member of staff is moving from a different Aletheia school — existing accounts will be updated rather than created fresh`

---

### Field 8 — Accounts required
- Type: Checkbox (multi-select)
- Label: `Which accounts and access are needed?`
- Required: ✅ Yes
- Options:
  - Microsoft 365 (email, Teams, OneDrive)
  - Active Directory / school computer login
  - Arbor MIS
  - Google Workspace
  - Sign In App admin access
  - Other (specify below)

---

### Field 9 — Trust device required
- Type: Dropdown
- Label: `Does this staff member require a trust-issued device?`
- Required: ✅ Yes
- Options: Yes / No

---

### Field 10 — ID card required
- Type: Dropdown
- Label: `Does this staff member require an ID card?`
- Required: ✅ Yes
- Options: Yes / No

---

### Field 11 — Building access fob required
- Type: Dropdown
- Label: `Does this staff member require a building access fob?`
- Required: ✅ Yes
- Options: Yes / No

---

### Field 12 — Line manager
- Type: Single Line Text
- Label: `Line manager name`
- Required: ✅ Yes
- Help text: `IT will copy the line manager into the IT setup confirmation`

---

### Field 13 — Additional access notes
- Type: Paragraph Text
- Label: `Any specific system access or permissions needed?`
- Required: ❌ No
- Placeholder: `e.g. Arbor admin access, CCTV viewer access, finance system access`

---

### Field 14 — Additional notes
- Type: Paragraph Text
- Label: `Anything else IT or HR should know?`
- Required: ❌ No

---

Click **Save** when all fields are added.

---

## Part C — Set the Ticket Subject Template

```
New Staff: {{custom_field.cf_staff_member_full_name}} — {{custom_field.cf_school}} — Start: {{custom_field.cf_start_date}}
```

---

## Part D — Create the Workflow Automation

**Navigate to:** Admin → Workflow Automator → New Automator

**Name:** `New Staff — Create Child Tickets`

**Event:** Service Request is created

**Condition:**
- Service Item is **New Staff Member**
- AND: Field `This is an internal transfer` is **NOT checked**

**Actions (add all three in sequence):**

---

### Action 1 — Create IT child ticket

| Setting | Value |
|---|---|
| Subject | `IT: New account setup — {{ticket.custom_field.cf_staff_member_full_name}} — Start {{ticket.custom_field.cf_start_date}}` |
| Workspace | IT Support |
| Priority | High |
| Type | Service Request |

Description:
```
New Staff Member — IT Actions Required
Start date: {{ticket.custom_field.cf_start_date}}
School: {{ticket.custom_field.cf_school}}
Role: {{ticket.custom_field.cf_job_role_title}}
Contract: {{ticket.custom_field.cf_contract_type}}
Device required: {{ticket.custom_field.cf_does_this_staff_member_require_a_trust_issued_device}}
ID card required: {{ticket.custom_field.cf_does_this_staff_member_require_an_id_card}}
Building fob required: {{ticket.custom_field.cf_does_this_staff_member_require_a_building_access_fob}}
Accounts needed: {{ticket.custom_field.cf_which_accounts_and_access_are_needed}}
Additional access: {{ticket.custom_field.cf_any_specific_system_access_or_permissions_needed}}
Line manager: {{ticket.custom_field.cf_line_manager_name}}

CHECKLIST — all must be completed before start date:
[ ] Create Microsoft 365 account (email, Teams, OneDrive)
[ ] Create Active Directory / school computer login
[ ] Set up Arbor MIS account (if required)
[ ] Set up Google Workspace account (if required)
[ ] Configure Sign In App access (if required)
[ ] Set up any additional named access (see notes above)
[ ] Prepare device if required — configure, name, asset tag
[ ] Arrange ID card if required
[ ] Arrange building access fob if required
[ ] Send welcome email to line manager with login details
[ ] Confirm all actions completed before start date
```

---

### Action 2 — Create People & Culture child ticket

| Setting | Value |
|---|---|
| Subject | `People & Culture: New starter process — {{ticket.custom_field.cf_staff_member_full_name}} — Start {{ticket.custom_field.cf_start_date}}` |
| Workspace | People & Culture |
| Priority | High |
| Type | Service Request |

Description:
```
New Staff Member — People & Culture Actions
Start date: {{ticket.custom_field.cf_start_date}}
School: {{ticket.custom_field.cf_school}}
Role: {{ticket.custom_field.cf_job_role_title}}
Contract type: {{ticket.custom_field.cf_contract_type}}
Employment type: {{ticket.custom_field.cf_employment_type}}

CHECKLIST:
[ ] Issue contract and new starter paperwork
[ ] Complete DBS check and record outcome
[ ] Verify right to work documentation
[ ] Add to HR system
[ ] Confirm payroll start date with Finance
[ ] Brief line manager on induction schedule
[ ] Schedule induction day
```

---

### Action 3 — Create Finance child ticket

| Setting | Value |
|---|---|
| Subject | `Finance: New starter payroll setup — {{ticket.custom_field.cf_staff_member_full_name}} — Start {{ticket.custom_field.cf_start_date}}` |
| Workspace | Finance |
| Priority | Medium |
| Type | Service Request |

Description:
```
New Staff Member — Finance Actions
Start date: {{ticket.custom_field.cf_start_date}}
School: {{ticket.custom_field.cf_school}}
Role: {{ticket.custom_field.cf_job_role_title}}
Contract type: {{ticket.custom_field.cf_contract_type}}

CHECKLIST:
[ ] Set up on payroll system
[ ] Confirm salary grade and pay date
[ ] Collect bank details
[ ] Set up pension enrolment (auto-enrol if eligible)
[ ] Confirm budget code for post
```

---

Save the automator and set it to **Active**.

---

## Part E — Internal Transfer Automation

Create a second automator for the internal transfer path (IT-only child ticket):

**Name:** `New Staff — Internal Transfer IT Ticket`

**Event:** Service Request is created

**Condition:**
- Service Item is **New Staff Member**
- AND: Field `This is an internal transfer from another Aletheia school` IS checked

**Action — Create IT child ticket:**

| Setting | Value |
|---|---|
| Subject | `IT: Internal transfer account update — {{ticket.custom_field.cf_staff_member_full_name}} — Start {{ticket.custom_field.cf_start_date}}` |
| Workspace | IT Support |
| Priority | High |
| Type | Service Request |

Description:
```
Internal Transfer — IT Actions Required
Start date: {{ticket.custom_field.cf_start_date}}
New school: {{ticket.custom_field.cf_school}}
Role: {{ticket.custom_field.cf_job_role_title}}
Accounts needed: {{ticket.custom_field.cf_which_accounts_and_access_are_needed}}
Line manager: {{ticket.custom_field.cf_line_manager_name}}

CHECKLIST:
[ ] Update Microsoft 365 account — UPN, display name, school assignment
[ ] Move to correct OU in Active Directory
[ ] Update Arbor MIS account for new school
[ ] Update Google Workspace organisational unit
[ ] Update building access fob if required
[ ] Confirm with line manager at new school
```

Save and set to **Active**.

---

## Part F — Early Submission Reminder

Add a note to the service item description and confirm with HR that the form should be submitted as soon as a start date is confirmed — minimum 5 working days before. This is especially important for new term starters in September.

---

## Part G — Test

Before going live:

1. Submit a test request with a fictitious name, start date one week ahead
2. Verify:
   - [ ] Parent ticket created with correct subject
   - [ ] 3 child tickets created (IT, People & Culture, Finance)
   - [ ] IT child ticket is Priority: High
   - [ ] All form field values appear correctly in child ticket descriptions
3. Test the transfer path: tick the internal transfer checkbox and verify only the IT ticket is created
4. Close all child tickets and verify parent auto-closes

---

## Summary

| Item | Method | Status |
|---|---|---|
| New Staff Member service item | Portal (steps above) | ⏳ Pending |
| Form fields (14 fields) | Portal (steps above) | ⏳ Pending |
| Standard new starter automator (3 child tickets) | Portal (steps above) | ⏳ Pending |
| Internal transfer automator (IT only) | Portal (steps above) | ⏳ Pending |
| End-to-end test | Portal | ⏳ Pending |
