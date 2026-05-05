# SmartSchool Project Detail Page — Design

## Project Data

| Field | Value |
|-------|-------|
| Title | SmartSchool |
| Tagline | Multi-tenant school management platform — from classroom to parents. |
| Year | 2025 |
| Type | Web + Mobile |
| Role | Team Lead & Full Stack Developer |
| Live URL | https://smartschools.my |
| GitHub | Private (client project) |
| Status | Alpha testing (May 2026) |

## Tech Stack

Flutter · Dart · Next.js · Node.js · Prisma · PostgreSQL · AWS · Firebase

## Tags

Featured · Flutter · Next.js · Node.js · AWS

## Content Copy

### Overview
SmartSchool is a multi-tenant SaaS platform built for Malaysian schools. Each school gets its own isolated subdomain. Admins and teachers manage operations via web dashboard; parents track their children via mobile app.

### The Challenge
Multi-tenancy isolation — ensuring each school's data stays completely separate while sharing one infrastructure on AWS. Building real-time notifications across web and mobile from a single backend.

### What I Built
- Multi-tenant architecture with per-school subdomain routing
- Student enrollment & attendance tracking system
- Teacher & timetable management modules
- Announcement system with Firebase push notifications (mobile)
- Admin dashboard (Next.js) + cross-platform mobile app (Flutter)
- RESTful API with Node.js + Prisma + PostgreSQL on AWS

## Page Structure

1. Nav — existing pattern (LF.dev + links)
2. Back link — ← Back to Projects
3. Header — tags + title + tagline + CTA buttons
4. Screenshot — hero image placeholder
5. Content grid — left body (Overview / Challenge / What I Built) + right sidebar (Stack + Project Info)
6. Platform section — 2 cards (Dashboard, Mobile App)
7. Footer

## CTA Buttons

- Primary: `View Live →` → https://smartschools.my
- No GitHub button (private client repo)

## Platform Cards

| Card | Name | Users | Description |
|------|------|-------|-------------|
| 1 | Dashboard | Admin & Teacher | Manage enrollment, attendance, timetable, and announcements via web |
| 2 | Mobile App | Admin, Teacher & Parent | iOS & Android app for on-the-go school management and parent monitoring |

## Visual Style

- Fonts: Archivo + Space Grotesk (match existing portfolio)
- Theme: light, minimal, flat design
- No heavy shadows or gradients
- Hover transitions: 150-200ms ease
- cursor-pointer on all clickable elements
- Responsive: 375px / 768px / 1024px / 1440px
- Contrast: 4.5:1 minimum (WCAG AA)
- Platform card icons: SVG (monitor for Dashboard, smartphone for Mobile App)
- Platform cards: 2-col desktop, stacked mobile
