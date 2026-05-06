# Favicon Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add LF logo as browser tab favicon to all 5 portfolio HTML pages.

**Architecture:** Insert a single `<link rel="icon">` tag into the `<head>` of each HTML file, referencing the existing `logo_lf.png` at the project root.

**Tech Stack:** Static HTML, PNG image

---

### Task 1: Add favicon to index.html

**Files:**
- Modify: `index.html:10` (after last `<link>` in `<head>`)

**Step 1: Add favicon link tag**

Insert after line 10 (after the devicons stylesheet link):

```html
  <link rel="icon" type="image/png" href="logo_lf.png" />
```

**Step 2: Verify in browser**

Open `index.html` in browser. Check browser tab shows LF logo.

**Step 3: Commit**

```bash
git add index.html
git commit -m "feat: add LF favicon to index.html"
```

---

### Task 2: Add favicon to mediviron.html

**Files:**
- Modify: `mediviron.html` (inside `<head>`)

**Step 1: Find last `<link>` tag in `<head>` of mediviron.html, insert after it:**

```html
  <link rel="icon" type="image/png" href="logo_lf.png" />
```

**Step 2: Commit**

```bash
git add mediviron.html
git commit -m "feat: add LF favicon to mediviron.html"
```

---

### Task 3: Add favicon to senada.html

**Files:**
- Modify: `senada.html` (inside `<head>`)

**Step 1: Find last `<link>` tag in `<head>` of senada.html, insert after it:**

```html
  <link rel="icon" type="image/png" href="logo_lf.png" />
```

**Step 2: Commit**

```bash
git add senada.html
git commit -m "feat: add LF favicon to senada.html"
```

---

### Task 4: Add favicon to smartschool.html

**Files:**
- Modify: `smartschool.html` (inside `<head>`)

**Step 1: Find last `<link>` tag in `<head>` of smartschool.html, insert after it:**

```html
  <link rel="icon" type="image/png" href="logo_lf.png" />
```

**Step 2: Commit**

```bash
git add smartschool.html
git commit -m "feat: add LF favicon to smartschool.html"
```

---

### Task 5: Add favicon to project.html

**Files:**
- Modify: `project.html` (inside `<head>`)

**Step 1: Find last `<link>` tag in `<head>` of project.html, insert after it:**

```html
  <link rel="icon" type="image/png" href="logo_lf.png" />
```

**Step 2: Commit**

```bash
git add project.html
git commit -m "feat: add LF favicon to project.html"
```
