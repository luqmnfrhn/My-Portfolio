# Portfolio Design — Luqman Farhan

**Date:** 2026-04-05  
**Goal:** Showcase portfolio to attract freelance clients and full-time job opportunities  
**Approach:** Minimal Light (Approach A)

---

## File Structure

```
Portfolio/
├── index.html      # Markup only — no inline styles or scripts
├── style.css       # All styles, CSS custom properties
└── script.js       # Scroll behavior, reveal animations
```

---

## Design System

### Colors

| Token         | Value     | Usage                        |
|---------------|-----------|------------------------------|
| `--bg`        | `#FAFAFA` | Page background              |
| `--surface`   | `#FFFFFF` | Cards, nav                   |
| `--border`    | `#E4E4E7` | Borders, dividers            |
| `--text`      | `#09090B` | Primary text                 |
| `--muted`     | `#71717A` | Secondary text, labels       |
| `--accent`    | `#2563EB` | CTA, links, accent elements  |
| `--accent-h`  | `#1D4ED8` | Accent hover state           |

### Typography

| Role    | Font         | Weights       |
|---------|--------------|---------------|
| Heading | Archivo      | 700, 800      |
| Body    | Space Grotesk| 400, 500      |
| Mono    | Space Grotesk| 400 (mono variant for code snippets) |

Google Fonts import:
```css
@import url('https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600;700;800&family=Space+Grotesk:wght@300;400;500;600;700&display=swap');
```

### Spacing & Layout

- Max width: `1100px`
- Section padding: `6rem 0`
- Border radius: `12px` (cards), `99px` (pills)
- Transitions: `200ms ease` for colors, `300ms ease` for transforms
- Animations: `fadeUp` on hero, `reveal` class via IntersectionObserver for all sections

---

## Sections

### 1. Nav
- Sticky, `--surface` bg, bottom border appears on scroll
- Logo: `LF.dev` — Space Grotesk mono, `--accent` color
- Links: About · Projects · Skills · Contact — uppercase, 0.75rem, tracked
- Mobile: nav links hidden, hamburger toggle

### 2. Hero
Two-column grid (1fr 1fr), collapses to single on mobile.

**Left:**
- Tag pill: `Open to work · Full Stack & Mobile` — blue border + text, mono font
- Name: `Luqman` (dark) + `Farhan.` (accent blue), clamp(3rem, 7vw, 5.5rem), weight 800
- Role: `Full Stack · DevOps · Mobile Developer`
- Stack line (mono, muted): `Flutter · Next.js · Node.js · TypeScript`
- CTAs: `View My Work →` (primary blue filled) + `Get In Touch` (ghost, border)

**Right:**
- Light code card (`--surface` bg, `--border` border)
- macOS dots header + filename `developer.ts`
- Syntax-highlighted TS object with Luqman's real name, role, location, stack

### 3. About
Two-column grid (1fr 1.3fr).

**Left:** Photo placeholder (400×500px) with accent box overlay showing years of experience.

**Right:**
- Section label + heading
- 2 paragraphs of bio (placeholder — user fills in)
- Education timeline (border-top divider per item, year in accent mono)

### 4. Projects
Header row: title left, "All on GitHub ↗" ghost button right.

**Cards:**
- 1 featured card: full-width, `#EFF6FF` bg tint, `Featured` accent tag
- 2 regular cards: white bg, border, 2-col grid
- Hover: `translateY(-4px)` + accent top bar animates `scaleX(0 → 1)`
- Footer: SVG GitHub icon link + SVG external link icon + arrow circle

### 5. Skills
Section label + heading, then 3 groups: **Frontend & Mobile**, **Backend**, **Tools & DevOps**.

Each group has a label, then an icon tile grid (auto-fill, minmax 80px).

**Tile structure:**
- White card, border, hover: border-color → accent
- SVG logo from Simple Icons (24×24)
- Name label below, 0.75rem mono

**Stack tiles:**

| Group | Technologies |
|-------|-------------|
| Frontend & Mobile | Flutter, Dart, React, Next.js, TypeScript, JavaScript |
| Backend | Node.js, PostgreSQL, Firebase, WordPress |
| Tools & DevOps | Docker, AWS, Postman, Git |

### 6. Contact
Centered layout, radial gradient bg (blue tint at bottom).

- Section label + heading: `Got a project in mind?`
- Subtext: available for freelance + full-time
- Large email link with blue underline, hover → accent color
- Social row: GitHub · LinkedIn · Download CV — SVG icons, `--muted` → accent on hover

### 7. Footer
Single line, center-aligned, mono font, muted color.
`© 2026 Luqman Farhan — Designed & built with care`

---

## Interactions & Animations

| Behavior | Implementation |
|----------|---------------|
| Nav border on scroll | `scroll` event → toggle `.scrolled` class |
| Scroll reveal | `IntersectionObserver` → toggle `.visible` on `.reveal` elements |
| Hero fade-up | CSS `@keyframes fadeUp` with staggered delays (0.1s–0.5s) |
| Project card hover | CSS transitions only — no JS |
| Skill tile hover | CSS border-color transition |
| Cursor blink in code card | CSS `@keyframes blink` |

---

## Accessibility & Quality Checklist

- [ ] All images have `alt` text
- [ ] No emojis used as icons — SVG only (Simple Icons)
- [ ] `cursor-pointer` on all interactive elements
- [ ] Color contrast 4.5:1 minimum (light theme naturally high contrast)
- [ ] Focus states visible
- [ ] `prefers-reduced-motion` respected
- [ ] Responsive at 375px, 768px, 1024px, 1440px
- [ ] No horizontal scroll on mobile

---

## Out of Scope

- Contact form (email link only)
- Blog section
- Dark mode toggle
- Animations beyond scroll-reveal and hero fadeUp
