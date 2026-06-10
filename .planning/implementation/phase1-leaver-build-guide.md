# Phase 1: Staff Leaver Workflow — Build Guide
**Freshservice Admin Portal Steps**
**Date:** 10 June 2026

The "Staff Changes" category has been created via API (ID: 53000054716).
Everything below must be done in the Freshservice admin portal.

---

## Part A — Create the Staff Leaver Service Item

**Navigate to:** Admin → Service Catalog → Staff Changes category

### Step 1: Create the item

Click **+ New Service Item** inside the Staff Changes category.

| Field | Value |
|---|---|
| Name | Staff Leaver |
| Description | Use this form to notify all departments when a member of staff is leaving. Submit as soon as a leaving date is confirmed — at least 5 working days before their last day where possible. |
| Visibility | All Users |
| Allow attachments | No |
| Icon | Choose a person/exit icon from the library |

Click **Save** — do not add form fields yet, just create the item first.

---

### Step 2: Add form fields

Still on the Staff Leaver item, go to the **Form Fields** tab. Add the following fields in order:

---

**Field 1 — Staff member full name**
- Type: **Single Line Text**
- Label: `Staff member full name`
- Required: ✅ Yes
- Placeholder: `First name and last name`

---

**Field 2 — School**
- Type: **Dropdown**
- Label: `School`
- Required: ✅ Yes
- Options (add each):
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

**Field 3 — Job role / title**
- Type: **Single Line Text**
- Label: `Job role / title`
- Required: ✅ Yes
- Placeholder: `e.g. Class Teacher, Teaching Assistant, Site Manager`

---

**Field 4 — Employment type**
- Type: **Dropdown**
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

**Field 5 — Last working day**
- Type: **Date**
- Label: `Last working day`
- Required: ✅ Yes

---

**Field 6 — Reason for leaving**
- Type: **Dropdown**
- Label: `Reason for leaving`
- Required: ✅ Yes
- Options:
  - Resignation
  - Retirement
  - End of contract
  - Dismissal
  - Transfer to another Aletheia school
  - Other

---

**Field 7 — Internal transfer flag**
- Type: **Checkbox** (single checkbox)
- Label: `This is an internal transfer to another Aletheia school`
- Required: ❌ No
- Help text: `Tick this if the member of staff is moving to a different Aletheia school — accounts will be updated rather than disabled`

---

**Field 8 — Trust device**
- Type: **Dropdown**
- Label: `Does this member of staff have a trust-issued device?`
- Required: ✅ Yes
- Options: Yes / No

---

**Field 9 — ID card**
- Type: **Dropdown**
- Label: `Does this member of staff have an ID card?`
- Required: ✅ Yes
- Options: Yes / No

---

**Field 10 — Building access fob**
- Type: **Dropdown**
- Label: `Does this member of staff have a building access fob or key fob?`
- Required: ✅ Yes
- Options: Yes / No

---

**Field 11 — Governor flag**
- Type: **Dropdown**
- Label: `Is this person a Governor?`
- Required: ✅ Yes
- Options: Yes / No
- Help text: `If Yes, a separate IT support call will be raised for their Office 365 and GovernorHub accounts`

---

**Field 12 — Additional access notes**
- Type: **Paragraph Text**
- Label: `Any other accounts or system access to be aware of?`
- Required: ❌ No
- Placeholder: `e.g. named CCTV admin login, finance software account, Arbor admin access`
- Help text: `List any systems not covered by the standard process above`

---

**Field 13 — Additional notes**
- Type: **Paragraph Text**
- Label: `Anything else IT or HR should know?`
- Required: ❌ No

---

Click **Save** when all fields are added.

---

### Step 3: Set the ticket subject template

Still on the service item, find **Subject** (in the Configurations tab or similar):

Set to:
```
Staff Leaver: {{custom_field.cf_staff_member_full_name}} — {{custom_field.cf_school}} — Last day: {{custom_field.cf_last_working_day}}
```

This means every ticket has an immediately readable subject line for agents.

---

## Part B — Create the Workflow Automation (Child Tickets)

**Navigate to:** Admin → Workflow Automator → New Automator

Create **one automator** that fires when the Staff Leaver service request is submitted and creates all child tickets.

### Automator 1: Staff Leaver — Create Child Tickets

**Name:** `Staff Leaver — Create Child Tickets`

**Event:** Service Request is created

**Condition:**
- Service Item is **Staff Leaver**
- AND: Field `This is an internal transfer` is **NOT checked**

**Actions** (add all four in sequence):

---

**Action 1 — Create IT child ticket**

Create a linked ticket with:
| Setting | Value |
|---|---|
| Subject | `IT: Disable accounts — {{ticket.custom_field.cf_staff_member_full_name}} — Last day {{ticket.custom_field.cf_last_working_day}}` |
| Workspace | IT Support |
| Group | INC - [relevant hub — use requester's department to route, or default to INC - 2nd Line] |
| Priority | High |
| Type | Service Request |
| Description | See checklist below |

Description (paste exactly):
```
Staff Leaver — IT Actions Required
Last working day: {{ticket.custom_field.cf_last_working_day}}
School: {{ticket.custom_field.cf_school}}
Role: {{ticket.custom_field.cf_job_role_title}}
Device issued: {{ticket.custom_field.cf_does_this_member_of_staff_have_a_trust_issued_device}}
ID card issued: {{ticket.custom_field.cf_does_this_member_of_staff_have_an_id_card}}
Building fob issued: {{ticket.custom_field.cf_does_this_member_of_staff_have_a_building_access_fob_or_key_fob}}
Governor: {{ticket.custom_field.cf_is_this_person_a_governor}}
Additional access notes: {{ticket.custom_field.cf_any_other_accounts_or_system_access_to_be_aware_of}}

CHECKLIST — all must be completed by 17:00 on last working day:
[ ] Disable Microsoft 365 / Active Directory account
[ ] Set email out-of-office and redirect if required
[ ] Remove from all Teams, SharePoint sites and shared mailboxes
[ ] Disable MIS (Arbor) account if applicable
[ ] Revoke CCTV system access if applicable
[ ] Revoke finance system access if applicable
[ ] Revoke Sign In App access if applicable
[ ] Revoke any other named access (see notes above)
[ ] Collect device (if issued)
[ ] Deactivate ID card (if issued)
[ ] Deactivate building access fob (if issued)
[ ] GOVERNOR: If Yes above — raise a separate support call for Office 365 account removal (do not delay this ticket)
[ ] Confirm all actions completed — record date and time in ticket notes
```

---

**Action 2 — Create People & Culture child ticket**

| Setting | Value |
|---|---|
| Subject | `People & Culture: Leaver process — {{ticket.custom_field.cf_staff_member_full_name}}` |
| Workspace | People & Culture |
| Priority | Medium |
| Type | Service Request |

Description:
```
Staff Leaver — People & Culture Actions
Last working day: {{ticket.custom_field.cf_last_working_day}}
School: {{ticket.custom_field.cf_school}}
Role: {{ticket.custom_field.cf_job_role_title}}
Reason: {{ticket.custom_field.cf_reason_for_leaving}}

CHECKLIST:
[ ] Confirm termination date on HR system
[ ] Process P45
[ ] Send final pay information to Finance via payroll portal
[ ] Collect any HR documentation from leaver
[ ] Confirm reference policy with line manager
[ ] Update personnel record status to Leaver
```

---

**Action 3 — Create Finance child ticket**

| Setting | Value |
|---|---|
| Subject | `Finance: Final pay — {{ticket.custom_field.cf_staff_member_full_name}} — Last day {{ticket.custom_field.cf_last_working_day}}` |
| Workspace | Finance |
| Priority | Medium |
| Type | Service Request |

Description:
```
Staff Leaver — Finance Actions
Last working day: {{ticket.custom_field.cf_last_working_day}}
School: {{ticket.custom_field.cf_school}}
Device issued: {{ticket.custom_field.cf_does_this_member_of_staff_have_a_trust_issued_device}}

CHECKLIST:
[ ] Confirm final salary payment date and amount
[ ] Stop any recurring expense allowances or travel claims
[ ] Process equipment cost recovery if device is not returned (liaise with IT)
[ ] Update budget records
```

---

**Action 4 — Create Marketing child ticket**

| Setting | Value |
|---|---|
| Subject | `Marketing: Update comms lists — {{ticket.custom_field.cf_staff_member_full_name}}` |
| Workspace | Marketing & Communications |
| Priority | Low |
| Type | Service Request |

Description:
```
Staff Leaver — Marketing & Communications Actions
Last working day: {{ticket.custom_field.cf_last_working_day}}
School: {{ticket.custom_field.cf_school}}

CHECKLIST:
[ ] Remove from trust-wide mailing lists and distribution groups
[ ] Remove from staff directory or intranet profile if applicable
[ ] Update any public-facing content that references this person
```

---

Save the automator and set it to **Active**.

---

## Part C — Create the Escalation Automation

**Navigate to:** Admin → Workflow Automator → New Automator

**Name:** `Staff Leaver — IT Escalation on Last Working Day`

**Event:** Ticket is updated (time-based: at 17:00 on the due date)

**Condition:**
- Subject contains `IT: Disable accounts`
- AND: Status is NOT Resolved
- AND: Status is NOT Closed

**Action:**
- Send email notification to: Luke Dobson (luke@aletheiatrust.org.uk — or use agent lookup)
- Email subject: `⚠ OVERDUE: Staff leaver IT ticket not resolved — {{ticket.subject}}`
- Email body:
  ```
  An IT staff leaver ticket has not been resolved by the end of the last working day.

  Ticket: {{ticket.subject}}
  Due: {{ticket.due_by}}
  Assigned to: {{ticket.agent_name}}

  Please ensure all accounts are disabled immediately.

  View ticket: {{ticket.url}}
  ```

Save and set to **Active**.

---

## Part D — Closing Notification

**Navigate to:** Admin → Email Notifications → Requester Notifications

Find or create: **Service Request Resolved** notification.

Ensure it is enabled so that when the parent ticket is closed, the requester receives a confirmation email automatically. Freshservice sends this by default — verify it is turned on for the Staff Changes workspace.

---

## Part E — Test the Workflow

Before going live, run a full end-to-end test:

1. Log in as a test school user (or use your own account)
2. Navigate to the portal → Staff Changes → Staff Leaver
3. Fill in the form with test data — use a fictitious name, set last working day to tomorrow
4. Submit
5. Verify:
   - [ ] Parent ticket created with correct subject line
   - [ ] 4 child tickets created (IT, People & Culture, Finance, Marketing)
   - [ ] IT child ticket has full checklist in description
   - [ ] IT child ticket is Priority: High
   - [ ] Marketing child ticket is Priority: Low
   - [ ] Submitter receives confirmation email when all tickets closed
6. Close all child tickets
7. Verify parent auto-closes and confirmation email is sent
8. Test escalation: leave IT ticket open past 17:00 and verify escalation email fires

**Sign off test results before publishing the form to all staff.**

---

## Summary of What Was Done via API vs Portal

| Item | Method | Status |
|---|---|---|
| "Staff Changes" category created | API | ✅ Done |
| Staff Leaver service item | Portal (steps above) | ⏳ Pending |
| Form fields (13 fields) | Portal (steps above) | ⏳ Pending |
| Child ticket workflow automator | Portal (steps above) | ⏳ Pending |
| Escalation automator | Portal (steps above) | ⏳ Pending |
| End-to-end test | Portal | ⏳ Pending |
