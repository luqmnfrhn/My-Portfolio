# SmartSchool Project Detail Page — Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build `smartschool.html` — a project detail page for SmartSchool, a multi-tenant school management SaaS, following the existing portfolio pattern (senada.html) with an added Platform section.

**Architecture:** Clone senada.html structure exactly, fill in real project data, add a 2-card Platform section below the content grid. Add CSS for the Platform section to project.css. No new JS needed.

**Tech Stack:** Vanilla HTML, existing style.css + project.css, devicons CDN, Google Fonts (Archivo + Space Grotesk — already loaded via style.css).

---

### Task 1: Build smartschool.html — full page HTML

**Files:**
- Modify: `smartschool.html` (currently empty)
- Reference: `senada.html` (pattern source)
- Reference: `project.css` (existing styles)

**Step 1: Write the HTML**

Replace the empty `smartschool.html` with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>SmartSchool — Luqman Farhan</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600;700;800&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/devicon.min.css" />
  <link rel="stylesheet" href="style.css" />
  <link rel="stylesheet" href="project.css" />
</head>
<body>

  <!-- ── NAV ──────────────────────────────────────────── -->
  <nav id="navbar">
    <div class="inner">
      <a href="index.html" class="nav-logo">LF.dev</a>
      <ul class="nav-links">
        <li><a href="index.html#about">About</a></li>
        <li><a href="index.html#projects">Projects</a></li>
        <li><a href="index.html#skills">Skills</a></li>
        <li><a href="index.html#contact">Contact</a></li>
      </ul>
    </div>
  </nav>

  <!-- ── PROJECT DETAIL ───────────────────────────────── -->
  <main class="project-detail">
    <div class="container">

      <!-- Back link -->
      <a href="index.html#projects" class="back-link">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <path d="M19 12H5M12 5l-7 7 7 7"/>
        </svg>
        Back to Projects
      </a>

      <!-- Header -->
      <div class="project-header reveal">
        <div class="project-header-meta">
          <div class="project-tags">
            <span class="tag accent">Featured</span>
            <span class="tag">Flutter</span>
            <span class="tag">Next.js</span>
            <span class="tag">Node.js</span>
            <span class="tag">AWS</span>
          </div>
          <h1 class="project-detail-title">SmartSchool</h1>
          <p class="project-tagline">Multi-tenant school management platform — from classroom to parents.</p>
        </div>

        <!-- CTA buttons -->
        <div class="project-header-cta">
          <a href="https://smartschools.my" target="_blank" rel="noopener" class="btn btn-primary">
            View Live →
          </a>
        </div>
      </div>

      <!-- Screenshot -->
      <div class="project-screenshot reveal">
        <img src="projects/smartschool/screenshot.png" alt="SmartSchool dashboard screenshot" class="screenshot-img" />
      </div>

      <!-- Content grid: description left, details right -->
      <div class="project-content reveal">

        <!-- Left: description -->
        <div class="project-body">
          <h2 class="content-heading">Overview</h2>
          <p>SmartSchool is a multi-tenant SaaS platform built for Malaysian schools. Each school gets its own isolated subdomain. Admins and teachers manage daily operations via a web dashboard, while parents monitor their children through a dedicated mobile app on iOS and Android.</p>

          <h2 class="content-heading">The Challenge</h2>
          <p>Enforcing strict multi-tenancy isolation — keeping each school's data completely separate while running on shared AWS infrastructure. Layered on top of that: building a unified real-time notification pipeline that reaches both web and mobile from a single backend service.</p>

          <h2 class="content-heading">What I Built</h2>
          <ul class="feature-list">
            <li>Multi-tenant architecture with per-school subdomain routing</li>
            <li>Student enrollment and attendance tracking system</li>
            <li>Teacher and timetable management modules</li>
            <li>Announcement system with Firebase push notifications for mobile</li>
            <li>Admin dashboard built with Next.js and cross-platform mobile app in Flutter</li>
            <li>RESTful API with Node.js, Prisma ORM, and PostgreSQL deployed on AWS</li>
          </ul>
        </div>

        <!-- Right: project details sidebar -->
        <aside class="project-sidebar">

          <div class="sidebar-card">
            <div class="sidebar-label">Tech Stack</div>
            <div class="stack-tiles">
              <div class="stack-tile">
                <i class="devicon-flutter-plain colored"></i>
                <span>Flutter</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-dart-plain colored"></i>
                <span>Dart</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-nextjs-plain"></i>
                <span>Next.js</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-nodejs-plain colored"></i>
                <span>Node.js</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-postgresql-plain colored"></i>
                <span>PostgreSQL</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-amazonwebservices-plain-wordmark colored"></i>
                <span>AWS</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-firebase-plain colored"></i>
                <span>Firebase</span>
              </div>
            </div>
          </div>

          <div class="sidebar-card">
            <div class="sidebar-label">Project Info</div>
            <div class="info-list">
              <div class="info-item">
                <span class="info-key">Year</span>
                <span class="info-val">2025</span>
              </div>
              <div class="info-item">
                <span class="info-key">Type</span>
                <span class="info-val">Web + Mobile</span>
              </div>
              <div class="info-item">
                <span class="info-key">Role</span>
                <span class="info-val">Team Lead & Full Stack Developer</span>
              </div>
              <div class="info-item">
                <span class="info-key">Live</span>
                <a href="https://smartschools.my" target="_blank" rel="noopener" class="info-link">View →</a>
              </div>
            </div>
          </div>

        </aside>
      </div>

      <!-- Platform section -->
      <div class="platform-section reveal">
        <h2 class="platform-heading">Platform</h2>
        <div class="platform-grid">

          <div class="platform-card">
            <div class="platform-icon" aria-hidden="true">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <rect x="2" y="3" width="20" height="14" rx="2"/>
                <path d="M8 21h8M12 17v4"/>
              </svg>
            </div>
            <div class="platform-card-body">
              <div class="platform-name">Dashboard</div>
              <div class="platform-users">Admin &amp; Teacher</div>
              <p class="platform-desc">Manage enrollment, attendance, timetable, and announcements via web browser.</p>
            </div>
          </div>

          <div class="platform-card">
            <div class="platform-icon" aria-hidden="true">
              <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
                <rect x="5" y="2" width="14" height="20" rx="2"/>
                <path d="M12 18h.01"/>
              </svg>
            </div>
            <div class="platform-card-body">
              <div class="platform-name">Mobile App</div>
              <div class="platform-users">Admin, Teacher &amp; Parent</div>
              <p class="platform-desc">iOS &amp; Android app for on-the-go school management and parent monitoring.</p>
            </div>
          </div>

        </div>
      </div>

    </div>
  </main>

  <!-- ── FOOTER ────────────────────────────────────────── -->
  <footer>
    <div class="container">
      <p>© 2026 Luqman Farhan — Designed &amp; built with care</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

**Step 2: Verify file saved correctly**

Open `smartschool.html` in browser. Confirm nav, back link, header, tags, screenshot placeholder, content grid, sidebar, platform cards, and footer all render.

**Step 3: Commit**

```bash
git add smartschool.html
git commit -m "feat: add SmartSchool project detail page HTML"
```

---

### Task 2: Add Platform section CSS to project.css

**Files:**
- Modify: `project.css` (append to end of file)

**Step 1: Append CSS**

Add to the end of `project.css`:

```css
/* ── Platform section ───────────────────────────────── */
.platform-section {
  margin-top: 4rem;
  padding-top: 3rem;
  border-top: 1px solid var(--border);
}
.platform-heading {
  font-family: var(--font-head);
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 1.5rem;
}
.platform-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.25rem;
}
.platform-card {
  display: flex;
  gap: 1rem;
  align-items: flex-start;
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  padding: 1.5rem;
  transition: border-color .2s ease;
  cursor: default;
}
.platform-card:hover {
  border-color: var(--accent);
}
.platform-icon {
  flex-shrink: 0;
  color: var(--accent);
  margin-top: .1rem;
}
.platform-name {
  font-family: var(--font-head);
  font-size: 1rem;
  font-weight: 700;
  color: var(--text);
  margin-bottom: .2rem;
}
.platform-users {
  font-size: .7rem;
  font-weight: 600;
  letter-spacing: .1em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: .6rem;
}
.platform-desc {
  font-size: .875rem;
  color: var(--muted);
  line-height: 1.7;
  margin: 0;
}

@media (max-width: 640px) {
  .platform-grid {
    grid-template-columns: 1fr;
  }
}
```

**Step 2: Verify visually**

Check platform cards at 375px (mobile stacked), 768px (still 1-col or check), 1024px+ (2-col side by side). Confirm hover border-color transition works.

**Step 3: Commit**

```bash
git add project.css
git commit -m "feat: add platform section styles to project.css"
```

---

### Task 3: Add screenshot placeholder image directory

**Files:**
- Create directory: `projects/smartschool/`
- The `screenshot.png` will be added manually later — just create the folder so the `<img>` doesn't 404-break layout (aspect-ratio CSS handles the empty state gracefully anyway).

**Step 1: Create directory**

```bash
mkdir -p "projects/smartschool"
```

**Step 2: Verify screenshot placeholder renders gracefully**

With no image, the `.project-screenshot` div should show as a grey box (via `background: var(--surface2)` and `aspect-ratio: 16/9`). Confirm no layout break.

**Step 3: Commit**

```bash
git add projects/smartschool
git commit -m "chore: add smartschool screenshot directory"
```

---

### Task 4: Wire up smartschool.html in index.html projects section

**Files:**
- Modify: `index.html` — find the projects section and add/update SmartSchool card to link to `smartschool.html`

**Step 1: Locate the projects section**

Search `index.html` for `id="projects"` and find where project cards are listed.

**Step 2: Add or update SmartSchool project card**

If a SmartSchool card exists but links to `#`, update `href` to `smartschool.html`.
If no card exists, add one matching the existing card pattern with title "SmartSchool", tags (Flutter, Next.js, Node.js, AWS), and link `smartschool.html`.

**Step 3: Verify**

Click SmartSchool card on homepage — confirm it navigates to `smartschool.html` correctly.

**Step 4: Commit**

```bash
git add index.html
git commit -m "feat: link SmartSchool card to project detail page"
```
