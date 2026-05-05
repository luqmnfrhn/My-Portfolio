# Mediviron Clinic Project Page Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add Mediviron Clinic as a portfolio project — new detail page `mediviron.html` + update `index.html` project card.

**Architecture:** Static HTML page mirroring existing `smartschool.html` structure. Reuses `style.css` and `project.css` — no new CSS needed. Replace placeholder "Project Three" card in `index.html` with Mediviron card.

**Tech Stack:** Plain HTML, existing CSS (`style.css`, `project.css`), devicons for stack tiles.

---

### Task 1: Create `mediviron.html`

**Files:**
- Create: `mediviron.html`
- Reference: `smartschool.html` (copy structure from this file)

**Step 1: Create the file**

Create `/Users/luqmanfarhan/Code Project/Portfolio/mediviron.html` with the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Mediviron Clinic — Luqman Farhan</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600;700;800&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/devicon.min.css" />
  <link rel="stylesheet" href="style.css" />
  <link rel="stylesheet" href="project.css" />
</head>
<body>

  <!-- NAV -->
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

  <!-- PROJECT DETAIL -->
  <main class="project-detail">
    <div class="container">

      <a href="index.html#projects" class="back-link">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
          <path d="M19 12H5M12 5l-7 7 7 7"/>
        </svg>
        Back to Projects
      </a>

      <div class="project-header reveal">
        <div class="project-header-meta">
          <div class="project-tags">
            <span class="tag accent">Freelance</span>
            <span class="tag">Astro</span>
            <span class="tag">HTML/CSS</span>
          </div>
          <h1 class="project-detail-title">Mediviron Clinic</h1>
          <p class="project-tagline">Modern landing page for a Kuala Lumpur family clinic.</p>
        </div>

        <div class="project-header-cta">
          <a href="https://medivironclinic.com" target="_blank" rel="noopener" class="btn btn-primary">
            View Live →
          </a>
        </div>
      </div>

      <div class="project-content reveal">
        <div class="project-body">
          <h2 class="content-heading">Overview</h2>
          <p>Freelance project for Clinic Mediviron Jalan Imbi, a family clinic near Bukit Bintang in Kuala Lumpur. The client needed a clean, fast, and mobile-friendly landing page to establish their online presence and make it easy for patients to find them.</p>

          <h2 class="content-heading">What I Built</h2>
          <ul class="feature-list">
            <li>Hero section with clinic name, tagline, and primary CTA</li>
            <li>Services section covering General Practice, ECG, and Ultrasound</li>
            <li>Location and operating hours with nearby landmark references</li>
            <li>WhatsApp CTA for quick patient contact</li>
            <li>Fully responsive layout across mobile, tablet, and desktop</li>
          </ul>

          <h2 class="content-heading">Tech &amp; Decisions</h2>
          <p>Built with Astro for static output — zero JavaScript overhead on a page that doesn't need it. Fast load times, clean HTML, and easy deployment. Right tool for a clinic landing page where SEO and performance matter more than interactivity.</p>
        </div>

        <aside class="project-sidebar">
          <div class="sidebar-card">
            <div class="sidebar-label">Tech Stack</div>
            <div class="stack-tiles">
              <div class="stack-tile">
                <i class="devicon-astro-plain"></i>
                <span>Astro</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-html5-plain colored"></i>
                <span>HTML5</span>
              </div>
              <div class="stack-tile">
                <i class="devicon-css3-plain colored"></i>
                <span>CSS3</span>
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
                <span class="info-val">Landing Page</span>
              </div>
              <div class="info-item">
                <span class="info-key">Role</span>
                <span class="info-val">Freelance Developer</span>
              </div>
              <div class="info-item">
                <span class="info-key">Live</span>
                <a href="https://medivironclinic.com" target="_blank" rel="noopener" class="info-link">View →</a>
              </div>
            </div>
          </div>
        </aside>
      </div>

    </div>
  </main>

  <footer>
    <div class="container">
      <p>© 2026 Luqman Farhan — Designed &amp; built with care</p>
    </div>
  </footer>

  <script src="script.js"></script>
</body>
</html>
```

**Step 2: Verify file exists**

Open `mediviron.html` in browser (or check file exists at repo root).

**Step 3: Commit**

```bash
git add mediviron.html
git commit -m "feat: add Mediviron Clinic project detail page"
```

---

### Task 2: Update `index.html` project card

**Files:**
- Modify: `index.html` (lines ~150–164 — the "Project Three" placeholder card)

**Step 1: Replace placeholder card**

In `index.html`, find this block:

```html
        <!-- ✏️ Replace href with your actual project page -->
        <a href="project.html" class="project-card reveal">
          <div class="project-tags">
            <span class="tag">Flutter</span>
            <span class="tag">Dart</span>
            <span class="tag">Firebase</span>
          </div>
          <h3 class="project-title">Project Three</h3>
          <p class="project-desc">Even a small project is worth showing if it demonstrates a specific skill or solves a real problem you personally faced.</p>
          <div class="project-footer">
            <div class="project-links">
              <span class="project-link">View Details →</span>
            </div>
            <div class="project-arrow" aria-hidden="true">→</div>
          </div>
        </a>
```

Replace with:

```html
        <a href="mediviron.html" class="project-card reveal">
          <div class="project-tags">
            <span class="tag accent">Freelance</span>
            <span class="tag">Astro</span>
            <span class="tag">HTML/CSS</span>
          </div>
          <h3 class="project-title">Mediviron Clinic — Landing Page</h3>
          <p class="project-desc">Freelance landing page for a KL family clinic. Services overview, location, operating hours, and WhatsApp booking — built with Astro for fast static output.</p>
          <div class="project-footer">
            <div class="project-links">
              <span class="project-link">View Details →</span>
            </div>
            <div class="project-arrow" aria-hidden="true">→</div>
          </div>
        </a>
```

**Step 2: Verify in browser**

Open `index.html` — confirm Mediviron card appears in projects grid, click links to `mediviron.html` and live site.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: replace Project Three placeholder with Mediviron Clinic card"
```
