---
layout: default
title: Phase 8 — Department Catalogues Guide
parent: Implementation
nav_order: 8
---

# Phase 8: Finance, People & Culture, and Marketing Catalogues — Build Guide
**Date:** 10 June 2026
**Status:** Requires department head input sessions before full build

This phase builds out the service catalogue for the three non-IT workspaces. The items below are recommended based on common needs in multi-academy trusts. Each department head should review and confirm before items go live.

---

## Finance Catalogue

**Workspace:** Finance (Workspace 10)
**Category:** Create a new category: **Finance Requests** within the Finance workspace

### Recommended Service Items

---

#### F1 — Purchase Order Request

| Field | Value |
|---|---|
| Name | Purchase Order Request |
| Description | Request a purchase order for goods or services. All purchases over £100 require a PO before the order is placed. |
| Priority | Medium |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown — full school list)
2. Supplier name (Single Line Text, required)
3. Description of goods/services (Paragraph Text, required)
4. Estimated total cost (Single Line Text, required — e.g. £250.00)
5. Budget code (Single Line Text, required)
6. Date required by (Date, required)
7. Supporting documentation (Attachment — invoice quote, prospectus etc)
8. Additional notes (Paragraph Text, optional)

**Subject template:**
```
PO Request: {{custom_field.cf_supplier_name}} — {{custom_field.cf_school}} — {{custom_field.cf_estimated_total_cost}}
```

---

#### F2 — Expense Claim

| Field | Value |
|---|---|
| Name | Expense Claim |
| Description | Submit an expense claim for out-of-pocket costs incurred in the course of your work. Attach receipts. Claims without receipts cannot be processed. |
| Priority | Medium |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Claim period (Single Line Text — e.g. May 2026)
3. Total amount claimed (Single Line Text, required)
4. Description of expenses (Paragraph Text, required)
5. Receipts (Attachment, required)
6. Bank account confirmed on HR system? (Dropdown: Yes / No — if No, direct to HR first)

**Subject template:**
```
Expense Claim: {{requested_for}} — {{custom_field.cf_school}} — {{custom_field.cf_claim_period}}
```

---

#### F3 — Budget Query

| Field | Value |
|---|---|
| Name | Budget Query |
| Description | Raise a query about your school or department budget, a budget code, or a spend report. |
| Priority | Low |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Query type (Dropdown: Budget balance / Budget code query / Spend report / Forecast / Other)
3. Details (Paragraph Text, required)

**Subject template:**
```
Budget Query: {{custom_field.cf_query_type}} — {{custom_field.cf_school}}
```

---

#### F4 — New Supplier Setup

| Field | Value |
|---|---|
| Name | New Supplier Setup |
| Description | Request a new supplier to be added to the finance system. A signed supplier form and bank details are required before any payment can be made. |
| Priority | Medium |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Supplier name (Single Line Text, required)
3. Supplier contact name (Single Line Text, required)
4. Supplier email (Single Line Text, required)
5. Supplier address (Paragraph Text, required)
6. Signed supplier form (Attachment, required)
7. Additional notes (Paragraph Text, optional)

**Subject template:**
```
New Supplier: {{custom_field.cf_supplier_name}} — {{custom_field.cf_school}}
```

---

#### F5 — Payroll Query

| Field | Value |
|---|---|
| Name | Payroll Query |
| Description | Raise a query about your payslip, pay date, deductions, pension, or any other payroll matter. |
| Priority | Medium |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Query type (Dropdown: Payslip / Pay date / Deductions / Pension / Tax code / Other)
3. Pay period affected (Single Line Text — e.g. June 2026)
4. Details (Paragraph Text, required)
5. Note: Do not include bank account or National Insurance details in this form.

**Subject template:**
```
Payroll Query: {{custom_field.cf_query_type}} — {{requested_for}} — {{custom_field.cf_pay_period_affected}}
```

---

## People & Culture Catalogue

**Workspace:** People & Culture (Workspace 9)
**Category:** Create a new category: **HR Requests** within the People & Culture workspace

### Recommended Service Items

---

#### H1 — Absence Notification

| Field | Value |
|---|---|
| Name | Absence Notification |
| Description | Notify HR of a staff absence. For same-day absences, contact your line manager directly first, then complete this form. |
| Priority | High |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Absence type (Dropdown: Sickness / Compassionate / Emergency / Planned — other leave / Other)
3. First day of absence (Date, required)
4. Expected return date (Date, optional)
5. Cover arranged? (Dropdown: Yes / No / Not applicable)
6. Additional details (Paragraph Text, optional)

**Subject template:**
```
Absence: {{requested_for}} — {{custom_field.cf_school}} — From {{custom_field.cf_first_day_of_absence}}
```

---

#### H2 — Contract / Employment Query

| Field | Value |
|---|---|
| Name | Contract or Employment Query |
| Description | Raise a query about your contract, working hours, leave entitlement, or terms and conditions of employment. |
| Priority | Medium |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Query type (Dropdown: Contract terms / Hours / Annual leave / Maternity/Paternity / Flexible working / Other)
3. Details (Paragraph Text, required)

**Subject template:**
```
HR Query: {{custom_field.cf_query_type}} — {{requested_for}} — {{custom_field.cf_school}}
```

---

#### H3 — DBS Check Request

| Field | Value |
|---|---|
| Name | DBS Check Request |
| Description | Request a new or renewal DBS check. Provide all required identification documents before the check can be processed. |
| Priority | High |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Check type (Dropdown: New check / Renewal / Enhanced / Standard)
3. Staff member name (Single Line Text, required — for line managers submitting on behalf of others)
4. Role (Single Line Text, required)
5. ID documents provided? (Dropdown: Yes — to HR directly / No — to be arranged)
6. Additional notes (Paragraph Text, optional)

**Subject template:**
```
DBS Check: {{custom_field.cf_staff_member_name}} — {{custom_field.cf_school}} — {{custom_field.cf_check_type}}
```

---

#### H4 — Reference Request

| Field | Value |
|---|---|
| Name | Reference Request |
| Description | Request an employment reference for a current or former member of staff. All references must be authorised by HR before being issued. |
| Priority | Medium |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Staff member name (Single Line Text)
3. Requesting organisation (Single Line Text)
4. Reference type (Dropdown: Standard employment / Character / Academic)
5. Deadline (Date)
6. Additional details (Paragraph Text, optional)

**Subject template:**
```
Reference: {{custom_field.cf_staff_member_name}} — {{custom_field.cf_school}} — Due {{custom_field.cf_deadline}}
```

---

## Marketing & Communications Catalogue

**Workspace:** Marketing & Communications (Workspace 11)
**Category:** Create a new category: **Communications Requests** within the Marketing workspace

### Recommended Service Items

---

#### M1 — Content / Copywriting Request

| Field | Value |
|---|---|
| Name | Content or Copywriting Request |
| Description | Request help writing or reviewing content for newsletters, letters to parents, website copy, or social media. |
| Priority | Low |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Content type (Dropdown: Newsletter / Parent letter / Website / Social media / Press release / Other)
3. Audience (Dropdown: Parents / Staff / Governors / Public / Mixed)
4. Deadline (Date, required)
5. Brief / key messages (Paragraph Text, required)
6. Draft to review (Attachment, optional)

**Subject template:**
```
Content Request: {{custom_field.cf_content_type}} — {{custom_field.cf_school}} — Due {{custom_field.cf_deadline}}
```

---

#### M2 — Photography / Media Request

| Field | Value |
|---|---|
| Name | Photography or Media Request |
| Description | Request photography, video, or other media coverage for a school event or activity. |
| Priority | Low |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Event / activity name (Single Line Text, required)
3. Date of event (Date, required)
4. Time and location (Single Line Text, required)
5. Media type (Dropdown: Photography / Video / Both)
6. Consent confirmed? (Dropdown: Yes — all subjects have current consent / No — consent to be arranged / Not applicable)
7. Additional details (Paragraph Text, optional)

**Subject template:**
```
Media Request: {{custom_field.cf_event_activity_name}} — {{custom_field.cf_school}} — {{custom_field.cf_date_of_event}}
```

---

#### M3 — Brand / Logo / Design Request

| Field | Value |
|---|---|
| Name | Brand or Design Request |
| Description | Request design assets, branded materials, or guidance on correct use of the Aletheia brand. |
| Priority | Low |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Request type (Dropdown: Logo files / Branded template / New design / Brand guidance / Other)
3. Format needed (Single Line Text — e.g. PNG, PDF, PowerPoint)
4. Deadline (Date, optional)
5. Details (Paragraph Text, required)

**Subject template:**
```
Brand Request: {{custom_field.cf_request_type}} — {{custom_field.cf_school}}
```

---

#### M4 — Social Media Request

| Field | Value |
|---|---|
| Name | Social Media Post Request |
| Description | Request a social media post on trust or school channels. Content must be approved before publishing. Allow at least 3 working days. |
| Priority | Low |
| Visibility | All Users |

**Form fields:**
1. School (Dropdown)
2. Platform (Checkbox multi-select: Facebook / X (Twitter) / Instagram / LinkedIn / School website)
3. Preferred publish date (Date, optional)
4. Draft post content (Paragraph Text, required)
5. Images to attach (Attachment, optional)
6. Consent confirmed for any people featured? (Dropdown: Yes / No / No people featured)

**Subject template:**
```
Social Media: {{custom_field.cf_school}} — {{custom_field.cf_preferred_publish_date}}
```

---

## Implementation Notes

- Each workspace catalogue requires the relevant department head to confirm items before go-live
- Departments new to Freshservice (Finance, HR, Marketing) should be introduced to the platform before their catalogue launches — a short walkthrough is recommended
- Start with 2–3 items per department and expand over time based on usage
- Set up email notifications for each workspace so department heads receive alerts when tickets are raised

---

## Summary

| Department | Items | Status |
|---|---|---|
| Finance | F1 Purchase Order, F2 Expense Claim, F3 Budget Query, F4 New Supplier, F5 Payroll Query | ⏳ Confirm with Finance lead |
| People & Culture | H1 Absence, H2 Contract Query, H3 DBS Check, H4 Reference | ⏳ Confirm with HR lead |
| Marketing | M1 Content, M2 Photography, M3 Brand/Design, M4 Social Media | ⏳ Confirm with Marketing lead |
