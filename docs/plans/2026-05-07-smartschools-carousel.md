# SmartSchools Logo + Carousel Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add SmartSchools logo inline next to the page title, and replace the static logo showcase with a CSS-driven auto-slide screenshot carousel with dot indicators and a progress bar.

**Architecture:** Pure CSS `@keyframes` drives slide visibility and progress bar animation. Vanilla JS (~15 lines) handles dot generation, active dot sync, and pause-on-hover. No external dependencies. Adding a screenshot = drop one `<img>` in the HTML.

**Tech Stack:** HTML, CSS (custom properties, keyframes), vanilla JS

---

### Task 1: Logo inline with title

**Files:**
- Modify: `smartschool.html:49`
- Modify: `project.css:201-216` (SmartSchool showcase section)

**Step 1: Wrap `<h1>` in title row**

In `smartschool.html`, find line 49:
```html
<h1 class="project-detail-title">SmartSchools</h1>
```
Replace with:
```html
<div class="project-title-row">
  <img src="logo_smartschools.png" class="project-brand-logo" alt="">
  <h1 class="project-detail-title">SmartSchools</h1>
</div>
```

**Step 2: Add CSS for title row**

In `project.css`, add after the `.project-detail-title` block (after line 42):
```css
.project-title-row {
  display: flex;
  align-items: center;
  gap: .75rem;
}
.project-brand-logo {
  height: 36px;
  width: auto;
  display: block;
  flex-shrink: 0;
}
```

**Step 3: Verify in browser**

Open `smartschool.html` in browser. Logo should appear left of "SmartSchools" title, vertically centered, ~36px tall.

**Step 4: Commit**
```bash
git add smartschool.html project.css
git commit -m "feat: add SmartSchools logo inline with page title"
```

---

### Task 2: Replace showcase block with carousel HTML

**Files:**
- Modify: `smartschool.html:60-62`

**Step 1: Replace static logo block**

Find lines 60–62 in `smartschool.html`:
```html
<div class="project-screenshot smartschool-showcase reveal">
  <img src="logo_smartschools.png" alt="SmartSchools logo" class="smartschool-logo-img" />
</div>
```

Replace with:
```html
<div class="ss-carousel reveal">
  <div class="ss-track">
    <div class="ss-slide"><img src="placeholder_web_1.png" alt="Dashboard overview"></div>
    <div class="ss-slide"><img src="placeholder_web_2.png" alt="Attendance tracking"></div>
    <div class="ss-slide"><img src="placeholder_mobile_1.png" alt="Mobile home screen"></div>
    <div class="ss-slide"><img src="placeholder_mobile_2.png" alt="Mobile announcements"></div>
  </div>
  <div class="ss-progress"><div class="ss-bar"></div></div>
  <div class="ss-dots"></div>
</div>
```

Note: placeholder filenames — swap for real screenshots when ready. Each `<div class="ss-slide">` wraps one `<img>`. To add screenshot later: duplicate a `<div class="ss-slide">...</div>` block.

**Step 2: Commit**
```bash
git add smartschool.html
git commit -m "feat: add carousel HTML structure to SmartSchools page"
```

---

### Task 3: Carousel CSS

**Files:**
- Modify: `project.css` — replace `.smartschool-showcase` and `.smartschool-logo-img` blocks (lines 201–216), add carousel styles

**Step 1: Remove old SmartSchool showcase CSS**

In `project.css`, delete lines 201–216:
```css
/* ── SmartSchool showcase ───────────────────────────── */
.smartschool-showcase { ... }
.smartschool-logo-img { ... }
```

**Step 2: Add carousel CSS in its place**

```css
/* ── SmartSchools carousel ──────────────────────────── */
.ss-carousel {
  position: relative;
  margin-bottom: 4rem;
  border-radius: var(--radius);
  border: 1px solid var(--border);
  background: var(--surface2);
  overflow: hidden;
  aspect-ratio: 16 / 9;
  user-select: none;
}

.ss-track {
  position: relative;
  width: 100%;
  height: 100%;
}

.ss-slide {
  position: absolute;
  inset: 0;
  opacity: 0;
  transition: opacity .5s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.ss-slide.active {
  opacity: 1;
}

.ss-slide img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: block;
}

/* Progress bar */
.ss-progress {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 3px;
  background: rgba(255,255,255,.08);
  z-index: 10;
}

.ss-bar {
  height: 100%;
  width: 0%;
  background: var(--accent);
  animation: ss-progress 4.5s linear forwards;
}

@keyframes ss-progress {
  from { width: 0%; }
  to   { width: 100%; }
}

/* Dots */
.ss-dots {
  position: absolute;
  bottom: 1rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: .45rem;
  z-index: 10;
}

.ss-dot {
  width: 6px;
  height: 6px;
  border-radius: 50%;
  background: rgba(255,255,255,.35);
  cursor: pointer;
  transition: background .2s, transform .2s;
  border: none;
  padding: 0;
}

.ss-dot.active {
  background: var(--accent);
  transform: scale(1.3);
}

.ss-dot:hover {
  background: rgba(255,255,255,.65);
}
```

**Step 3: Verify in browser**

First slide should be visible, others hidden. Progress bar at bottom. Dots below (via JS in Task 4).

**Step 4: Commit**
```bash
git add project.css
git commit -m "feat: add SmartSchools carousel CSS with progress bar and dots"
```

---

### Task 4: Carousel JS

**Files:**
- Modify: `smartschool.html` — add `<script>` before `</body>`

**Step 1: Add carousel script**

In `smartschool.html`, just before `</body>`, add:
```html
<script>
  (function () {
    const carousel = document.querySelector('.ss-carousel');
    if (!carousel) return;

    const slides = Array.from(carousel.querySelectorAll('.ss-slide'));
    const dotsContainer = carousel.querySelector('.ss-dots');
    const bar = carousel.querySelector('.ss-bar');
    const DURATION = 4500;
    let current = 0;
    let timer = null;
    let paused = false;

    // Build dots
    slides.forEach((_, i) => {
      const dot = document.createElement('button');
      dot.className = 'ss-dot' + (i === 0 ? ' active' : '');
      dot.setAttribute('aria-label', 'Slide ' + (i + 1));
      dot.addEventListener('click', () => goTo(i));
      dotsContainer.appendChild(dot);
    });

    const dots = Array.from(dotsContainer.querySelectorAll('.ss-dot'));

    function show(index) {
      slides[current].classList.remove('active');
      dots[current].classList.remove('active');
      current = (index + slides.length) % slides.length;
      slides[current].classList.add('active');
      dots[current].classList.add('active');
      // Restart progress bar
      bar.style.animation = 'none';
      bar.offsetHeight; // reflow
      bar.style.animation = 'ss-progress ' + DURATION + 'ms linear forwards';
    }

    function goTo(index) {
      clearTimeout(timer);
      show(index);
      if (!paused) schedule();
    }

    function schedule() {
      timer = setTimeout(() => {
        show(current + 1);
        schedule();
      }, DURATION);
    }

    // Pause on hover
    carousel.addEventListener('mouseenter', () => { paused = true; clearTimeout(timer); });
    carousel.addEventListener('mouseleave', () => { paused = false; schedule(); });

    // Init
    slides[0].classList.add('active');
    schedule();
  })();
</script>
```

**Step 2: Verify in browser**

- First slide visible on load
- Auto-advances every 4.5s
- Progress bar fills then resets
- Dots update with each slide
- Clicking dot jumps to that slide
- Hover pauses auto-advance

**Step 3: Commit**
```bash
git add smartschool.html
git commit -m "feat: add SmartSchools carousel JS — auto-slide, dots, pause on hover"
```

---

### Task 5: Swap placeholders for real screenshots

**Files:**
- Add screenshots to: `/Users/luqmanfarhan/Code Project/Portfolio/` root
- Modify: `smartschool.html` — update `src` and `alt` on each `<div class="ss-slide"><img>` element

**Step 1: Add screenshot files**

Drop real screenshot PNGs into the portfolio root directory. Recommended names:
- `ss_smartschools_dashboard.png` (1280×800)
- `ss_smartschools_attendance.png` (1280×800)
- `ss_smartschools_mobile_home.png` (390×844)
- `ss_smartschools_mobile_feed.png` (390×844)

**Step 2: Update HTML**

Replace each placeholder `src` in the `.ss-slide` blocks with real filenames and update `alt` text.

**Step 3: Verify in browser**

Cycle through all slides. Web screenshots fill container. Mobile screenshots letterbox naturally (surface2 background on sides).

**Step 4: Commit**
```bash
git add *.png smartschool.html
git commit -m "feat: add SmartSchools real screenshots to carousel"
```

---

## Adding screenshots in the future

Drop one block inside `.ss-track` in `smartschool.html`:
```html
<div class="ss-slide"><img src="your_screenshot.png" alt="Description"></div>
```

JS and CSS auto-detect slide count. No other changes needed.
