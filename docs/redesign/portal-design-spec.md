---
layout: default
title: "Portal Design Specification"
parent: "Design & Architecture"
nav_order: 2
---


# Freshservice Portal Redesign — Design Specification
**Aletheia Academies Trust**
**Date:** 10 June 2026
**Status:** DRAFT — Awaiting Approval

---

## Design Philosophy

The current portal is underused. Staff default to email because the portal offers no obvious advantage. The redesign must answer one question for every user who lands on it: **"Can I solve this myself in under 60 seconds?"**

Three principles drive every decision:

1. **Search first** — A prominent search bar that covers both knowledge articles and service requests reduces friction for the most common use case (finding an answer).
2. **Tiles over menus** — Popular requests must be one click away. No one browses a service catalogue if they can't see what they need in 3 seconds.
3. **Department clarity without complexity** — Staff need to know they've come to the right place for IT, HR, Finance and Comms — but they shouldn't have to understand the internal structure to get help.

---

## Portal Colour Scheme

| Element | Value |
|---|---|
| Header / navigation background | `#1e4379` (deep navy) |
| Header text and logo | `#ffffff` |
| Primary buttons | `#1e4379` with white text |
| Primary button hover | `#164698` |
| Accent / highlight | `#e22a20` (crimson) |
| Active nav item / badge | `#e22a20` |
| Card background | `#ffffff` |
| Page background | `#f5f5f5` |
| Body text | `#333333` |
| Secondary text / labels | `#666666` |
| Card border | `#e0e0e0` |
| Success | `#18562c` |
| Warning | `#e8a000` |
| Error | `#e22a20` |

---

## Homepage Layout

```
┌─────────────────────────────────────────────────────────┐
│  [ALETHEIA LOGO]          My Tickets   Knowledge   [👤]  │  ← Navy header #1e4379
├─────────────────────────────────────────────────────────┤
│                                                         │
│         How can we help you today?                      │  ← Hero section, navy/white
│  ┌─────────────────────────────────────────────────┐   │
│  │ 🔍  Search for help, articles or requests...    │   │  ← Large search bar
│  └─────────────────────────────────────────────────┘   │
│                                                         │
├─────────────────────────────────────────────────────────┤
│  COMMON REQUESTS                                        │  ← Quick-access tiles, white bg
│                                                         │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐  │
│  │ 🔑       │ │ 👤       │ │ 👋       │ │ 🖨️       │  │
│  │ Password │ │  New     │ │  Staff   │ │ Printing │  │
│  │  Reset   │ │  Staff   │ │  Leaver  │ │  Credit  │  │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘  │
│                                                         │
│  ┌──────────┐ ┌──────────┐                             │
│  │ 🪪       │ │ 📧       │                             │
│  │  ID Card │ │  Email   │                             │
│  │ Request  │ │  Groups  │                             │
│  └──────────┘ └──────────┘                             │
│                                                         │
├─────────────────────────────────────────────────────────┤
│  SUPPORT DEPARTMENTS                                    │  ← Department cards, light grey bg
│                                                         │
│  ┌─────────────────┐  ┌─────────────────┐              │
│  │ 💻 IT Support   │  │ 👥 People &     │              │
│  │                 │  │    Culture      │              │
│  │ Accounts, devices│  │ HR, onboarding, │             │
│  │ systems & access│  │ contracts & pay │              │
│  │                 │  │                 │              │
│  │ [Browse →]      │  │ [Browse →]      │              │
│  └─────────────────┘  └─────────────────┘              │
│                                                         │
│  ┌─────────────────┐  ┌─────────────────┐              │
│  │ 💰 Finance      │  │ 📢 Marketing &  │              │
│  │                 │  │    Comms        │              │
│  │ Budgets, claims,│  │ Communications, │              │
│  │ payroll queries │  │ media & content │              │
│  │                 │  │                 │              │
│  │ [Browse →]      │  │ [Browse →]      │              │
│  └─────────────────┘  └─────────────────┘              │
│                                                         │
├─────────────────────────────────────────────────────────┤
│  KNOWLEDGE BASE — POPULAR ARTICLES                      │  ← Knowledge highlights
│                                                         │
│  📄 How to reset your password                         │
│  📄 Setting up Microsoft Authenticator                  │
│  📄 Connecting to the school Wi-Fi                      │
│  📄 Arbor — logging in and getting started              │
│  📄 How to request a Google Classroom                   │
│                                                         │
│                          [Browse all articles →]        │
│                                                         │
├─────────────────────────────────────────────────────────┤
│  Footer: Aletheia Academies Trust · IT@aletheiatrust.org.uk  │
└─────────────────────────────────────────────────────────┘
                                          [💬 Live Chat]  ← Floating, bottom-right
```

---

## Page-by-Page Spec

### Header (all pages)
- Background: `#1e4379`
- Logo: Aletheia Academies Trust (white version), left-aligned
- Navigation links: My Tickets | Knowledge Base | [User avatar/name]
- No hamburger menu on desktop — keep it flat
- Mobile: logo + hamburger → slides in same nav items

### Hero Section
- Background: gradient `#1e4379` → `#164698` (subtle, not garish)
- Heading: "How can we help you today?" — white, Montserrat, 32px
- Search bar: white, full-width on mobile, 60% on desktop, with magnifier icon
- Search searches: service catalogue items + knowledge base articles simultaneously
- Below search (small text, light): "Or browse by department below"

### Common Requests
- 6 tiles in a 4+2 or 3+3 grid (responsive)
- Each tile: icon (emoji or icon font), request name, no description
- Single click → opens the service request form directly
- Tiles are curated — not auto-generated from catalogue
- Order by: most commonly submitted (review after 30 days and reorder)
- Crimson `#e22a20` accent on hover border

**Initial 6 tiles:**
1. Password Reset / Account Locked
2. New Staff Member
3. Staff Leaver
4. Printing Credit
5. ID Card Request
6. Email Group / Distribution List

### Department Cards
- 4 cards in a 2×2 grid
- Each: icon + department name + 1-line description + "Browse services →" link
- Card background: white, subtle shadow, `#e0e0e0` border
- Hover: navy border `#1e4379`, slight lift (box-shadow)
- Click → department's service catalogue page

### Knowledge Highlights
- 5 most-viewed articles surfaced on homepage (manually curated initially)
- Displayed as a simple list with document icon
- "Browse all articles →" link at bottom

### Live Chat Widget
- Floating button, bottom-right, persistent across all pages
- Label: "IT Support Chat"
- Badge shows: "Online" (green) / "Offline — leave a message" (grey) based on business hours
- Opens 3CX live chat panel (see integration spec)
- Available during school hours only (configure via 3CX schedule)

---

## Mobile Responsiveness

| Breakpoint | Layout change |
|---|---|
| < 768px (mobile) | Single column. Tiles: 2×3 grid. Dept cards: stacked. |
| 768–1024px (tablet) | Tiles: 3+3. Dept cards: 2×2. |
| > 1024px (desktop) | Full layout as above. |

---

## Accessibility

- All colour combinations meet WCAG 2.1 AA minimum
- Navy `#1e4379` on white: contrast ratio 7.5:1 ✓
- Crimson `#e22a20` on white: 4.8:1 ✓ (large text / UI components)
- All interactive elements have visible focus states
- Search bar has visible label (screen reader accessible)
- Tile icons have `aria-label` text
- Live chat button has clear text label, not icon-only

---

## What Changes From Current Portal

| Current | Proposed |
|---|---|
| Default Freshservice layout | Custom branded layout with trust colours |
| Service catalogue browsing only | Search bar + quick-access tiles + catalogue |
| IT workspace only visible on landing | All 4 departments visible from homepage |
| No featured knowledge articles | 5 curated articles on homepage |
| No live chat entry point | Persistent 3CX chat widget |
| No department descriptions | Each department has a plain-English description |

---

## Implementation Notes

The Freshservice portal can be customised via:
- **Portal settings** → primary colour, logo, banner text
- **Custom CSS** → deeper visual overrides (card styles, typography, tile grid)
- **Custom HTML** → homepage sections (quick-access tiles, department cards)
- **Featured articles** → curated in knowledge base settings

The live chat widget is added via a JavaScript snippet in the portal's custom HTML/footer section.

The department card layout requires custom HTML in the portal homepage template.

---

## Approval Checklist

Before implementing any portal changes:
- [ ] Colour scheme approved (navy `#1e4379` + crimson `#e22a20`)
- [ ] Font confirmed (Montserrat + Open Sans, or override)
- [ ] 6 quick-access tiles confirmed or adjusted
- [ ] Department card descriptions approved
- [ ] Knowledge base articles to feature on homepage agreed
- [ ] Live chat hours confirmed (school hours only? extended hours for IT?)
