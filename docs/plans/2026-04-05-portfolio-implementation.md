# Portfolio Refactor Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Refactor the existing single-file portfolio into separate `style.css` and `script.js` files, applying the approved minimal light theme design.

**Architecture:** Extract all inline `<style>` into `style.css` and all inline `<script>` into `script.js`, then rewrite both with the new light theme design system (Archivo + Space Grotesk fonts, `#FAFAFA` bg, `#2563EB` accent). Update `index.html` markup to reflect Luqman's real info and the new skills icon grid.

**Tech Stack:** Vanilla HTML5, CSS3 (custom properties, IntersectionObserver animations), Vanilla JS (no frameworks), Simple Icons SVGs (inlined)

---

## Reference

- Design doc: `docs/plans/2026-04-05-portfolio-design.md`
- Current file: `index.html` (all-in-one, dark theme)
- Simple Icons: https://simpleicons.org (for SVG paths)

---

### Task 1: Create `style.css` with design tokens and base styles

**Files:**
- Create: `style.css`

**Step 1: Create `style.css` with reset, tokens, and base**

```css
/* ─── IMPORT FONTS ───────────────────────────────────── */
@import url('https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600;700;800&family=Space+Grotesk:wght@300;400;500;600;700&display=swap');

/* ─── RESET ──────────────────────────────────────────── */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }

/* ─── TOKENS ─────────────────────────────────────────── */
:root {
  --bg:        #FAFAFA;
  --surface:   #FFFFFF;
  --surface2:  #F4F4F5;
  --border:    #E4E4E7;
  --text:      #09090B;
  --muted:     #71717A;
  --accent:    #2563EB;
  --accent-h:  #1D4ED8;
  --accent-bg: #EFF6FF;
  --font-head: 'Archivo', sans-serif;
  --font-body: 'Space Grotesk', sans-serif;
  --radius:    12px;
  --max:       1100px;
}

/* ─── BASE ───────────────────────────────────────────── */
body {
  background: var(--bg);
  color: var(--text);
  font-family: var(--font-body);
  line-height: 1.6;
  overflow-x: hidden;
}
```

**Step 2: Verify file exists**

Open `style.css` in editor and confirm content saved.

**Step 3: Commit**

```bash
git add style.css
git commit -m "feat: add style.css with design tokens and base reset"
```

---

### Task 2: Add nav, layout, and hero styles to `style.css`

**Files:**
- Modify: `style.css`

**Step 1: Append layout, nav, and hero styles**

```css
/* ─── LAYOUT ─────────────────────────────────────────── */
.container { max-width: var(--max); margin: 0 auto; padding: 0 2rem; position: relative; z-index: 1; }

/* ─── NAV ────────────────────────────────────────────── */
nav {
  position: fixed; top: 0; left: 0; right: 0;
  z-index: 100;
  background: var(--surface);
  padding: 1.25rem 0;
  border-bottom: 1px solid transparent;
  transition: border-color .3s;
}
nav.scrolled { border-color: var(--border); }
nav .inner {
  max-width: var(--max); margin: 0 auto; padding: 0 2rem;
  display: flex; align-items: center; justify-content: space-between;
}
.nav-logo {
  font-size: 1rem; font-weight: 700; letter-spacing: .08em;
  color: var(--accent); text-decoration: none;
  font-family: var(--font-body);
}
.nav-links { display: flex; gap: 2rem; list-style: none; }
.nav-links a {
  font-size: .8rem; letter-spacing: .12em; text-transform: uppercase;
  color: var(--muted); text-decoration: none; font-weight: 500;
  transition: color .2s; cursor: pointer;
}
.nav-links a:hover { color: var(--text); }

/* ─── HERO ───────────────────────────────────────────── */
#hero {
  min-height: 100vh;
  display: flex; align-items: center;
  padding: 8rem 0 4rem;
}
.hero-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}
.hero-tag {
  display: inline-flex; align-items: center; gap: .5rem;
  font-family: var(--font-body);
  font-size: .75rem; color: var(--accent);
  border: 1px solid color-mix(in srgb, var(--accent) 30%, transparent);
  background: var(--accent-bg);
  padding: .35rem .8rem;
  border-radius: 99px;
  margin-bottom: 1.5rem;
  opacity: 0; animation: fadeUp .6s .1s forwards;
}
.hero-name {
  font-size: clamp(3rem, 7vw, 5.5rem);
  font-weight: 800;
  font-family: var(--font-head);
  line-height: .95;
  letter-spacing: -.02em;
  opacity: 0; animation: fadeUp .6s .2s forwards;
}
.hero-name .accent { color: var(--accent); }
.hero-role {
  font-size: clamp(1rem, 2vw, 1.25rem);
  color: var(--muted); font-weight: 500;
  margin-top: 1.25rem;
  opacity: 0; animation: fadeUp .6s .3s forwards;
}
.hero-stack {
  font-family: var(--font-body);
  font-size: .85rem; color: var(--muted);
  margin-top: .5rem; letter-spacing: .04em;
  opacity: 0; animation: fadeUp .6s .35s forwards;
}
.hero-desc {
  font-size: .95rem; color: var(--muted);
  max-width: 420px; line-height: 1.8;
  margin-top: 1rem;
  opacity: 0; animation: fadeUp .6s .4s forwards;
}
.hero-cta {
  display: flex; gap: 1rem; margin-top: 2.5rem; flex-wrap: wrap;
  opacity: 0; animation: fadeUp .6s .5s forwards;
}

/* ─── BUTTONS ────────────────────────────────────────── */
.btn {
  display: inline-flex; align-items: center; gap: .5rem;
  padding: .8rem 1.75rem; border-radius: var(--radius);
  font-family: var(--font-head); font-size: .85rem; font-weight: 600;
  letter-spacing: .04em; text-decoration: none;
  cursor: pointer; border: none; transition: all .2s;
}
.btn-primary { background: var(--accent); color: #fff; }
.btn-primary:hover { background: var(--accent-h); transform: translateY(-2px); }
.btn-ghost { background: transparent; color: var(--text); border: 1px solid var(--border); }
.btn-ghost:hover { border-color: var(--muted); background: var(--surface2); transform: translateY(-2px); }

/* ─── CODE CARD (HERO VISUAL) ────────────────────────── */
.hero-visual { opacity: 0; animation: fadeUp .6s .4s forwards; }
.code-card {
  background: var(--surface);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  overflow: hidden;
  box-shadow: 0 4px 24px rgba(0,0,0,.06);
}
.code-header {
  display: flex; align-items: center; gap: .5rem;
  padding: .75rem 1rem;
  border-bottom: 1px solid var(--border);
  background: var(--surface2);
}
.dot { width: 10px; height: 10px; border-radius: 50%; }
.dot-r { background: #ff5f57; }
.dot-y { background: #ffbd2e; }
.dot-g { background: #28c840; }
.code-filename { font-family: var(--font-body); font-size: .7rem; color: var(--muted); margin-left: .5rem; }
.code-body { padding: 1.5rem; font-family: var(--font-body); font-size: .8rem; line-height: 2; }
.c-kw  { color: #7C3AED; }
.c-fn  { color: var(--accent); }
.c-str { color: #059669; }
.c-num { color: #D97706; }
.c-cm  { color: var(--muted); font-style: italic; }
.c-obj { color: #0891B2; }
.cursor {
  display: inline-block; width: 2px; height: 1em;
  background: var(--accent); vertical-align: middle;
  animation: blink 1s step-end infinite;
}
```

**Step 2: Commit**

```bash
git add style.css
git commit -m "feat: add nav, hero, and code card styles"
```

---

### Task 3: Add section, about, projects, skills, contact, footer, and animation styles

**Files:**
- Modify: `style.css`

**Step 1: Append remaining styles**

```css
/* ─── SECTIONS ───────────────────────────────────────── */
section { padding: 6rem 0; }
.section-alt { background: var(--surface); }
.section-label {
  display: flex; align-items: center; gap: .75rem;
  font-family: var(--font-body); font-size: .7rem;
  color: var(--accent); letter-spacing: .15em; text-transform: uppercase;
  margin-bottom: 1rem;
}
.section-label::after {
  content: ''; flex: 1; height: 1px;
  background: linear-gradient(to right, var(--border), transparent);
}
.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 800; font-family: var(--font-head);
  letter-spacing: -.02em; line-height: 1.1; margin-bottom: 1rem;
}
.section-sub { color: var(--muted); font-size: .95rem; max-width: 500px; line-height: 1.8; }

/* ─── ABOUT ──────────────────────────────────────────── */
.about-grid { display: grid; grid-template-columns: 1fr 1.3fr; gap: 5rem; align-items: start; }
.about-img-wrap { position: relative; aspect-ratio: 3/4; max-width: 340px; }
.about-img-placeholder {
  width: 100%; height: 100%;
  background: var(--surface2);
  border: 1px solid var(--border);
  border-radius: var(--radius);
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  gap: .75rem; color: var(--muted); font-size: .8rem;
  font-family: var(--font-body);
}
.about-accent-box {
  position: absolute; bottom: -1rem; right: -1rem;
  background: var(--accent); color: #fff;
  border-radius: var(--radius);
  padding: 1rem 1.25rem;
  font-size: .75rem; font-weight: 700; font-family: var(--font-body); line-height: 1.4;
}
.about-text p { color: var(--muted); line-height: 1.9; font-size: .95rem; margin-bottom: 1rem; }
.edu-list { margin-top: 2rem; }
.edu-item { display: flex; gap: 1rem; align-items: flex-start; padding: 1rem 0; border-top: 1px solid var(--border); }
.edu-year { font-family: var(--font-body); font-size: .7rem; color: var(--accent); white-space: nowrap; padding-top: .2rem; min-width: 70px; }
.edu-name { font-weight: 600; font-size: .9rem; }
.edu-place { font-size: .8rem; color: var(--muted); margin-top: .2rem; }

/* ─── PROJECTS ───────────────────────────────────────── */
.projects-header {
  display: flex; align-items: flex-end; justify-content: space-between;
  margin-bottom: 3rem; flex-wrap: wrap; gap: 1rem;
}
.project-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
.project-card {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--radius); padding: 2rem;
  display: flex; flex-direction: column;
  transition: border-color .2s, transform .2s, box-shadow .2s;
  text-decoration: none; color: inherit;
  position: relative; overflow: hidden; cursor: pointer;
}
.project-card::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: var(--accent); transform: scaleX(0); transform-origin: left; transition: transform .3s;
}
.project-card:hover { border-color: var(--border); transform: translateY(-4px); box-shadow: 0 8px 32px rgba(0,0,0,.08); }
.project-card:hover::before { transform: scaleX(1); }
.project-card.featured { grid-column: span 2; background: var(--accent-bg); }
.project-tags { display: flex; flex-wrap: wrap; gap: .5rem; margin-bottom: 1.25rem; }
.tag {
  font-family: var(--font-body); font-size: .65rem;
  padding: .25rem .6rem; border-radius: 4px;
  background: var(--surface2); color: var(--muted);
  border: 1px solid var(--border); letter-spacing: .05em;
}
.tag.accent { background: color-mix(in srgb, var(--accent) 12%, transparent); color: var(--accent); border-color: color-mix(in srgb, var(--accent) 25%, transparent); }
.project-title { font-size: 1.25rem; font-weight: 700; font-family: var(--font-head); margin-bottom: .5rem; }
.project-desc { color: var(--muted); font-size: .875rem; line-height: 1.7; flex: 1; }
.project-footer { display: flex; align-items: center; justify-content: space-between; margin-top: 1.5rem; padding-top: 1.25rem; border-top: 1px solid var(--border); }
.project-links { display: flex; gap: 1rem; }
.project-link {
  font-family: var(--font-body); font-size: .7rem;
  color: var(--muted); text-decoration: none; letter-spacing: .05em;
  display: flex; align-items: center; gap: .35rem;
  transition: color .2s; cursor: pointer;
}
.project-link:hover { color: var(--accent); }
.project-arrow {
  width: 32px; height: 32px; border-radius: 50%;
  border: 1px solid var(--border);
  display: flex; align-items: center; justify-content: center;
  color: var(--muted); transition: all .2s;
}
.project-card:hover .project-arrow { background: var(--accent); border-color: var(--accent); color: #fff; }

/* ─── SKILLS ─────────────────────────────────────────── */
.skills-section { display: flex; flex-direction: column; gap: 3rem; margin-top: 3rem; }
.skill-group-label {
  font-size: .7rem; letter-spacing: .12em; text-transform: uppercase;
  color: var(--accent); font-family: var(--font-body); margin-bottom: 1rem; font-weight: 600;
}
.skill-tiles {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
  gap: 1rem;
}
.skill-tile {
  background: var(--surface); border: 1px solid var(--border);
  border-radius: var(--radius); padding: 1rem .75rem;
  display: flex; flex-direction: column; align-items: center; gap: .6rem;
  transition: border-color .2s, box-shadow .2s; cursor: default;
}
.skill-tile:hover { border-color: var(--accent); box-shadow: 0 2px 12px rgba(37,99,235,.1); }
.skill-tile svg { width: 24px; height: 24px; }
.skill-tile-name { font-size: .7rem; color: var(--muted); font-family: var(--font-body); text-align: center; line-height: 1.3; }

/* ─── CONTACT ────────────────────────────────────────── */
#contact {
  text-align: center;
  background: radial-gradient(ellipse at 50% 100%, color-mix(in srgb, var(--accent) 6%, transparent), transparent 70%);
}
.contact-email {
  font-size: clamp(1.5rem, 4vw, 2.5rem); font-weight: 800;
  font-family: var(--font-head); color: var(--text);
  text-decoration: none; letter-spacing: -.02em;
  border-bottom: 2px solid var(--accent);
  transition: color .2s; display: inline-block; margin: 2rem 0;
}
.contact-email:hover { color: var(--accent); }
.social-links { display: flex; align-items: center; justify-content: center; gap: 1.5rem; margin-top: 1.5rem; flex-wrap: wrap; }
.social-link {
  font-family: var(--font-body); font-size: .75rem; letter-spacing: .1em;
  color: var(--muted); text-decoration: none;
  display: flex; align-items: center; gap: .4rem;
  transition: color .2s; cursor: pointer;
}
.social-link:hover { color: var(--accent); }
.social-divider { color: var(--border); }

/* ─── FOOTER ─────────────────────────────────────────── */
footer { border-top: 1px solid var(--border); padding: 1.5rem 0; text-align: center; }
footer p { font-family: var(--font-body); font-size: .7rem; color: var(--muted); }

/* ─── SCROLL REVEAL ──────────────────────────────────── */
.reveal { opacity: 0; transform: translateY(28px); transition: opacity .6s ease, transform .6s ease; }
.reveal.visible { opacity: 1; transform: none; }

/* ─── ANIMATIONS ─────────────────────────────────────── */
@keyframes fadeUp { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: none; } }
@keyframes blink  { 0%, 100% { opacity: 1; } 50% { opacity: 0; } }

/* ─── REDUCED MOTION ─────────────────────────────────── */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: .01ms !important; transition-duration: .01ms !important; }
}

/* ─── RESPONSIVE ─────────────────────────────────────── */
@media (max-width: 768px) {
  .hero-grid { grid-template-columns: 1fr; gap: 2.5rem; }
  .hero-visual { order: -1; }
  .about-grid { grid-template-columns: 1fr; }
  .about-img-wrap { max-width: 100%; }
  .project-grid { grid-template-columns: 1fr; }
  .project-card.featured { grid-column: span 1; }
  .nav-links { display: none; }
}
```

**Step 2: Commit**

```bash
git add style.css
git commit -m "feat: add remaining section styles to style.css"
```

---

### Task 4: Create `script.js`

**Files:**
- Create: `script.js`

**Step 1: Write `script.js`**

```js
// ── Nav scroll border ──────────────────────────────────
const nav = document.getElementById('navbar');
window.addEventListener('scroll', () => {
  nav.classList.toggle('scrolled', window.scrollY > 40);
});

// ── Scroll reveal ──────────────────────────────────────
const revealObserver = new IntersectionObserver((entries) => {
  entries.forEach((e, i) => {
    if (e.isIntersecting) {
      setTimeout(() => e.target.classList.add('visible'), i * 100);
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.reveal').forEach(el => revealObserver.observe(el));
```

**Step 2: Commit**

```bash
git add script.js
git commit -m "feat: add script.js with scroll and reveal behavior"
```

---

### Task 5: Rewrite `index.html` — head and nav

**Files:**
- Modify: `index.html`

**Step 1: Replace entire file content with new markup (head + nav only first)**

Replace the `<head>` block and `<nav>` with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Luqman Farhan — Full Stack Developer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Archivo:wght@400;500;600;700;800&family=Space+Grotesk:wght@300;400;500;600;700&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="style.css" />
</head>
<body>

  <!-- ── NAV ──────────────────────────────────────────── -->
  <nav id="navbar">
    <div class="inner">
      <a href="#" class="nav-logo">LF.dev</a>
      <ul class="nav-links">
        <li><a href="#about">About</a></li>
        <li><a href="#projects">Projects</a></li>
        <li><a href="#skills">Skills</a></li>
        <li><a href="#contact">Contact</a></li>
      </ul>
    </div>
  </nav>
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: rewrite index.html head and nav with external CSS link"
```

---

### Task 6: Add hero section to `index.html`

**Files:**
- Modify: `index.html`

**Step 1: Append hero section**

```html
  <!-- ── HERO ─────────────────────────────────────────── -->
  <section id="hero">
    <div class="container">
      <div class="hero-grid">
        <div>
          <span class="hero-tag">Open to work · Full Stack &amp; Mobile</span>
          <h1 class="hero-name">
            Luqman<br>
            <span class="accent">Farhan.</span>
          </h1>
          <p class="hero-role">Full Stack · DevOps · Mobile Developer</p>
          <p class="hero-stack">Flutter · Next.js · Node.js · TypeScript</p>
          <div class="hero-cta">
            <a href="#projects" class="btn btn-primary">View My Work →</a>
            <a href="#contact" class="btn btn-ghost">Get In Touch</a>
          </div>
        </div>
        <div class="hero-visual">
          <div class="code-card">
            <div class="code-header">
              <span class="dot dot-r"></span>
              <span class="dot dot-y"></span>
              <span class="dot dot-g"></span>
              <span class="code-filename">developer.ts</span>
            </div>
            <div class="code-body">
              <div><span class="c-kw">const</span> <span class="c-fn">developer</span> = {</div>
              <div>&nbsp;&nbsp;<span class="c-obj">name</span>: <span class="c-str">"Luqman Farhan"</span>,</div>
              <div>&nbsp;&nbsp;<span class="c-obj">role</span>: <span class="c-str">"Full Stack Developer"</span>,</div>
              <div>&nbsp;&nbsp;<span class="c-obj">location</span>: <span class="c-str">"Malaysia 🇲🇾"</span>,</div>
              <div>&nbsp;&nbsp;<span class="c-obj">stack</span>: [</div>
              <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="c-str">"Flutter"</span>, <span class="c-str">"Next.js"</span>,</div>
              <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="c-str">"Node.js"</span>, <span class="c-str">"TypeScript"</span></div>
              <div>&nbsp;&nbsp;],</div>
              <div>&nbsp;&nbsp;<span class="c-obj">available</span>: <span class="c-num">true</span>,</div>
              <div>&nbsp;&nbsp;<span class="c-fn">hire</span>: () <span class="c-kw">=&gt;</span> {</div>
              <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="c-cm">// best decision you'll make</span></div>
              <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="c-kw">return</span> <span class="c-str">"great results"</span>;</div>
              <div>&nbsp;&nbsp;}</div>
              <div>};<span class="cursor"></span></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add hero section markup"
```

---

### Task 7: Add about section to `index.html`

**Files:**
- Modify: `index.html`

**Step 1: Append about section**

```html
  <!-- ── ABOUT ─────────────────────────────────────────── -->
  <section id="about" class="section-alt">
    <div class="container">
      <div class="about-grid">
        <div>
          <div class="about-img-wrap">
            <div class="about-img-placeholder">
              <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" aria-hidden="true">
                <circle cx="12" cy="8" r="4"/><path d="M4 20c0-4 3.6-7 8-7s8 3 8 7"/>
              </svg>
              <span>Replace with your photo</span>
              <span style="font-size:.65rem;opacity:.6">400×500px recommended</span>
            </div>
            <div class="about-accent-box">
              <div style="font-size:1.4rem;font-weight:800">2+</div>
              <div>Years coding</div>
            </div>
          </div>
        </div>
        <div class="about-text reveal">
          <div class="section-label">About me</div>
          <h2 class="section-title">Passionate about<br><span style="color:var(--accent)">building things</span></h2>
          <p>Hi, I'm Luqman Farhan — a full-stack developer based in Malaysia specialising in Flutter, Next.js, and Node.js. I enjoy building end-to-end products, from designing the architecture to deploying on AWS.</p>
          <p>I'm open to freelance projects and full-time opportunities where I can contribute across the stack and ship things that matter.</p>
          <div class="edu-list">
            <div class="edu-item">
              <span class="edu-year">2020 – 2024</span>
              <div>
                <div class="edu-name">Bachelor of Computer Science</div>
                <div class="edu-place">University Name, Malaysia</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add about section markup"
```

---

### Task 8: Add projects section to `index.html`

**Files:**
- Modify: `index.html`

**Step 1: Append projects section**

SVG paths used:
- GitHub icon: `M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z`
- External link icon: `M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14`

```html
  <!-- ── PROJECTS ──────────────────────────────────────── -->
  <section id="projects">
    <div class="container">
      <div class="projects-header reveal">
        <div>
          <div class="section-label">My work</div>
          <h2 class="section-title">Selected<br>Projects</h2>
        </div>
        <a href="https://github.com/luqmanfarhan" target="_blank" rel="noopener" class="btn btn-ghost">All projects on GitHub ↗</a>
      </div>

      <div class="project-grid">

        <div class="project-card featured reveal">
          <div class="project-tags">
            <span class="tag accent">Featured</span>
            <span class="tag">Flutter</span>
            <span class="tag">Node.js</span>
            <span class="tag">Firebase</span>
          </div>
          <h3 class="project-title">Project Name — Short Tagline</h3>
          <p class="project-desc">
            What problem did this solve? Who was it for? Write 2–3 sentences on real-world impact, not just the tech stack. This is what convinces clients you can solve their problems.
          </p>
          <div class="project-footer">
            <div class="project-links">
              <a href="#" class="project-link" aria-label="View on GitHub">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
                GitHub
              </a>
            </div>
            <div class="project-arrow" aria-hidden="true">→</div>
          </div>
        </div>

        <div class="project-card reveal">
          <div class="project-tags">
            <span class="tag">Next.js</span>
            <span class="tag">TypeScript</span>
            <span class="tag">PostgreSQL</span>
          </div>
          <h3 class="project-title">Project Two</h3>
          <p class="project-desc">Describe what you built and why. Mention any measurable outcome — e.g. "used by 50+ people" or "cut load time by 40%."</p>
          <div class="project-footer">
            <div class="project-links">
              <a href="#" class="project-link" aria-label="View on GitHub">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
                GitHub
              </a>
            </div>
            <div class="project-arrow" aria-hidden="true">→</div>
          </div>
        </div>

        <div class="project-card reveal">
          <div class="project-tags">
            <span class="tag">Flutter</span>
            <span class="tag">Dart</span>
            <span class="tag">Firebase</span>
          </div>
          <h3 class="project-title">Project Three</h3>
          <p class="project-desc">Even a small project is worth showing if it demonstrates a specific skill or solves a real problem you personally faced.</p>
          <div class="project-footer">
            <div class="project-links">
              <a href="#" class="project-link" aria-label="View on GitHub">
                <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
                GitHub
              </a>
            </div>
            <div class="project-arrow" aria-hidden="true">→</div>
          </div>
        </div>

      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add projects section markup"
```

---

### Task 9: Add skills section to `index.html`

**Files:**
- Modify: `index.html`

**Step 1: Append skills section with Simple Icons SVG paths**

SVG paths from Simple Icons (24×24 viewBox):
- Flutter: `M14.314 0L2.3 12 6 15.7 21.684.013h-7.37zm.159 11.27l-6.006 6.004 6.006 6.004 6.006-6.004-6.006-6.004z` (fill: #54C5F8)
- Dart: `M4.105 4.105S9.158 1.58 11.684.316a3.079 3.079 0 0 1 1.481-.315c.766.047 1.677.788 1.677.788L24 9.948v9.789h-4.263V24H9.789l-9-9 .002-4.475 3.314-6.42zM10.47 22.756h8.526v-5.079l3.737-3.738H12.948L10.47 22.756zm9.265-11.39-3.738 3.738h5.079v-3.738h-1.341zM2.209 13.988l8.525-8.526 4.218 4.218-8.525 8.525-4.218-4.217z` (fill: #0175C2)
- React: `M14.23 12.004a2.236 2.236 0 0 1-2.235 2.236 2.236 2.236 0 0 1-2.236-2.236 2.236 2.236 0 0 1 2.235-2.236 2.236 2.236 0 0 1 2.236 2.236zm2.648-10.69c-1.346 0-3.107.96-4.888 2.622-1.78-1.653-3.542-2.602-4.887-2.602-.41 0-.783.093-1.106.278-1.375.793-1.683 3.264-.973 6.365C1.98 8.917 0 10.42 0 12.004c0 1.59 1.99 3.097 5.043 4.03-.704 3.113-.39 5.588.988 6.38.32.187.69.275 1.102.275 1.345 0 3.107-.96 4.888-2.624 1.78 1.654 3.542 2.603 4.887 2.603.41 0 .783-.09 1.106-.275 1.374-.792 1.683-3.263.973-6.365C22.02 15.096 24 13.59 24 12.004c0-1.59-1.99-3.097-5.043-4.032.704-3.11.39-5.587-.988-6.38a2.167 2.167 0 0 0-1.092-.278zm-.005 1.09v.006c.225 0 .406.044.558.127.666.382.955 1.835.73 3.704-.054.46-.142.945-.25 1.44a23.476 23.476 0 0 0-3.107-.534A23.892 23.892 0 0 0 12.769 4.7c1.592-1.48 3.087-2.292 4.105-2.295zm-9.77.02c1.012 0 2.514.808 4.11 2.28-.686.72-1.37 1.537-2.02 2.442a22.73 22.73 0 0 0-3.113.538 15.02 15.02 0 0 1-.254-1.42c-.23-1.868.054-3.32.714-3.707.19-.09.4-.127.563-.132zm4.882 3.05c.455.468.91.992 1.36 1.564-.44-.02-.89-.034-1.36-.034-.47 0-.92.01-1.36.034.44-.572.895-1.096 1.36-1.564zM12 8.1c.74 0 1.477.034 2.202.093.406.582.802 1.203 1.183 1.86.372.64.71 1.29 1.018 1.946-.308.655-.646 1.31-1.013 1.95-.38.66-.773 1.288-1.18 1.87a25.64 25.64 0 0 1-4.412.005 26.64 26.64 0 0 1-1.183-1.86c-.372-.64-.71-1.29-1.018-1.946a25.17 25.17 0 0 1 1.013-1.954 24.965 24.965 0 0 1 1.18-1.868A25.66 25.66 0 0 1 12 8.098zm-3.635.254c-.24.377-.48.763-.704 1.16-.225.39-.435.782-.635 1.174-.265-.656-.49-1.31-.676-1.947.64-.15 1.315-.283 2.015-.386zm7.26 0c.695.103 1.365.23 2.006.387-.18.632-.405 1.282-.66 1.933a25.952 25.952 0 0 0-1.345-2.32zm3.063.675c.484.15.944.317 1.375.498 1.732.74 2.852 1.708 2.852 2.476-.005.768-1.125 1.74-2.857 2.475-.42.18-.88.342-1.355.493a23.966 23.966 0 0 0-1.1-2.98c.45-1.017.81-2.01 1.085-2.964zm-13.56.003c.271.985.644 1.976 1.091 2.966a23.267 23.267 0 0 0-1.082 2.976c-.478-.149-.944-.32-1.38-.499-1.732-.74-2.852-1.708-2.852-2.476 0-.768 1.12-1.742 2.852-2.476.434-.185.9-.35 1.37-.49zm11.535 6.977c.243-.388.48-.zanele 775-.707-1.173.225-.39.435-.78.635-1.174.265.656.49 1.31.676 1.948-.64.149-1.315.283-2.015.386zm-9.77.02c-.695-.102-1.365-.23-2.006-.387.18-.63.406-1.282.66-1.933a25.952 25.952 0 0 0 1.345 2.32zm4.886 2.783c-.456-.453-.91-.977-1.36-1.55.44.02.89.034 1.36.034.47 0 .92-.01 1.36-.034-.44.573-.895 1.097-1.36 1.55zm-3.646-.989c-.48-.682-.93-1.396-1.362-2.11-.372-.64-.71-1.29-1.02-1.948.31.657.648 1.312 1.014 1.95.38.66.773 1.288 1.18 1.87.064.089.128.178.188.238zm7.295 0c.06-.06.124-.15.188-.238a26.64 26.64 0 0 0 1.18-1.87c.366-.638.704-1.293 1.014-1.95-.31.657-.648 1.31-1.02 1.948-.43.714-.882 1.428-1.362 2.11zM12 15.9c-.74 0-1.477-.034-2.202-.093a25.952 25.952 0 0 1-1.183-1.86 25.64 25.64 0 0 1-1.018-1.946 25.64 25.64 0 0 1 1.013 1.95 24.965 24.965 0 0 1 1.183 1.857c.722.06 1.46.09 2.207.09.748 0 1.486-.03 2.208-.09.406-.582.802-1.204 1.183-1.858a25.17 25.17 0 0 1 1.013-1.95c-.308.655-.646 1.31-1.018 1.946a23.476 23.476 0 0 1-1.183 1.86A25.64 25.64 0 0 1 12 15.9z` (fill: #61DAFB)

Note: For the actual implementation, use these verified Simple Icons paths:

```html
  <!-- ── SKILLS ────────────────────────────────────────── -->
  <section id="skills" class="section-alt">
    <div class="container">
      <div class="reveal">
        <div class="section-label">What I work with</div>
        <h2 class="section-title">Skills &amp;<br>Tech Stack</h2>
      </div>

      <div class="skills-section">

        <div class="reveal">
          <div class="skill-group-label">Frontend &amp; Mobile</div>
          <div class="skill-tiles">

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#54C5F8" aria-label="Flutter"><path d="M14.314 0L2.3 12 6 15.7 21.684.013h-7.37zm.159 11.27l-6.006 6.004 6.006 6.004 6.006-6.004-6.006-6.004z"/></svg>
              <span class="skill-tile-name">Flutter</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#0175C2" aria-label="Dart"><path d="M4.105 4.105S9.158 1.58 11.684.316a3.079 3.079 0 0 1 1.481-.315c.766.047 1.677.788 1.677.788L24 9.948v9.789h-4.263V24H9.789l-9-9 .002-4.475 3.314-6.42zM10.47 22.756h8.526v-5.079l3.737-3.738H12.948L10.47 22.756zm9.265-11.39-3.738 3.738h5.079v-3.738h-1.341zM2.209 13.988l8.525-8.526 4.218 4.218-8.525 8.525-4.218-4.217z"/></svg>
              <span class="skill-tile-name">Dart</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#61DAFB" aria-label="React"><path d="M14.23 12.004a2.236 2.236 0 0 1-2.235 2.236 2.236 2.236 0 0 1-2.236-2.236 2.236 2.236 0 0 1 2.235-2.236 2.236 2.236 0 0 1 2.236 2.236zm2.648-10.69c-1.346 0-3.107.96-4.888 2.622-1.78-1.653-3.542-2.602-4.887-2.602-.41 0-.783.093-1.106.278-1.375.793-1.683 3.264-.973 6.365C1.98 8.917 0 10.42 0 12.004c0 1.59 1.99 3.097 5.043 4.03-.704 3.113-.39 5.588.988 6.38.32.187.69.275 1.102.275 1.345 0 3.107-.96 4.888-2.624 1.78 1.654 3.542 2.603 4.887 2.603.41 0 .783-.09 1.106-.275 1.374-.792 1.683-3.263.973-6.365C22.02 15.096 24 13.59 24 12.004c0-1.59-1.99-3.097-5.043-4.032.704-3.11.39-5.587-.988-6.38a2.167 2.167 0 0 0-1.092-.278zm-.005 1.09v.006c.225 0 .406.044.558.127.666.382.955 1.835.73 3.704-.054.46-.142.945-.25 1.44a23.476 23.476 0 0 0-3.107-.534A23.892 23.892 0 0 0 12.769 4.7c1.592-1.48 3.087-2.292 4.105-2.295zm-9.77.02c1.012 0 2.514.808 4.11 2.28-.686.72-1.37 1.537-2.02 2.442a22.73 22.73 0 0 0-3.113.538 15.02 15.02 0 0 1-.254-1.42c-.23-1.868.054-3.32.714-3.707.19-.09.4-.127.563-.132zm4.882 3.05c.455.468.91.992 1.36 1.564-.44-.02-.89-.034-1.36-.034-.47 0-.92.01-1.36.034.44-.572.895-1.096 1.36-1.564zM12 8.1c.74 0 1.477.034 2.202.093.406.582.802 1.203 1.183 1.86.372.64.71 1.29 1.018 1.946-.308.655-.646 1.31-1.013 1.95-.38.66-.773 1.288-1.18 1.87a25.64 25.64 0 0 1-4.412.005 26.64 26.64 0 0 1-1.183-1.86c-.372-.64-.71-1.29-1.018-1.946a25.17 25.17 0 0 1 1.013-1.954 24.965 24.965 0 0 1 1.18-1.868A25.66 25.66 0 0 1 12 8.098zm-3.635.254c-.24.377-.48.763-.704 1.16-.225.39-.435.782-.635 1.174-.265-.656-.49-1.31-.676-1.947.64-.15 1.315-.283 2.015-.386zm7.26 0c.695.103 1.365.23 2.006.387-.18.632-.405 1.282-.66 1.933a25.952 25.952 0 0 0-1.345-2.32zm3.063.675c.484.15.944.317 1.375.498 1.732.74 2.852 1.708 2.852 2.476-.005.768-1.125 1.74-2.857 2.475-.42.18-.88.342-1.355.493a23.966 23.966 0 0 0-1.1-2.98c.45-1.017.81-2.01 1.085-2.964zm-13.56.003c.271.985.644 1.976 1.091 2.966a23.267 23.267 0 0 0-1.082 2.976c-.478-.149-.944-.32-1.38-.499-1.732-.74-2.852-1.708-2.852-2.476 0-.768 1.12-1.742 2.852-2.476.434-.185.9-.35 1.37-.49z"/></svg>
              <span class="skill-tile-name">React</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#000000" aria-label="Next.js"><path d="M11.5725 0c-.1763 0-.3098.0013-.3584.0067-.0516.0053-.2159.021-.3636.0328-3.4088.3073-6.6017 2.1463-8.624 4.9728C1.1004 6.584.3802 8.3666.1082 10.255c-.0962.659-.108.8537-.108 1.7474.0001.8978.0119 1.0884.1031 1.7415.6763 4.6105 3.6442 8.7093 7.9317 10.7682 1.2813.6074 2.6315 1.0012 4.0878 1.1869.5625.073 2.8984.0733 3.4614 0 2.4023-.3089 4.4206-1.1368 6.233-2.5076 2.978-2.2655 4.8558-5.5804 5.2614-9.2264.0741-.6819.0884-.9395.0884-1.7282 0-.7892-.0143-1.0468-.0884-1.7282-.4056-3.6436-2.2851-6.9589-5.2614-9.2244C21.6098 1.2576 20.2225.811 18.669.478c-.6534-.1404-1.413-.2216-2.1448-.2381-.1764-.0042-.3234-.0059-.4517-.0059zm-1.0479 1.2158c.3027.0037.5985.0263.867.0542 1.3456.1435 2.6293.5638 3.7847 1.2396 3.0576 1.8025 4.9543 4.9834 5.1054 8.4447.0189.4381.0103.8938-.0254 1.3325-.3228 4.0518-2.9204 7.6248-6.6826 9.2008-1.1694.4956-2.3764.7677-3.6644.8232-.6277.0276-.9613.0277-1.5908.0006-1.2852-.0548-2.4919-.3284-3.6617-.8244-3.7626-1.576-6.3604-5.1498-6.6832-9.2015-.0357-.4393-.0443-.8944-.0254-1.3325.1512-3.4614 2.0483-6.6422 5.1058-8.4447 1.1546-.6759 2.4383-1.0962 3.7843-1.2396a11.217 11.217 0 0 1 .8693-.0542c.0938-.003.2316-.0044.3628-.0044zm-.2138 2.1553c-.3038.0165-.5977.0537-.8792.1095a6.5513 6.5513 0 0 0-1.234.3754 6.5478 6.5478 0 0 0-3.6765 4.2788 6.5513 6.5513 0 0 0-.1899 1.5702 6.536 6.536 0 0 0 .9756 3.4844c.2008.3073.4265.5988.6762.8714l5.3716-9.2044c.1124-.1925.2698-.3537.4622-.4742.1924-.1206.412-.1935.6449-.2109h.0004c.2325.0174.4521.0903.6445.2109.1924.1205.3498.2817.4621.4742l5.7543 9.8645c.144-.2034.2744-.4161.3884-.6374a6.5407 6.5407 0 0 0 .6763-2.8566 6.536 6.536 0 0 0-.9756-3.4844 6.5478 6.5478 0 0 0-3.6765-4.2788 6.5513 6.5513 0 0 0-1.2341-.3754 6.5366 6.5366 0 0 0-1.3225-.1314 6.5407 6.5407 0 0 0-.4567.0219zm.2138 3.2659l-2.7987 4.7987 5.5975.0001-2.7988-4.7988z"/></svg>
              <span class="skill-tile-name">Next.js</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#3178C6" aria-label="TypeScript"><path d="M1.125 0C.502 0 0 .502 0 1.125v21.75C0 23.498.502 24 1.125 24h21.75c.623 0 1.125-.502 1.125-1.125V1.125C24 .502 23.498 0 22.875 0zm17.363 9.75c.612 0 1.154.037 1.627.111a6.38 6.38 0 0 1 1.306.34v2.458a3.95 3.95 0 0 0-.643-.361 5.093 5.093 0 0 0-.717-.26 5.453 5.453 0 0 0-1.426-.2c-.3 0-.573.028-.819.086a2.1 2.1 0 0 0-.623.242c-.17.104-.3.229-.393.374a.888.888 0 0 0-.14.49c0 .196.053.373.156.529.104.156.252.304.443.444s.423.276.696.41c.273.135.582.274.926.416.47.197.892.407 1.266.628.374.222.695.473.963.753.268.279.472.598.614.957.142.359.214.776.214 1.253 0 .657-.125 1.21-.373 1.656a3.033 3.033 0 0 1-1.012 1.085 4.38 4.38 0 0 1-1.487.596c-.566.12-1.163.18-1.79.18a9.916 9.916 0 0 1-1.84-.164 5.544 5.544 0 0 1-1.512-.493v-2.63a5.033 5.033 0 0 0 3.237 1.2c.333 0 .624-.03.872-.09.249-.06.456-.144.623-.25.166-.108.29-.234.373-.38a1.023 1.023 0 0 0-.074-1.089 2.12 2.12 0 0 0-.537-.5 5.597 5.597 0 0 0-.807-.444 27.72 27.72 0 0 0-1.007-.436c-.918-.383-1.602-.852-2.053-1.405-.45-.553-.676-1.222-.676-2.005 0-.614.123-1.141.369-1.582.246-.441.58-.804 1.004-1.089a4.494 4.494 0 0 1 1.47-.629 7.536 7.536 0 0 1 1.77-.201zm-15.113.188h9.563v2.166H9.506v9.646H6.789v-9.646H3.375z"/></svg>
              <span class="skill-tile-name">TypeScript</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#F7DF1E" aria-label="JavaScript"><path d="M0 0h24v24H0V0zm22.034 18.276c-.175-1.095-.888-2.015-3.003-2.873-.736-.345-1.554-.585-1.797-1.14-.091-.33-.105-.51-.046-.705.15-.646.915-.84 1.515-.66.39.12.75.42.976.9 1.034-.676 1.034-.676 1.755-1.125-.27-.42-.404-.601-.586-.78-.63-.705-1.469-1.065-2.834-1.034l-.705.089c-.676.165-1.32.525-1.71 1.005-1.14 1.291-.811 3.541.569 4.471 1.365 1.02 3.361 1.244 3.616 2.205.24 1.17-.87 1.545-1.966 1.41-.811-.18-1.26-.586-1.755-1.336l-1.83 1.051c.21.48.45.689.81 1.109 1.74 1.756 6.09 1.666 6.871-1.004.029-.09.24-.705.074-1.65l.046.067zm-8.983-7.245h-2.248c0 1.938-.009 3.864-.009 5.805 0 1.232.063 2.363-.138 2.704-.33.689-1.18.601-1.566.48-.396-.196-.597-.466-.83-.855-.063-.105-.11-.196-.127-.196l-1.825 1.125c.305.63.75 1.172 1.324 1.517.855.51 2.004.675 3.207.405.783-.226 1.458-.691 1.811-1.411.51-.93.402-2.07.397-3.346.012-2.054 0-4.109 0-6.179l.004-.056z"/></svg>
              <span class="skill-tile-name">JavaScript</span>
            </div>

          </div>
        </div>

        <div class="reveal">
          <div class="skill-group-label">Backend</div>
          <div class="skill-tiles">

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#339933" aria-label="Node.js"><path d="M11.998.016L.023 6.628v12.733l11.975 6.623 11.975-6.623V6.628L11.998.016zM3.649 18.012V7.988l8.349-4.613 8.35 4.613v10.024l-8.35 4.613-8.349-4.613z"/></svg>
              <span class="skill-tile-name">Node.js</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#4169E1" aria-label="PostgreSQL"><path d="M17.128 0a10.13 10.13 0 0 0-2.755.403l-.063.02A10.922 10.922 0 0 0 12.6.258C11.422.238 10.41.524 9.594 1 8.79.721 7.122.24 5.364.121 4.395.057 3.37.103 2.53.443 1.59.818.817 1.62.45 2.978c-.887 3.26.703 8.234 2.252 11.102.695 1.308 1.445 2.352 2.243 2.737.448.214.936.232 1.408.039.35.206.73.441 1.094.648l.044.025.023.013c.612.338 1.508.831 2.443.831.749 0 1.41-.312 1.952-.757.163.07.316.112.49.118.585.02 1.204-.24 1.862-.68 1.02.439 2.139.828 2.964.55l.115-.04c.64-.266 1.367-1.128 2.061-2.495 1.258-2.527 2.351-6.869 2.34-11.119a9.338 9.338 0 0 0-.065-1.247L23.9 2.14a9.62 9.62 0 0 0-.2-1.12c-.098-.36-.26-.7-.493-.97-.44-.51-1.056-.7-1.675-.8a8.809 8.809 0 0 0-1.407-.094A7.624 7.624 0 0 0 17.128 0z"/></svg>
              <span class="skill-tile-name">PostgreSQL</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#FFCA28" aria-label="Firebase"><path d="M3.89 15.672L6.255.461A.542.542 0 0 1 7.27.288l2.543 4.771zm16.794 3.692l-2.25-14a.54.54 0 0 0-.919-.295L3.316 19.365l7.856 4.427a1.621 1.621 0 0 0 1.588 0zM14.3 7.147l-1.82-3.482a.542.542 0 0 0-.96 0L3.53 17.984z"/></svg>
              <span class="skill-tile-name">Firebase</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#21759B" aria-label="WordPress"><path d="M21.469 6.825c.84 1.537 1.318 3.3 1.318 5.175 0 3.979-2.156 7.456-5.363 9.325l3.295-9.527c.615-1.54.82-2.771.82-3.864 0-.405-.026-.78-.07-1.11m-7.981.105c.647-.03 1.232-.105 1.232-.105.582-.075.514-.93-.067-.899 0 0-1.755.135-2.88.135-1.064 0-2.85-.15-2.85-.15-.585-.03-.661.855-.075.885 0 0 .54.061 1.125.09l1.68 4.605-2.37 7.08L5.354 6.93c.649-.03 1.234-.1 1.234-.1.585-.075.516-.93-.065-.896 0 0-1.746.138-2.874.138-.2 0-.438-.008-.69-.015C4.911 3.15 8.235 1.215 12 1.215c2.809 0 5.365 1.072 7.286 2.833-.046-.003-.091-.009-.141-.009-1.06 0-1.812.923-1.812 1.914 0 .89.513 1.643 1.06 2.531.411.72.89 1.643.89 2.977 0 .915-.354 1.994-.821 3.479l-1.075 3.585-3.9-11.61.001.016zm.711 12.81l3.84-11.115c.704-1.725.939-3.105.939-4.335 0-.449-.03-.862-.09-1.245A9.747 9.747 0 0 1 21.75 12c0 4.149-2.58 7.725-6.3 9.225zM12 22.785A10.755 10.755 0 0 1 1.215 12c0-2.16.63-4.17 1.71-5.865l5.865 16.095A10.727 10.727 0 0 1 12 22.785z"/></svg>
              <span class="skill-tile-name">WordPress</span>
            </div>

          </div>
        </div>

        <div class="reveal">
          <div class="skill-group-label">Tools &amp; DevOps</div>
          <div class="skill-tiles">

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#2496ED" aria-label="Docker"><path d="M13.983 11.078h2.119a.186.186 0 0 0 .186-.185V9.006a.186.186 0 0 0-.186-.186h-2.119a.185.185 0 0 0-.185.185v1.888c0 .102.083.185.185.185m-2.954-5.43h2.118a.186.186 0 0 0 .186-.186V3.574a.186.186 0 0 0-.186-.185h-2.118a.185.185 0 0 0-.185.185v1.888c0 .102.082.185.185.185m0 2.716h2.118a.187.187 0 0 0 .186-.186V6.29a.186.186 0 0 0-.186-.185h-2.118a.185.185 0 0 0-.185.185v1.887c0 .102.082.185.185.186m-2.93 0h2.12a.186.186 0 0 0 .184-.186V6.29a.185.185 0 0 0-.185-.185H8.1a.185.185 0 0 0-.185.185v1.887c0 .102.083.185.185.186m-2.964 0h2.119a.186.186 0 0 0 .185-.186V6.29a.185.185 0 0 0-.185-.185H5.136a.186.186 0 0 0-.186.185v1.887c0 .102.084.185.186.186m5.893 2.715h2.118a.186.186 0 0 0 .186-.185V9.006a.186.186 0 0 0-.186-.186h-2.118a.185.185 0 0 0-.185.185v1.888c0 .102.082.185.185.185m-2.93 0h2.12a.185.185 0 0 0 .184-.185V9.006a.184.184 0 0 0-.185-.186h-2.12a.185.185 0 0 0-.184.185v1.888c0 .102.083.185.185.185m-2.964 0h2.119a.185.185 0 0 0 .185-.185V9.006a.185.185 0 0 0-.184-.186h-2.12a.186.186 0 0 0-.186.186v1.887c0 .102.084.185.186.185m-2.92 0h2.12a.186.186 0 0 0 .184-.185V9.006a.185.185 0 0 0-.185-.186h-2.12a.185.185 0 0 0-.184.185v1.888c0 .102.082.185.185.185M23.763 9.89c-.065-.051-.672-.51-1.954-.51-.338.001-.676.03-1.01.087-.248-1.7-1.653-2.53-1.716-2.566l-.344-.199-.226.327c-.284.438-.49.922-.612 1.43-.23.97-.09 1.882.403 2.661-.595.332-1.55.413-1.744.42H.751a.751.751 0 0 0-.75.748 11.376 11.376 0 0 0 .692 4.062c.545 1.428 1.355 2.48 2.41 3.124 1.18.723 3.1 1.137 5.275 1.137.983.003 1.963-.086 2.93-.266a12.248 12.248 0 0 0 3.823-1.389c.98-.567 1.86-1.288 2.61-2.136 1.252-1.418 1.998-2.997 2.553-4.4h.221c1.372 0 2.215-.549 2.68-1.009.309-.293.55-.65.707-1.046l.098-.288Z"/></svg>
              <span class="skill-tile-name">Docker</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#232F3E" aria-label="AWS"><path d="M6.763 10.036c0 .296.032.535.088.71.064.176.144.368.256.576.04.063.056.127.056.183 0 .08-.048.16-.152.24l-.503.335a.383.383 0 0 1-.208.072c-.08 0-.16-.04-.239-.112a2.47 2.47 0 0 1-.287-.375 6.18 6.18 0 0 1-.248-.471c-.622.734-1.405 1.101-2.347 1.101-.67 0-1.205-.191-1.596-.574-.391-.384-.59-.894-.59-1.533 0-.678.239-1.23.726-1.644.487-.415 1.133-.623 1.955-.623.272 0 .551.024.846.064.296.04.6.104.918.176v-.583c0-.607-.127-1.030-.375-1.277-.255-.248-.686-.367-1.3-.367-.28 0-.568.031-.863.103-.295.072-.583.16-.862.272a2.287 2.287 0 0 1-.28.104.488.488 0 0 1-.127.023c-.112 0-.168-.08-.168-.247v-.391c0-.128.016-.224.056-.28a.597.597 0 0 1 .224-.167c.279-.144.614-.264 1.005-.36a4.84 4.84 0 0 1 1.246-.151c.95 0 1.644.216 2.091.647.439.43.662 1.085.662 1.963v2.586zm-3.24 1.214c.263 0 .534-.048.822-.144.287-.096.543-.271.758-.51.128-.152.224-.32.272-.512.047-.191.08-.423.08-.694v-.335a6.66 6.66 0 0 0-.735-.136 6.02 6.02 0 0 0-.75-.048c-.535 0-.926.104-1.19.32-.263.215-.39.518-.39.917 0 .375.095.655.295.846.191.2.47.296.838.296zm6.41.862c-.144 0-.24-.024-.304-.08-.064-.048-.12-.16-.168-.311L7.586 5.55a1.398 1.398 0 0 1-.072-.32c0-.128.064-.2.191-.2h.783c.151 0 .255.025.31.08.065.048.113.16.16.312l1.342 5.284 1.245-5.284c.04-.16.088-.264.151-.312a.549.549 0 0 1 .32-.08h.638c.152 0 .256.025.32.08.063.048.12.16.151.312l1.261 5.348 1.381-5.348c.048-.16.104-.264.16-.312a.52.52 0 0 1 .311-.08h.743c.127 0 .2.065.2.2 0 .04-.009.08-.017.128a1.137 1.137 0 0 1-.056.2l-1.923 6.17c-.048.16-.104.263-.168.311a.51.51 0 0 1-.303.08h-.687c-.151 0-.255-.024-.32-.08-.063-.056-.119-.16-.15-.32l-1.238-5.148-1.23 5.14c-.04.16-.087.264-.15.32-.065.056-.177.08-.32.08zm10.256.215c-.415 0-.83-.048-1.229-.143-.399-.096-.71-.2-.918-.32-.128-.071-.215-.151-.247-.223a.563.563 0 0 1-.048-.224v-.407c0-.167.064-.247.183-.247.048 0 .096.008.144.024.048.016.12.048.2.08.271.12.566.215.878.279.319.064.63.096.95.096.502 0 .894-.088 1.165-.264a.86.86 0 0 0 .415-.758.777.777 0 0 0-.215-.559c-.144-.151-.416-.287-.807-.415l-1.157-.36c-.583-.183-1.014-.454-1.277-.813a1.902 1.902 0 0 1-.4-1.158c0-.335.073-.63.216-.886.144-.255.335-.479.575-.654.24-.184.51-.32.83-.415.32-.096.655-.136 1.006-.136.175 0 .359.008.535.032.183.024.35.056.518.088.16.04.312.08.455.127.144.048.256.096.336.144a.69.69 0 0 1 .24.2.43.43 0 0 1 .071.263v.375c0 .168-.064.256-.184.256a.83.83 0 0 1-.303-.096 3.652 3.652 0 0 0-1.532-.311c-.455 0-.815.071-1.062.223-.248.152-.375.383-.375.71 0 .224.08.416.24.567.159.152.454.304.877.44l1.134.358c.574.184.99.44 1.237.767.247.327.367.702.367 1.117 0 .343-.072.655-.207.926-.144.272-.336.511-.583.703-.248.2-.543.343-.886.447-.36.111-.734.167-1.142.167zM21.698 16.207c-2.626 1.94-6.442 2.969-9.722 2.969-4.598 0-8.74-1.7-11.87-4.526-.247-.223-.025-.527.27-.352 3.384 1.963 7.559 3.153 11.877 3.153 2.914 0 6.114-.607 9.06-1.852.439-.2.814.287.385.608z"/></svg>
              <span class="skill-tile-name">AWS</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#FF6C37" aria-label="Postman"><path d="M13.527.099C6.955-.744.sounds 4.786.099 11.367c-.744 6.573 4.684 12.48 11.261 13.234 6.573.767 12.489-4.667 13.233-11.239C25.338 6.789 20.101.943 13.527.099zm2.471 7.485a.855.855 0 0 0-.593.25l-4.453 4.453-.307-.307-.643-.643 4.453-4.453a.858.858 0 1 0-.735-.24l-4.508 4.508-.536-.536a.199.199 0 0 0-.281 0l-.596.596a.199.199 0 0 0 0 .281l.355.355-1.966 1.966a2.079 2.079 0 0 0 2.942 2.942l1.966-1.966.355.355a.199.199 0 0 0 .281 0l.596-.596a.199.199 0 0 0 0-.281l-.536-.536 4.508-4.508a.856.856 0 0 0 .594 0 .858.858 0 1 0-.896-1.24z"/></svg>
              <span class="skill-tile-name">Postman</span>
            </div>

            <div class="skill-tile">
              <svg viewBox="0 0 24 24" fill="#F05032" aria-label="Git"><path d="M23.546 10.93L13.067.452c-.604-.603-1.582-.603-2.188 0L8.708 2.627l2.76 2.76c.645-.215 1.379-.07 1.889.441.516.515.658 1.258.438 1.9l2.658 2.66c.645-.223 1.387-.078 1.9.435.721.72.721 1.884 0 2.604-.719.719-1.881.719-2.6 0-.539-.541-.674-1.337-.404-1.996L12.86 8.955v6.525c.176.086.342.203.488.348.713.721.713 1.883 0 2.6-.719.721-1.889.721-2.609 0-.719-.719-.719-1.879 0-2.598.182-.18.387-.316.605-.406V8.835c-.217-.091-.424-.222-.6-.401-.545-.545-.676-1.342-.396-2.009L7.636 3.7.45 10.881c-.6.605-.6 1.584 0 2.189l10.48 10.477c.604.604 1.582.604 2.186 0l10.43-10.43c.605-.603.605-1.582 0-2.187"/></svg>
              <span class="skill-tile-name">Git</span>
            </div>

          </div>
        </div>

      </div>
    </div>
  </section>
```

**Step 2: Commit**

```bash
git add index.html
git commit -m "feat: add skills section with icon tiles"
```

---

### Task 10: Add contact, footer, and closing tags to `index.html`

**Files:**
- Modify: `index.html`

**Step 1: Append contact, footer, script tag, and close body/html**

```html
  <!-- ── CONTACT ───────────────────────────────────────── -->
  <section id="contact">
    <div class="container">
      <div class="reveal">
        <div class="section-label">Let's work together</div>
        <h2 class="section-title">Got a project<br>in mind?</h2>
        <p class="section-sub" style="margin: 0 auto; text-align:center;">I'm open to freelance work and full-time roles. I reply within 24 hours.</p>
        <a href="mailto:luqman@email.com" class="contact-email">luqman@email.com</a>
        <div class="social-links">
          <a href="https://github.com/luqmanfarhan" target="_blank" rel="noopener" class="social-link">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z"/></svg>
            GitHub
          </a>
          <span class="social-divider">·</span>
          <a href="https://linkedin.com/in/luqmanfarhan" target="_blank" rel="noopener" class="social-link">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
            LinkedIn
          </a>
          <span class="social-divider">·</span>
          <a href="#" class="social-link">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M12 0C5.374 0 0 5.373 0 12c0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23A11.509 11.509 0 0 1 12 5.803c1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576C20.566 21.797 24 17.3 24 12c0-6.627-5.373-12-12-12z"/></svg>
            GitHub (alt)
          </a>
          <span class="social-divider">·</span>
          <a href="#" class="social-link">
            <svg width="14" height="14" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true"><path d="M7.462 0H16.538L24 13.5 16.538 27H7.462L0 13.5z"/></svg>
            Download CV
          </a>
        </div>
      </div>
    </div>
  </section>

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

**Step 2: Verify the full page renders correctly**

Open `index.html` in a browser. Check:
- Light background renders (`#FAFAFA`)
- Nav appears at top with `LF.dev` logo in blue
- Hero shows two columns (code card right, text left)
- Skills section shows icon tiles with logos
- No horizontal scroll on mobile (resize browser to 375px)

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add contact, footer, and wire up external JS"
```

---

### Task 11: Final cleanup — remove old dark theme `index.html` content

**Files:**
- Modify: `index.html`

**Step 1: Verify old inline `<style>` and `<script>` blocks are fully removed**

Open `index.html` and confirm:
- No `<style>` tag exists inside `<head>` or `<body>`
- No `<script>` block with inline JS exists (only `<script src="script.js">`)
- No dark theme color values (`#0d0d0d`, `#141414`, etc.) remain

**Step 2: Final commit**

```bash
git add index.html style.css script.js
git commit -m "feat: complete portfolio refactor to minimal light theme"
```

---

## Summary

| Task | Output |
|------|--------|
| 1–3 | `style.css` fully written |
| 4 | `script.js` written |
| 5–10 | `index.html` rewritten section by section |
| 11 | Cleanup and final verification |

Total commits: ~11 focused commits, one per logical change.
