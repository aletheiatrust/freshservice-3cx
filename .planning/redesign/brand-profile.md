# Aletheia Academies Trust — Brand Profile
**For use in Freshservice portal redesign**
**Extracted from:** aletheiatrust.org.uk
**Date:** 10 June 2026

---

## Trust-Level Portal Colours

The following are proposed for the unified Freshservice portal. The trust website uses a professional dark scheme with a prominent crimson accent.

| Role | Hex | Usage |
|---|---|---|
| Primary (nav / header / buttons) | `#1e4379` | Deep navy — dominant trust colour |
| Accent / CTA | `#e22a20` | Crimson red — buttons, highlights, alerts |
| Dark text | `#333333` | Body copy |
| Light background | `#f5f5f5` | Section breaks, card backgrounds |
| White | `#ffffff` | Main background |
| Hover / active | `#164698` | Darker navy for interactive states |

> **Action:** Confirm `#1e4379` as primary trust colour and `#e22a20` as accent before implementing portal theme. If brand guidelines document exists, provide it to override these values.

---

## Individual School Brand Colours

Each school has its own brand colour used on the trust website map. These could be used in future for school-specific portal elements, email templates, or department-level styling.

| School | Hex |
|---|---|
| Saint Georges C of E | `#be1823` |
| Shorne C of E | `#194420` |
| St Botolphs C of E | `#e22a20` |
| Stone St Mary's | `#18562c` |
| Horton Kirby | `#044b92` |
| Rosherville | `#4d69b1` |
| Sutton-at-Hone | `#405eab` |
| Holy Trinity | `#164698` |
| Cliffe Woods | `#31745b` |
| Halling | `#0a3322` |
| Sedleys | `#1e4379` |
| Ditton | `#0b31a8` |
| Knole Academy | `#003e7a` |
| Whitehill | `#063763` |
| Gravesend Grammar | `#194979` |
| Alkerden | `#4b6d50` |

> Note: These are the map marker fill colours from the trust website. They represent each school's individual brand identity and are not intended for use across the unified portal, but are documented here for reference.

---

## Typography

The trust website uses **Juniper Websites CMS** (school website platform). The font used on the site is likely a system/web-safe font stack. Without a brand guidelines document, recommended portal fonts are:

| Role | Font | Rationale |
|---|---|---|
| Headings | **Montserrat** (Google Fonts) | Professional, modern, educational sector widely uses it |
| Body | **Open Sans** | Clean, accessible, pairs well with Montserrat |
| Fallbacks | Helvetica, Arial, sans-serif | Safe fallback chain |

> **Action:** Confirm or override font choice. If the trust uses a specific licensed font, provide it.

---

## Logo

- **Format:** Crown and cross triangle motif with "Aletheia Academies Trust" wordmark
- **Colour:** Teal / navy on light backgrounds; white version for dark backgrounds
- **Location on Freshservice portal:** Top-left of navigation header
- **File:** Should be uploaded to Freshservice portal settings as the organisation logo
- **Source:** Available at trust systems at `aletheiatrust.org.uk/_site/images/` (Juniper CMS path pattern)

---

## Portal Design Principles

1. **Trust-first, school-aware** — The portal represents the whole trust. School colours are not used in the global UI, but school names appear in dropdowns and ticket routing.
2. **Accessibility first** — Navy `#1e4379` on white passes WCAG AA contrast (7.5:1). Crimson `#e22a20` on white passes AA for large text (4.8:1); use sparingly on small text.
3. **Department clarity** — Each of the 4 departments should have a clear visual entry point on the portal homepage, without requiring users to know which workspace to use.
4. **Self-service first** — Homepage should lead with the service catalogue and knowledge base, not a ticket submission form.
