# Mediviron Clinic Project Page — Design

**Date:** 2026-05-05
**Approach:** Minimal card matching existing portfolio style (Approach A)

## Summary

Add Mediviron Clinic as a portfolio project. Freelance Astro landing page, live at medivironclinic.com. Two changes: new detail page + update index.html project card.

## Files

### New: `mediviron.html`

Structure mirrors `smartschool.html` and `senada.html`.

- Nav (same as all pages)
- Back link → `index.html#projects`
- Project header
  - Tags: `Freelance`, `Astro`, `HTML/CSS`
  - Title: `Mediviron Clinic — Landing Page`
  - Tagline: `Modern clinic landing page for a Kuala Lumpur family clinic.`
  - CTA button: `View Live →` → `https://medivironclinic.com`
- Content sections
  - **Overview:** Freelance project. Built landing page for Clinic Mediviron Jalan Imbi, a family clinic near Bukit Bintang, KL.
  - **What I Built:** Services section, location + operating hours, WhatsApp CTA, fully responsive layout.
  - **Tech & Decisions:** Astro chosen for static output — no JS overhead, fast load, ideal for a clinic landing page that needs SEO and performance.

### Modified: `index.html`

Replace placeholder "Project Three" card (currently links to `project.html`) with:
- Tags: `Freelance`, `Astro`
- Title: `Mediviron Clinic — Landing Page`
- Description: Freelance Astro landing page for a KL family clinic. Services, location, and WhatsApp booking.
- Link → `mediviron.html`

## Out of Scope

- Screenshots/mockups (no assets available)
- New CSS — reuse existing `style.css` + `project.css`
