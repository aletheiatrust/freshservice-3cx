---
layout: default
title: Phase 4 — Portal Redesign Guide
parent: Implementation
nav_order: 4
---

# Phase 4: Portal Redesign — Build Guide
**Date:** 10 June 2026
**Status:** Ready for portal actioning

Work through each part in order. Everything here is copy-paste ready.

---

## Part A — Portal Settings

**Navigate to:** Admin → Portals → Support Portal → Settings

| Setting | Value |
|---|---|
| Portal name | Aletheia Academies Trust IT Support |
| Primary colour | `#1e4379` |
| Portal logo | Upload white/light version of Aletheia logo (PNG, transparent bg) |
| Favicon | Upload Aletheia logo icon (32×32 or 64×64 PNG) |
| Header background | Set to custom colour `#1e4379` |
| Banner / hero text | `How can we help you today?` |
| Footer text | `Aletheia Academies Trust · IT@aletheiatrust.org.uk` |

Save.

---

## Part B — Custom CSS

**Navigate to:** Admin → Portals → Support Portal → Customize Portal → CSS tab

Paste the following, replacing anything currently in the box:

```css
/* ============================================================
   ALETHEIA ACADEMIES TRUST — FRESHSERVICE PORTAL THEME
   Primary: #1e4379 (navy)  Accent: #e22a20 (crimson)
   ============================================================ */

/* --- Google Fonts --- */
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700&family=Open+Sans:wght@400;500;600&display=swap');

/* --- Base typography --- */
body, p, td, li, input, textarea, select {
  font-family: 'Open Sans', Arial, sans-serif;
  color: #333333;
}

h1, h2, h3, h4, h5, h6,
.page-title,
.portal-name {
  font-family: 'Montserrat', Arial, sans-serif;
  color: #1e4379;
}

/* --- Header --- */
.app-header,
header.app-header,
.header-wrapper {
  background-color: #1e4379 !important;
  border-bottom: 3px solid #e22a20;
}

.app-header a,
.app-header .nav-link,
.header-wrapper a {
  color: #ffffff !important;
}

.app-header a:hover,
.header-wrapper a:hover {
  color: #e8d0cf !important;
}

/* --- Hero / search banner --- */
.hero-section,
.portal-hero,
.search-section,
.home-search-section {
  background: linear-gradient(135deg, #1e4379 0%, #164698 100%);
  padding: 48px 24px;
  text-align: center;
}

.hero-section h1,
.hero-section .hero-title,
.portal-hero h1,
.home-search-section h1 {
  color: #ffffff;
  font-family: 'Montserrat', Arial, sans-serif;
  font-size: 32px;
  font-weight: 700;
  margin-bottom: 24px;
}

.search-box input,
.hero-section input[type="text"],
.portal-search input {
  border-radius: 6px;
  border: none;
  padding: 14px 20px;
  font-size: 16px;
  width: 100%;
  max-width: 620px;
  box-shadow: 0 2px 12px rgba(0,0,0,0.15);
}

/* --- Primary buttons --- */
.btn-primary,
.primary-btn,
button[type="submit"],
.submit-btn,
.request-btn {
  background-color: #1e4379 !important;
  border-color: #1e4379 !important;
  color: #ffffff !important;
  font-family: 'Open Sans', Arial, sans-serif;
  font-weight: 600;
  border-radius: 6px;
  padding: 10px 20px;
  transition: background-color 0.2s ease;
}

.btn-primary:hover,
.primary-btn:hover,
button[type="submit"]:hover {
  background-color: #164698 !important;
  border-color: #164698 !important;
}

/* --- Accent / active states --- */
.active-nav,
.nav-item.active,
.tab.active,
.badge,
.status-badge {
  background-color: #e22a20 !important;
  color: #ffffff !important;
}

a:focus,
button:focus,
input:focus,
select:focus,
textarea:focus {
  outline: 2px solid #e22a20;
  outline-offset: 2px;
}

/* --- Page background --- */
.main-content,
.portal-body,
body {
  background-color: #f5f5f5;
}

/* --- Cards (service items, tickets) --- */
.card,
.service-item-card,
.ticket-card,
.catalog-item {
  background: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  box-shadow: 0 1px 4px rgba(0,0,0,0.06);
  transition: box-shadow 0.2s ease, border-color 0.2s ease;
}

.card:hover,
.service-item-card:hover,
.catalog-item:hover {
  border-color: #1e4379;
  box-shadow: 0 4px 16px rgba(30,67,121,0.12);
}

/* --- Category headings --- */
.category-title,
.section-title {
  font-family: 'Montserrat', Arial, sans-serif;
  font-size: 18px;
  font-weight: 700;
  color: #1e4379;
  border-bottom: 2px solid #e22a20;
  padding-bottom: 8px;
  margin-bottom: 20px;
}

/* --- Knowledge base article links --- */
.article-title a,
.solution-title a {
  color: #1e4379;
  font-weight: 500;
}

.article-title a:hover,
.solution-title a:hover {
  color: #e22a20;
  text-decoration: underline;
}

/* --- Sidebar navigation --- */
.sidebar,
.left-nav,
.portal-sidebar {
  background: #ffffff;
  border-right: 1px solid #e0e0e0;
}

.sidebar a,
.left-nav a {
  color: #333333;
}

.sidebar a:hover,
.sidebar a.active,
.left-nav a:hover {
  color: #1e4379;
  background-color: #eef2f9;
  border-left: 3px solid #1e4379;
}

/* --- Ticket status colours --- */
.status-open { color: #1e4379; }
.status-resolved { color: #18562c; }
.status-pending { color: #e8a000; }

/* --- Footer --- */
.portal-footer,
footer {
  background-color: #1e4379;
  color: #ffffff;
  font-size: 13px;
  padding: 16px 24px;
  text-align: center;
}

.portal-footer a {
  color: #e8d0cf;
}

/* --- Responsive --- */
@media (max-width: 767px) {
  .hero-section h1,
  .portal-hero h1 {
    font-size: 24px;
  }

  .quick-tiles-grid {
    grid-template-columns: repeat(2, 1fr) !important;
  }

  .dept-cards-grid {
    grid-template-columns: 1fr !important;
  }
}

@media (min-width: 768px) and (max-width: 1023px) {
  .quick-tiles-grid {
    grid-template-columns: repeat(3, 1fr) !important;
  }
}

/* --- Quick-access tiles (custom HTML section) --- */
.quick-tiles-section {
  background: #ffffff;
  padding: 36px 24px;
  border-bottom: 1px solid #e0e0e0;
}

.quick-tiles-section h2 {
  font-family: 'Montserrat', Arial, sans-serif;
  font-size: 16px;
  font-weight: 700;
  color: #666666;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 24px;
}

.quick-tiles-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 16px;
  max-width: 900px;
  margin: 0 auto;
}

.quick-tile {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 24px 12px;
  background: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  text-decoration: none;
  color: #333333;
  font-family: 'Open Sans', Arial, sans-serif;
  font-size: 13px;
  font-weight: 600;
  text-align: center;
  transition: all 0.2s ease;
  cursor: pointer;
}

.quick-tile:hover {
  border-color: #e22a20;
  box-shadow: 0 4px 16px rgba(226,42,32,0.12);
  color: #1e4379;
  text-decoration: none;
}

.quick-tile .tile-icon {
  font-size: 28px;
  margin-bottom: 10px;
  display: block;
}

/* --- Department cards (custom HTML section) --- */
.dept-cards-section {
  background: #f5f5f5;
  padding: 36px 24px;
  border-bottom: 1px solid #e0e0e0;
}

.dept-cards-section h2 {
  font-family: 'Montserrat', Arial, sans-serif;
  font-size: 16px;
  font-weight: 700;
  color: #666666;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  margin-bottom: 24px;
}

.dept-cards-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  max-width: 900px;
  margin: 0 auto;
}

.dept-card {
  background: #ffffff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 24px;
  text-decoration: none;
  color: #333333;
  display: flex;
  flex-direction: column;
  box-shadow: 0 1px 4px rgba(0,0,0,0.06);
  transition: all 0.2s ease;
}

.dept-card:hover {
  border-color: #1e4379;
  box-shadow: 0 4px 16px rgba(30,67,121,0.12);
  text-decoration: none;
}

.dept-card .dept-icon {
  font-size: 28px;
  margin-bottom: 10px;
}

.dept-card .dept-name {
  font-family: 'Montserrat', Arial, sans-serif;
  font-size: 16px;
  font-weight: 700;
  color: #1e4379;
  margin-bottom: 6px;
}

.dept-card .dept-desc {
  font-size: 13px;
  color: #666666;
  flex-grow: 1;
  margin-bottom: 16px;
}

.dept-card .dept-link {
  font-size: 13px;
  font-weight: 600;
  color: #1e4379;
}

.dept-card:hover .dept-link {
  color: #e22a20;
}

/* --- 3CX Live Chat widget button override --- */
#livechat-button,
.livechat-launcher {
  background-color: #1e4379 !important;
  border-color: #1e4379 !important;
}
```

Save.

---

## Part C — Homepage Custom HTML

**Navigate to:** Admin → Portals → Support Portal → Customize Portal → Homepage

Add the following HTML blocks as custom sections. The portal editor may have a "Custom HTML" widget or section — paste each block in order below the default search hero.

### Block 1 — Quick Access Tiles

> **Before pasting:** Replace each `ITEM_ID` placeholder with the actual service item display_id from Freshservice. These are available in the URL when you open each service item in the portal (e.g. `/support/catalog/items/42`). The IDs for Phase 1 and 2 items will be available after those portal steps are completed.

```html
<div class="quick-tiles-section">
  <div style="max-width:900px; margin:0 auto;">
    <h2>COMMON REQUESTS</h2>
    <div class="quick-tiles-grid">

      <a class="quick-tile" href="/support/catalog/items/ITEM_ID_PASSWORD_RESET">
        <span class="tile-icon">🔑</span>
        Password Reset
      </a>

      <a class="quick-tile" href="/support/catalog/items/ITEM_ID_NEW_STAFF">
        <span class="tile-icon">👤</span>
        New Staff Account
      </a>

      <a class="quick-tile" href="/support/catalog/items/ITEM_ID_STAFF_LEAVER">
        <span class="tile-icon">👋</span>
        Staff Leaver
      </a>

      <a class="quick-tile" href="/support/catalog/items/ITEM_ID_PRINTING">
        <span class="tile-icon">🖨️</span>
        Printing Credit
      </a>

      <a class="quick-tile" href="/support/catalog/items/40">
        <span class="tile-icon">🪪</span>
        ID Card Request
      </a>

      <a class="quick-tile" href="/support/catalog/items/ITEM_ID_EMAIL_GROUP">
        <span class="tile-icon">📧</span>
        Email Groups
      </a>

    </div>
  </div>
</div>
```

**Known item display_ids (confirmed via API):**
| Item | Display ID | Status |
|---|---|---|
| Staff ID Card | 40 | ✅ Ready |
| Password Reset / Account Locked | TBC | ⏳ Create in Phase 2 portal steps |
| New User Account Request | TBC | ⏳ Create in Phase 2 portal steps |
| Staff Leaver | TBC | ⏳ Create in Phase 1 portal steps |
| Printing Credit Request | TBC | ⏳ Create in Phase 2 portal steps |
| New Email Distribution Group | TBC | ⏳ Create in Phase 2 portal steps |

---

### Block 2 — Department Cards

```html
<div class="dept-cards-section">
  <div style="max-width:900px; margin:0 auto;">
    <h2>SUPPORT DEPARTMENTS</h2>
    <div class="dept-cards-grid">

      <a class="dept-card" href="/support/catalog">
        <span class="dept-icon">💻</span>
        <div class="dept-name">IT Support</div>
        <div class="dept-desc">Accounts, devices, systems &amp; access</div>
        <span class="dept-link">Browse services →</span>
      </a>

      <a class="dept-card" href="/support/catalog">
        <span class="dept-icon">👥</span>
        <div class="dept-name">People &amp; Culture</div>
        <div class="dept-desc">HR, onboarding, contracts &amp; pay</div>
        <span class="dept-link">Browse services →</span>
      </a>

      <a class="dept-card" href="/support/catalog">
        <span class="dept-icon">💰</span>
        <div class="dept-name">Finance</div>
        <div class="dept-desc">Budgets, claims &amp; payroll queries</div>
        <span class="dept-link">Browse services →</span>
      </a>

      <a class="dept-card" href="/support/catalog">
        <span class="dept-icon">📢</span>
        <div class="dept-name">Marketing &amp; Comms</div>
        <div class="dept-desc">Communications, media &amp; content</div>
        <span class="dept-link">Browse services →</span>
      </a>

    </div>
  </div>
</div>
```

> **Note:** The `href` values above link to the general catalogue. Once each workspace has a direct URL in Freshservice, update each card's `href` to point directly to that workspace's catalogue page.

---

### Block 3 — 3CX Live Chat Widget

> ⏳ This block is added during Phase 6. Placeholder noted here for completeness.

```html
<!-- 3CX Live Chat Widget — added in Phase 6 -->
<!-- Hours: 08:00–16:30, term time -->
<!-- Script provided by 3CX admin panel once configured -->
```

---

## Part D — Featured Knowledge Articles

**Navigate to:** Admin → Portals → Support Portal → Featured Solutions

Set the following 5 articles as featured (these will appear on the homepage knowledge highlights section):

1. How to reset your password
2. Setting up Microsoft Authenticator
3. Connecting to the school Wi-Fi
4. Arbor — logging in and getting started
5. How to request a Google Classroom

> If any of these articles don't exist yet, create them as brief guides in the relevant KB category first. Password reset and Authenticator setup in particular should be priority articles to write.

---

## Part E — After Phase 1 & 2 Portal Steps: Update Tile Links

Once Phase 1 (Staff Leaver form) and Phase 2 (Password Reset, New Account, Printing Credit, Email Group items) have been created in the portal, return to the homepage HTML in Part C and replace each `ITEM_ID_*` placeholder with the actual display_id from the URL of each service item.

To find a display_id: open the service item in the portal → the number at the end of the URL is the display_id (e.g. `/support/catalog/items/42` → display_id is `42`).

---

## Summary

| Part | Action | Status |
|---|---|---|
| A — Portal settings | Colour, logo, banner text, footer | ⏳ Portal |
| B — Custom CSS | Full brand CSS | ⏳ Portal |
| C — Homepage HTML | Quick-access tiles + department cards | ⏳ Portal |
| D — Featured articles | 5 knowledge highlights | ⏳ Portal |
| E — Update tile links | After Phase 1 & 2 portal steps complete | ⏳ After Phase 1+2 |
| 3CX widget | Live chat button | ⏳ Phase 6 |
