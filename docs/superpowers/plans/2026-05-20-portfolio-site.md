# Portfolio Site Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a single-page portfolio on GitHub Pages with a Microsoft Word document aesthetic, fetching projects from both GitHub pinned repos and a local `projects.json`.

**Architecture:** A single `index.html` with embedded CSS and vanilla JavaScript. No build tools, no frameworks, no dependencies. Deployed via GitHub Pages.

**Tech Stack:** HTML5, CSS3, JavaScript (ES6+). GitHub Pages for hosting.

---

## File Structure

```
/home/codinglone/Documents/projects/codinglone-site/
├── index.html          # Single page: structure + styles + scripts
├── projects.json       # Custom projects (user-editable)
├── CNAME               # Custom domain pointer (optional)
└── README.md           # Repo documentation
```

---

### Task 1: Create `projects.json` with Pinned + Custom Projects

**Files:**
- Create: `projects.json`

- [ ] **Step 1: Write `projects.json`**

Pre-populated with pinned repos fetched via GH CLI, plus slots for custom projects:

```json
[
  {
    "name": "sonic-gate",
    "description": "CLI-first deterministic audio/video quality gate. Catches corrupted, invalid, or low-quality media before it reaches humans.",
    "url": "https://github.com/Codinglone/sonic-gate",
    "language": "Python",
    "pinned": true
  },
  {
    "name": "aether",
    "description": "Local-first, Linux-native computer-use agent with optional cloud vision.",
    "url": "https://github.com/Codinglone/aether",
    "language": "Python",
    "pinned": true
  },
  {
    "name": "mcp-context-bridge",
    "description": "A unified context layer that connects your local data — repositories, documents, remote machines, and notes — to LLM interfaces through the Model Context Protocol (MCP).",
    "url": "https://github.com/Codinglone/mcp-context-bridge",
    "language": "Python",
    "pinned": true
  },
  {
    "name": "SipForge",
    "description": "A distributed voice communication platform that integrates Asterisk telephony with AI-powered chatbots for English and Kinyarwanda languages.",
    "url": "https://github.com/Codinglone/SipForge",
    "language": "Python",
    "pinned": true
  },
  {
    "name": "Kivu Ride",
    "description": "A ride-hailing platform for iOS and Android with a FastAPI backend, React admin dashboard, and Expo mobile app. Features JWT auth, trip-matching, and DigitalOcean Spaces storage.",
    "url": "https://github.com/Codinglone/kivu-ride",
    "language": "Python / TypeScript",
    "pinned": false
  },
  {
    "name": "Lidata",
    "description": "A digital life assistant with FastAPI backend, Beanie ODM for MongoDB, and live PayPal webhook integration for subscription management.",
    "url": "https://github.com/Codinglone/lidata",
    "language": "Python",
    "pinned": false
  }
]
```

- [ ] **Step 2: Verify JSON validity**

Run: `python3 -m json.tool projects.json > /dev/null && echo "Valid JSON"`

Expected: `Valid JSON`

---

### Task 2: Write `index.html` — HTML Structure

**Files:**
- Create: `index.html`

- [ ] **Step 1: Write the HTML skeleton with header, about, projects section, and footer**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Fabrice Niyokwizerwa — Portfolio</title>
  <style>
    /* CSS will go here in Task 3 */
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>Fabrice Niyokwizerwa</h1>
      <p class="subtitle">Full-Stack AI Engineer | Kigali, Rwanda</p>
      <p class="socials">
        <a href="https://github.com/Codinglone" target="_blank">GitHub</a>
        <span class="sep">|</span>
        <a href="https://linkedin.com/in/fabrice-niyokwizerwa" target="_blank">LinkedIn</a>
        <span class="sep">|</span>
        <a href="mailto:codinglone@gmail.com">Email</a>
      </p>
    </header>

    <hr>

    <section id="about">
      <h2>About</h2>
      <p>
        I'm a full-stack AI Engineer based in Rwanda, building systems for languages the world tends to ignore.
        By day, I work on STT/TTS pipelines and data collection infrastructure for low-resource African languages
        at Digital Umuganda — fine-tuning speech models, shipping inference systems in production, and solving
        problems most engineers never encounter. Off the clock, I tinker with distributed systems, low-level code,
        and AI experiments. I approach everything with curiosity, humor, and a systems-oriented mindset.
      </p>
    </section>

    <section id="projects">
      <h2>Featured Projects</h2>
      <div id="projects-list">
        <p class="loading">Loading projects...</p>
      </div>
    </section>

    <hr>

    <footer>
      <p>&copy; 2025 — Built with simplicity in mind</p>
    </footer>
  </div>

  <script>
    /* JavaScript will go here in Task 4 */
  </script>
</body>
</html>
```

- [ ] **Step 2: Verify HTML structure**

Run: `python3 -c "from html.parser import HTMLParser; p=HTMLParser(); p.feed(open('index.html').read()); print('Valid HTML')"`

Expected: `Valid HTML`

---

### Task 3: Add CSS — Microsoft Word Document Aesthetic

**Files:**
- Modify: `index.html` (replace the `<style>` placeholder)

- [ ] **Step 1: Write the CSS block**

Replace the `<style>` placeholder with:

```html
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      background-color: #ffffff;
      color: #333333;
      font-family: 'Segoe UI', 'Helvetica Neue', Arial, sans-serif;
      font-size: 16px;
      line-height: 1.6;
      -webkit-font-smoothing: antialiased;
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 40px 20px;
    }

    header {
      text-align: center;
      margin-bottom: 30px;
    }

    header h1 {
      font-size: 28px;
      font-weight: normal;
      color: #000000;
      margin-bottom: 5px;
    }

    .subtitle {
      color: #666666;
      font-size: 14px;
      margin-bottom: 8px;
    }

    .socials {
      font-size: 14px;
    }

    .socials .sep {
      color: #999999;
      margin: 0 6px;
    }

    a {
      color: #0563c1;
      text-decoration: underline;
    }

    a:hover {
      color: #054d9a;
    }

    hr {
      border: none;
      border-top: 1px solid #cccccc;
      margin: 25px 0;
    }

    section {
      margin-bottom: 25px;
    }

    h2 {
      font-size: 18px;
      font-weight: normal;
      color: #2e74b5;
      margin-bottom: 12px;
    }

    p {
      text-align: justify;
      margin-bottom: 12px;
    }

    .loading {
      color: #666666;
      font-style: italic;
      text-align: left;
    }

    .error-note {
      color: #666666;
      font-size: 14px;
      font-style: italic;
      text-align: left;
    }

    .project {
      margin-bottom: 20px;
    }

    .project-header {
      font-weight: 600;
      color: #000000;
      margin-bottom: 4px;
    }

    .project-lang {
      color: #666666;
      font-weight: normal;
    }

    .project-desc {
      color: #555555;
      margin-bottom: 6px;
      text-align: justify;
    }

    .project-link {
      font-size: 14px;
    }

    footer {
      text-align: center;
      color: #999999;
      font-size: 12px;
      margin-top: 20px;
    }

    @media (max-width: 600px) {
      .container {
        padding: 20px 16px;
      }

      header h1 {
        font-size: 24px;
      }
    }
  </style>
```

- [ ] **Step 2: Verify CSS is well-formed**

Open `index.html` in a text editor and confirm the `<style>` block is complete and closed with `</style>`.

---

### Task 4: Add JavaScript — Fetch and Render `projects.json`

**Files:**
- Modify: `index.html` (replace the `<script>` placeholder)

- [ ] **Step 1: Write the JavaScript block**

Replace the `<script>` placeholder with:

```html
  <script>
    (async function() {
      const container = document.getElementById('projects-list');

      function createProjectCard(repo) {
        const lang = repo.language || 'N/A';
        return `
          <div class="project">
            <p class="project-header">${escapeHtml(repo.name)} <span class="project-lang">— ${escapeHtml(lang)}</span></p>
            <p class="project-desc">${escapeHtml(repo.description || 'No description provided.')}</p>
            <p><a href="${escapeHtml(repo.url)}" target="_blank" class="project-link">View on GitHub &rarr;</a></p>
          </div>
        `;
      }

      function escapeHtml(text) {
        if (!text) return '';
        const div = document.createElement('div');
        div.textContent = text;
        return div.innerHTML;
      }

      try {
        const response = await fetch('projects.json');
        if (!response.ok) {
          throw new Error('Failed to load projects.json');
        }
        const projects = await response.json();

        if (!Array.isArray(projects) || projects.length === 0) {
          throw new Error('No projects found');
        }

        container.innerHTML = projects.map(createProjectCard).join('');
      } catch (e) {
        console.warn('Projects load failed:', e);
        container.innerHTML = `
          <p class="error-note">
            Projects loading... In the meantime, find me on
            <a href="https://github.com/Codinglone" target="_blank">GitHub</a> and
            <a href="https://linkedin.com/in/fabrice-niyokwizerwa" target="_blank">LinkedIn</a>.
          </p>
        `;
      }
    })();
  </script>
```

- [ ] **Step 2: Verify JavaScript syntax**

Run: `node -c <(sed -n '/<script>/,/<\/script>/p' index.html | sed 's/<script>//' | sed 's/<\/script>//')`

Expected: `SyntaxError` should NOT appear. If `node` isn't available, visually inspect the script for balanced braces and quotes.

---

### Task 5: Write `README.md`

**Files:**
- Create: `README.md`

- [ ] **Step 1: Write README**

```markdown
# Fabrice Niyokwizerwa — Portfolio

A minimal, Microsoft Word-inspired portfolio hosted on GitHub Pages.

**Live site:** https://codinglone.github.io/codinglone-site/

## How to Add a Project

1. Open `projects.json`
2. Add a new object to the array:
   ```json
   {
     "name": "Your Project",
     "description": "What it does.",
     "url": "https://github.com/Codinglone/your-project",
     "language": "Python",
     "pinned": false
   }
   ```
3. Commit and push — GitHub Pages auto-deploys in ~30 seconds.

## Features

- Displays projects from `projects.json` (includes your pinned repos pre-populated)
- Add new projects by editing `projects.json` — no code changes needed
- Zero dependencies, zero build steps
- Responsive, Word-document aesthetic

## Tech Stack

- HTML5 + CSS3 + Vanilla JavaScript
- GitHub Pages
```

---

### Task 6: Local Verification

**Files:**
- Read: `index.html`

- [ ] **Step 1: Verify file completeness**

Run: `grep -c '<style>' index.html && grep -c '</style>' index.html && grep -c '<script>' index.html && grep -c '</script>' index.html`

Expected: Each command returns `1` (exactly one opening and closing tag for each).

- [ ] **Step 2: Serve locally and check in browser**

Run: `python3 -m http.server 8080 &`

Open `http://localhost:8080` in a browser and verify:
- [ ] Page background is white
- [ ] Name is centered at top
- [ ] Links are blue and underlined
- [ ] All projects from `projects.json` display correctly
- [ ] Pinned repos (sonic-gate, aether, mcp-context-bridge, SipForge) appear
- [ ] Custom projects (Kivu Ride, Lidata) appear
- [ ] No console errors
- [ ] Layout looks clean on mobile (use DevTools device mode)

- [ ] **Step 3: Kill local server**

Run: `pkill -f "python3 -m http.server 8080"`

---

### Task 7: Git Setup and Initial Commit

**Files:**
- All files in the repo

- [ ] **Step 1: Initialize git (if not already)**

Run: `git init`

Expected: `Initialized empty Git repository...` (or `Reinitialized...`)

- [ ] **Step 2: Add `.gitignore`**

Create `.gitignore`:
```
.superpowers/
```

- [ ] **Step 3: Stage and commit**

Run:
```bash
git add index.html projects.json README.md .gitignore
git commit -m "feat: add minimal portfolio site with Word aesthetic

- Single-page portfolio on GitHub Pages
- Microsoft Word document styling (white bg, blue links)
- Pre-populated projects.json with GitHub pinned repos
- Add projects dynamically by editing projects.json
- Zero dependencies, zero build step"
```

Expected: Commit succeeds with no errors.

---

## Spec Coverage Check

| Spec Requirement | Task |
|------------------|------|
| Single-page portfolio | Task 2 |
| GitHub Pages deployment | Task 7 |
| Word-document aesthetic (white bg, blue links) | Task 3 |
| GitHub pinned repos pre-populated in `projects.json` | Task 1 |
| `projects.json` for dynamic project additions | Task 1, Task 4 |
| No dependencies / build tools | All tasks |
| Mobile responsive | Task 3 (media query) |
| Graceful degradation | Task 4 (try/catch + fallback) |
| README with instructions | Task 5 |

## Placeholder Scan

- [x] No "TBD" or "TODO" in code
- [x] No vague "handle errors" — explicit try/catch blocks
- [x] No "similar to Task N" — each task is self-contained
- [x] All file paths are exact
- [x] All code blocks contain complete, runnable code

## Type Consistency

- [x] `repo.language` is the single source of truth (no GraphQL `primaryLanguage` nesting)
- [x] `projects.json` schema: `{ name, description, url, language, pinned }`
- [x] JS reads array directly from `projects.json` — no merge logic needed

---

## Execution Handoff

**Plan saved to:** `docs/superpowers/plans/2026-05-20-portfolio-site.md`

**Execution options:**

1. **Subagent-Driven (recommended)** — I dispatch a fresh subagent per task, review between tasks, fast iteration
2. **Inline Execution** — Execute tasks in this session batch-style with checkpoints

**Which approach?**
