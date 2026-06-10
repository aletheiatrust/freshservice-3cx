---
layout: default
title: Phase 3 — KB Restructure Guide
parent: Implementation
nav_order: 3
---

# Phase 3: Knowledge Base Restructure — Build Guide
**Date:** 10 June 2026
**Status:** Ready for portal actioning

---

## Current KB State (confirmed via API — 16 categories, 80 folders)

| Category | ID | Folders | Notes |
|---|---|---|---|
| Default Category | 53000012530 | Drafts | System default — leave alone |
| Apple | 53000021745 | MacOS-Internal(agents), iPads-Internal(agents), iPads, iOS | Mixed visibility |
| Arbor | 53000019645 | General, Attendance, Behaviour, Clubs, Communication, Custom Report Writer, Enrolment, Exams, Meals, Payments, Parent Portal, Staff Profile, Student Profile, Trips, Arbor Internal(agents) | Well populated |
| eSafety, Policies & Security | 53000012531 | Bitlocker, eSafety, GDPR, IT policies, eSafety Internal(agents) | Good — already fixed typo |
| Google | 53000019647 | Chromebooks, Classroom, Docs, Google Meet, Google-Internal(agents) | Good |
| Fusion | 53000021384 | Fusion app, Impact Back Office(logged-in) | Catering system |
| Microsoft Surface | 53000021671 | Hardware Troubleshooting(agents), iPads-Internal(agents), iOS | Overlaps with Hardware |
| Hardware | 53000021555 | Hardware-Internal(agents), General, Android | Agents-only internal folder |
| Interactive Boards | 53000021272 | BenQ, General, Vision, Interactive Board-Internal(agents), Promethean | Good |
| Microsoft Office | 53000019648 | General, Office 365, Access, Excel, Forms, OneDrive, One Note, Outlook, Powerpoint, Sharepoint, Teams, Microsoft Office Internal(agents) | Should be renamed Microsoft 365 |
| Phone System | 53000019646 | Handset Guides, Web & Mobile Clients | 3CX — relevant to Phase 6 |
| Photocopiers & Printers | 53000021335 | Papercut, Photocopiers-Internal(agents), Printing General | Good |
| Pupil Progress | 53000021960 | General(agents-only) | Agents-only — already hidden from staff |
| School Cloud | 53000021375 | Parents evening | Parents evening booking system |
| Sign In App | 53000021268 | Admin Portal, iPad & Printers, Mobile App | Visitor/contractor sign-in |
| Software | 53000019650 | AB Tutor V10, Adobe, Boost Insight, Cloud Drive Mapper, General, GL Assessment, Instashare, Internet Filtering, Lets View, Lynx, Microsoft Edge, My Concern, Remote Desktop, VLC Player, Windows, Windows Media Player, Zoom, Software-Internal(agents) | Very large — needs splitting |

**Visibility key:** vis:1 = all users / vis:2 = logged-in / vis:3 = agents-only / vis:5 = agents-only (alternate)

---

## Part A — Rename Categories (API-possible)

### A1 — Rename "Microsoft Office" → "Microsoft 365"

This can be done via API.

**API call** (already scripted — action below):
```
PUT /api/v2/solutions/categories/53000019648
{ "solution_category": { "name": "Microsoft 365" } }
```

✅ Done via API — see implementation log.

---

## Part B — New Categories to Create

**Navigate to:** Admin → Solutions → + New Category

### B1 — Microsoft Teams

Teams has grown significantly and currently sits as a single folder inside Microsoft 365. It deserves its own top-level category, especially given the Phase 6 3CX integration.

| Field | Value |
|---|---|
| Name | Microsoft Teams |
| Description | Guides for Microsoft Teams — meetings, channels, classes, and collaboration |
| Visibility | All Users |

After creating, move the **Teams** folder (currently in Microsoft 365) into this new category.

---

### B2 — People & Culture (HR)

No HR knowledge base exists. People & Culture workspace is active and staff will benefit from self-service HR guides (absence process, payroll queries, policies).

| Field | Value |
|---|---|
| Name | People & Culture |
| Description | HR guides, policies, and processes for staff |
| Visibility | All Users |

Seed with one initial folder: **Policies & Processes** — add HR team as contributors once category is created.

---

### B3 — Finance

No Finance knowledge base exists. Finance workspace is active.

| Field | Value |
|---|---|
| Name | Finance |
| Description | Finance guides and processes |
| Visibility | Logged-in users |

Seed with one initial folder: **General** — Finance team to populate.

---

### B4 — Marketing & Communications

No Marketing KB exists. Workspace is active.

| Field | Value |
|---|---|
| Name | Marketing & Communications |
| Description | Brand guidelines, communications templates, and media guidance |
| Visibility | Logged-in users |

Seed with one initial folder: **Brand & Templates** — Marketing team to populate.

---

## Part C — Restructure the Software Category

The **Software** category has 18 folders covering everything from Adobe to Zoom. This makes it hard to navigate. Split the most-used items into their own categories where they warrant it, and tidy the remainder.

### C1 — Move Zoom to its own folder under Microsoft Teams or leave under Software?

Zoom usage has likely declined since Teams became the primary platform. **Recommended:** leave under Software but consider archiving if articles are outdated.

### C2 — Split off "Internet Filtering" 

Internet filtering (Smoothwall / content filtering) is more naturally grouped under **eSafety, Policies & Security** than Software. Move the Internet Filtering folder there.

**Navigate to:** Admin → Solutions → Software → Internet Filtering folder → Edit → Change category to eSafety, Policies & Security.

### C3 — Split off "Remote Desktop"

Remote desktop access is an IT access/security topic. Move to **eSafety, Policies & Security** or create a new **Remote Access** folder within that category.

### C4 — Rename "Software" → "Applications & Software"

Makes the category purpose clearer.

---

## Part D — Address Microsoft Surface / Hardware Overlap

**Microsoft Surface** and **Hardware** are separate categories but clearly overlap. Microsoft Surface is essentially a subset of hardware.

**Recommended:** Merge Microsoft Surface into Hardware.

- Move all Surface folders (MacOS-Internal, iPads-Internal, iPads, iOS) into the Hardware category
- Delete the empty Microsoft Surface category
- The Hardware category becomes the home for all physical device guides

**Navigate to:** Admin → Solutions → each folder in Microsoft Surface → Edit → Change category to Hardware.

---

## Part E — Portal Actions Summary

All of the following require the Freshservice admin portal (category/folder moves cannot be done via the standard API):

| # | Action | Where |
|---|---|---|
| E1 | Rename "Microsoft Office" → "Microsoft 365" | Admin → Solutions → Microsoft Office → Edit |
| E2 | Create Microsoft Teams category | Admin → Solutions → + New Category |
| E3 | Move Teams folder from Microsoft 365 → new Microsoft Teams category | Admin → Solutions → Microsoft 365 → Teams → Edit |
| E4 | Create People & Culture category + General folder | Admin → Solutions → + New Category |
| E5 | Create Finance category + General folder | Admin → Solutions → + New Category |
| E6 | Create Marketing & Communications category + Brand & Templates folder | Admin → Solutions → + New Category |
| E7 | Move Internet Filtering folder → eSafety, Policies & Security | Admin → Solutions → Software → Internet Filtering → Edit |
| E8 | Move Remote Desktop folder → eSafety, Policies & Security | Admin → Solutions → Software → Remote Desktop → Edit |
| E9 | Move all Microsoft Surface folders → Hardware | Admin → Solutions → Microsoft Surface → each folder → Edit |
| E10 | Delete empty Microsoft Surface category | Admin → Solutions → Microsoft Surface → Delete (once empty) |
| E11 | Rename "Software" → "Applications & Software" | Admin → Solutions → Software → Edit |

---

## Part F — Pupil Progress

Already set to agents-only visibility (done in Phase 0). No further action needed unless the system is being decommissioned, in which case archive the category entirely.

**Question for later:** Is Pupil Progress (the assessment system) still in use at any school?

---

## Part G — Phone System Category

Currently contains 3CX handset guides and web/mobile client guides. This category will become more important in Phase 6 (3CX live chat integration). Leave as-is for now — revisit in Phase 6 to add live chat guides.

---

## Summary

| Part | Actions | Status |
|---|---|---|
| A — Rename Microsoft Office → Microsoft 365 | 1 rename | ⏳ Portal |
| B — New categories | 4 new categories (Teams, HR, Finance, Marketing) | ⏳ Portal |
| C — Software restructure | Move 2 folders, rename category | ⏳ Portal |
| D — Surface/Hardware merge | Move 4 folders, delete empty category | ⏳ Portal |
| E — Portal steps | 11 actions listed in order | ⏳ Portal |
| F — Pupil Progress | Already done | ✅ Complete |
| G — Phone System | Leave for Phase 6 | ⏳ Phase 6 |
