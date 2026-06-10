---
layout: default
title: Project Handoff
nav_order: 2
---

# Project Handoff — Freshservice & 3CX
**Aletheia Academies Trust**
**Date:** 10 June 2026
**Prepared by:** Claude (Anthropic) acting as Senior Freshservice Consultant
**Handed to:** Luke Dobson, IT Lead — Aletheia Academies Trust

---

## Documentation Site

**Everything is published here:**
**https://aletheiatrust.github.io/freshservice-3cx/**

**GitHub repository:**
**https://github.com/aletheiatrust/freshservice-3cx**

The sidebar on the docs site has every report, guide, and design document. The README on the GitHub repo has a direct link table to every page.

---

## What Has Been Done

### Completed via API (live on Freshservice now)

| Item | Date | Detail |
|---|---|---|
| KB typo fixed | 10 Jun 2026 | "Polices" → "Policies" in eSafety category |
| Pupil Progress KB hidden | 10 Jun 2026 | Set to agents-only (system unused) |
| Pupil Progress KB deleted | 10 Jun 2026 | Confirmed decommissioned — removed entirely |
| Microsoft Office KB renamed | 10 Jun 2026 | Now "Microsoft 365" |
| Whitehill domain added | 10 Jun 2026 | whitehillprimary.com added to department |
| Knole Academy updated | 10 Jun 2026 | David Collins set as head, knoleacademy.org added, type set to Secondary |
| Staff Changes category created | 10 Jun 2026 | Service catalogue category ID: 53000054716 |

### Confirmed decisions (documented, no action taken)

| Item | Decision |
|---|---|
| Gravesend department | Intentionally incomplete — pending AD migration before merger with Gravesend Grammar |
| Rainham Mark Grammar | Onboarding in progress — do not configure yet |
| Saint Georges Primary | Known limitation — cannot add shared domain; tickets route to all-through and need manual reassignment |
| Sedleys ID card type "Plan" | Confirmed correct — no change needed |
| Google Classroom items (17) | Left untouched — automations built on them |
| Employee Onboarding - MS AD | Left in HR Management — automations built on it |
| Google Drive Migration item | Left active — project still ongoing |

---

## What Needs Doing — By Phase

### Phase 1 — Staff Leaver Workflow
**Status:** Guide written, portal steps pending
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase1-leaver-build-guide
**Who does it:** Freshservice admin (Luke or delegate)
**Time to complete:** ~2 hours in the portal

Key steps:
1. Create Staff Leaver service item in Staff Changes category
2. Add 13 form fields
3. Create child ticket automator (4 child tickets: IT, HR, Finance, Marketing)
4. Create escalation automator (IT ticket overdue at 17:00 on last working day → email Luke)
5. Verify closing notification is enabled
6. Run end-to-end test with fictitious data

**This is the highest priority item — safeguarding and GDPR risk until it is live.**

---

### Phase 2 — Service Catalogue Restructure
**Status:** Guide written, portal steps pending
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase2-catalogue-build-guide
**Who does it:** Freshservice admin
**Time to complete:** ~3 hours in the portal

Key steps:
1. Rename "IT Services" → "Security & Access"
2. Rename "Google / Teams Classes" → "Classroom Setup"
3. Create 7 new service items (Password Reset, New User Account, Teams items, Email Group items, Printing Credit)
4. Rename "Copying Code" → "Photocopier PIN / Follow-Me Code"

After completing: note the display_id from the URL of each new item — needed for Phase 4 tile links.

---

### Phase 3 — Knowledge Base Restructure
**Status:** Category-level work guide written; content audit deferred
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase3-kb-restructure-guide
**Who does it:** Freshservice admin
**Time to complete:** ~1–2 hours in the portal (structure only)

Key steps:
1. Create 4 new KB categories: Microsoft Teams, People & Culture, Finance, Marketing & Communications
2. Move Teams folder from Microsoft 365 into new Microsoft Teams category
3. Move Internet Filtering and Remote Desktop folders from Software into eSafety, Policies & Security
4. Merge Microsoft Surface into Hardware (move all folders, delete empty category)
5. Rename Software → "Applications & Software"

**Content audit (deferred):** Article-level review and rewrites are on hold until API access to articles is confirmed or a manual review session is scheduled. Priority order when picked up: Microsoft 365 → eSafety → Arbor → Software → Google. Check API key scopes in Freshservice admin (Admin → API Settings) — if Knowledge Base scope can be enabled, the content audit can be done programmatically.

---

### Phase 4 — Portal Redesign
**Status:** Guide written with full CSS and HTML ready to paste
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase4-portal-redesign-guide
**Who does it:** Freshservice admin
**Time to complete:** ~1 hour in the portal

Key steps:
1. Set primary colour to `#1e4379` in portal settings
2. Upload Aletheia logo (white/light version for navy header)
3. Paste the full CSS block into the portal CSS editor
4. Add the quick-access tiles HTML block to the homepage
5. Add the department cards HTML block to the homepage
6. Set 5 featured knowledge articles

**After Phase 1 & 2 portal steps:** Return to the tiles HTML and replace `ITEM_ID_*` placeholders with the actual display_ids (found in the URL of each service item in the portal).

**3CX widget:** The homepage has a placeholder comment for the live chat script. Add the actual script in Phase 6.

---

### Phase 5 — New Staff Onboarding Workflow
**Status:** Guide written, portal steps pending
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase5-onboarding-workflow-guide
**Who does it:** Freshservice admin
**Time to complete:** ~2 hours in the portal

Mirror of Phase 1. Creates 3 child tickets (IT, HR, Finance) when a new staff member form is submitted. 14 form fields. Separate path for internal transfers (IT-only ticket).

---

### Phase 6 — 3CX Live Chat Integration
**Status:** Guide written
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase6-3cx-integration-guide
**Who does it:** 3CX admin + Freshservice admin
**Time to complete:** ~2 hours

Key steps:
1. Create IT Support Live Chat queue in 3CX, hours 08:00–16:30 Mon–Fri
2. Configure widget appearance (navy `#1e4379`)
3. Copy widget JS snippet from 3CX admin
4. Paste widget script into Freshservice portal homepage (replacing the Phase 4 placeholder)
5. Configure Freshservice CRM connector in 3CX (auto-creates tickets from chats/calls)
6. Test: widget visible, online/offline states correct, chat creates Freshservice ticket
7. Announce to staff

---

### Phase 7 — SharePoint Integration
**Status:** Guide written
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase7-sharepoint-integration-guide
**Who does it:** SharePoint admin + Freshservice admin
**Time to complete:** ~1–2 hours

SharePoint tenant: saintgeorgescofeschool647.sharepoint.com
Microsoft 365 SSO is already active — no extra auth config needed.

Key steps:
1. Embed Freshservice support widget on SharePoint intranet homepage (test iFrame first; if blocked by X-Frame-Options, use widget script instead)
2. Add SharePoint link to Freshservice portal header
3. Optionally create a dedicated IT Support Hub page on SharePoint
4. Update KB articles to link directly to relevant SharePoint document libraries

---

### Phase 8 — Finance, HR, and Marketing Catalogues
**Status:** Guide written with recommended items; department input required
**Guide:** https://aletheiatrust.github.io/freshservice-3cx/implementation/phase8-department-catalogues-guide
**Who does it:** Department heads + Freshservice admin
**Time to complete:** ~1 hour per department (after sign-off sessions)

Recommended items:
- **Finance:** Purchase Order Request, Expense Claim, Budget Query, New Supplier Setup, Payroll Query
- **People & Culture:** Absence Notification, Contract/Employment Query, DBS Check Request, Reference Request
- **Marketing:** Content/Copywriting Request, Photography/Media Request, Brand/Design Request, Social Media Post Request

Before building: schedule a short walkthrough with each department head to confirm items and descriptions are correct for how they work.

---

### Deferred — KB Content Audit
**Status:** Noted — to be picked up separately
**Detail:** Article-level review and rewrites deferred pending API scope fix or manual review session.
**To unblock:** Check API key scopes in Freshservice Admin → API Settings. Enable Knowledge Base / Solutions scope if available. Once enabled, content can be pulled and reviewed programmatically.
**Priority order:** Microsoft 365 → eSafety, Policies & Security → Arbor → Software → Google

---

## Key Technical Notes

| Item | Detail |
|---|---|
| Freshservice domain | aletheiaacademiestrust.freshservice.com |
| Portal URL | https://support.aletheiatrust.org |
| API key | Stored in `.env` (gitignored) — never committed to repo |
| Workspaces | IT Support (2), People & Culture (9), Finance (10), Marketing & Comms (11) |
| Staff Changes category ID | 53000054716 |
| 3CX version | Version 20 Update 8, self-hosted |
| SharePoint tenant | saintgeorgescofeschool647.sharepoint.com |
| IT support email | IT@aletheiatrust.org.uk |
| Brand colours | Navy `#1e4379` / Crimson `#e22a20` |
| Escalation contact | Luke Dobson — luke@aletheiatrust.org.uk |

---

## Recommended Sequence

If picking this up fresh, work through the phases in this order:

1. **Phase 1** — Leaver workflow (safeguarding priority)
2. **Phase 2** — Catalogue restructure (creates the items needed for Phase 4 tiles)
3. **Phase 4** — Portal redesign (CSS and HTML, update tile links after Phase 2)
4. **Phase 3** — KB structure (portal work) + content audit when API scope available
5. **Phase 5** — Onboarding workflow (natural companion to Phase 1)
6. **Phase 6** — 3CX live chat
7. **Phase 7** — SharePoint integration
8. **Phase 8** — Department catalogues (requires department head sessions)

---

## Files in This Repository

```
.env                          ← API credentials (gitignored)
CLAUDE.md                     ← Project brief and working principles
.planning/
  audits/
    department-notes.md       ← Known issues per department
  reports/
    01-initial-assessment.md  ← Full portal/catalogue/KB audit
    02-departments-and-workflows.md ← Workspace analysis and workflow designs
  redesign/
    brand-profile.md          ← Trust colours, school colours, typography
    portal-design-spec.md     ← Full portal redesign specification
    workflow-leavers.md       ← Leaver workflow design document
  integration/
    sharepoint-3cx-architecture.md ← Integration options and architecture
  implementation/
    prioritised-plan.md       ← Master phase plan
    phase1-leaver-build-guide.md
    phase2-catalogue-build-guide.md
    phase3-kb-restructure-guide.md
    phase4-portal-redesign-guide.md
    phase5-onboarding-workflow-guide.md
    phase6-3cx-integration-guide.md
    phase7-sharepoint-integration-guide.md
    phase8-department-catalogues-guide.md
    handoff.md                ← This document
docs/                         ← GitHub Pages site (mirrors .planning/)
```
