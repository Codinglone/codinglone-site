# Portfolio Site Design Spec

**Date:** 2026-05-20  
**Topic:** Minimalist Word-Document Style Portfolio on GitHub Pages  
**Owner:** Fabrice Niyokwizerwa (Codinglone)  
**Status:** Draft — pending review

---

## 1. Overview

A single-page portfolio site deployed on GitHub Pages. The design mimics a Microsoft Word document: pure white background, blue hyperlinks, clean typography, and minimal visual elements. Projects are sourced from two places: (1) a static `projects.json` file for manually added projects, and (2) live GitHub pinned repositories fetched via the public GraphQL API.

### Key Constraints
- GitHub Pages only — no backend, no database, no build step
- Zero external dependencies (no frameworks, no CDNs)
- Must be editable by simply pushing changes to the repo

---

## 2. Architecture

### File Structure
```
portfolio/
├── index.html          # Single page with embedded CSS + JS
├── projects.json       # Custom projects (user-editable)
├── CNAME               # (optional) Custom domain config
└── .github/
    └── workflows/
        └── pages.yml   # (optional) GitHub Actions for Pages
```

### Tech Stack
- **HTML5** — semantic structure
- **CSS3** — embedded in `<style>` tag, no external stylesheets
- **Vanilla JavaScript** — embedded in `<script>` tag, fetches GitHub API + `projects.json`
- **No build tools, no frameworks, no npm**

---

## 3. Components & Layout

### 3.1 Header
- **Name:** Fabrice Niyokwizerwa — large (`28px`), centered, `font-weight: normal`, color `#000`
- **Title:** "Full-Stack AI Engineer | Kigali, Rwanda" — centered, `14px`, color `#666`
- **Social Links:** GitHub, LinkedIn, Email — centered, `14px`, blue underlined links
  - GitHub: `https://github.com/Codinglone`
  - LinkedIn: `https://linkedin.com/in/fabrice-niyokwizerwa` (to be confirmed)
  - Email: `mailto:codinglone@gmail.com`

### 3.2 About
- Heading: "About" — `18px`, color `#2e74b5` (Word heading blue), `font-weight: normal`
- Paragraph: 2-3 sentence bio, left-aligned, `text-align: justify`, `line-height: 1.6`
- Content: "I'm a full-stack AI Engineer based in Rwanda, building systems for languages the world tends to ignore. I work on STT/TTS pipelines and data collection infrastructure for low-resource African languages."

### 3.3 Projects
- Heading: "Featured Projects" — same style as About heading
- Merged list from two sources, displayed as a vertical stack:
  1. GitHub pinned repos (fetched dynamically)
  2. Custom projects from `projects.json` (deduplicated against GitHub repos)
- **Each project card:**
  - Name + language badge (e.g., "SipForge — Python")
  - Description paragraph
  - GitHub link in blue underline

### 3.4 Footer
- Minimal copyright line: "© 2025 — Built with simplicity in mind"
- Centered, `12px`, color `#999`

### 3.5 Dividers
- Horizontal rules (`<hr>`) between major sections
- Style: `border: none; border-top: 1px solid #ccc;`

---

## 4. Data Flow

### 4.1 Source A — `projects.json` (Static)
```json
[
  {
    "name": "Project Name",
    "description": "Brief description of the project.",
    "url": "https://github.com/Codinglone/project-name",
    "language": "Python",
    "pinned": false
  }
]
```
- Fetched via `fetch('projects.json')` on page load
- Stored as raw JSON in the repo
- User adds/edits projects by modifying this file and pushing

### 4.2 Source B — GitHub GraphQL API (Dynamic)
- Endpoint: `https://api.github.com/graphql`
- Query:
```graphql
query {
  user(login: "Codinglone") {
    pinnedItems(first: 6, types: REPOSITORY) {
      nodes {
        ... on Repository {
          name
          description
          url
          stargazerCount
          primaryLanguage { name }
        }
      }
    }
  }
}
```
- **No auth token required** for public repos (uses unauthenticated requests)
- Rate limit: 60 requests/hour per IP (sufficient for a portfolio)

### 4.3 Merge Logic
1. Fetch GitHub pinned repos
2. Fetch `projects.json`
3. Deduplicate: if a `projects.json` entry has the same `url` as a GitHub repo, skip it
4. Render: GitHub repos first (they're "pinned"), then custom projects
5. If GitHub API fails, show only `projects.json` entries with a subtle note
6. If `projects.json` fails, show only GitHub repos
7. If both fail, show a friendly error with social links

---

## 5. Styling — Microsoft Word Document Aesthetic

### Color Palette
| Token | Value | Usage |
|-------|-------|-------|
| `--bg` | `#ffffff` | Page background |
| `--text` | `#333333` | Body text |
| `--heading` | `#2e74b5` | Section headings |
| `--link` | `#0563c1` | Hyperlinks |
| `--link-hover` | `#054d9a` | Link hover state |
| `--muted` | `#666666` | Subtitles, secondary text |
| `--border` | `#cccccc` | Horizontal rules |
| `--footer` | `#999999` | Footer text |

### Typography
| Element | Size | Weight | Color |
|---------|------|--------|-------|
| Name | `28px` | `normal` | `#000` |
| Title | `14px` | `normal` | `#666` |
| Heading | `18px` | `normal` | `#2e74b5` |
| Body | `16px` | `normal` | `#333` |
| Links | `16px` | `normal` | `#0563c1` |
| Footer | `12px` | `normal` | `#999` |

### Layout
- Container: `max-width: 800px`, centered with `margin: 0 auto`
- Padding: `40px` horizontal on desktop, `20px` on mobile
- Font stack: `'Segoe UI', 'Helvetica Neue', Arial, sans-serif`
- Line height: `1.6` for body text

### Responsive Behavior
- On screens `< 600px`: reduce padding to `20px`, name to `24px`
- Links remain underlined (no hover underline reveal — always underlined like Word)

---

## 6. Error Handling

| Scenario | Behavior |
|----------|----------|
| GitHub API rate limited | Show `projects.json` only + subtle gray note: "GitHub projects unavailable — showing saved projects" |
| `projects.json` 404 | Show GitHub repos only |
| Both sources fail | Show friendly message: "Projects loading... In the meantime, find me on [GitHub] and [LinkedIn]." |
| Network timeout | Same as "both fail" — fallback to static content |

---

## 7. Deployment

### GitHub Pages Setup
1. Create a new repo (e.g., `codinglone.github.io` for root domain, or any name for subdirectory)
2. Push `index.html` and `projects.json` to the `main` branch
3. Go to repo Settings → Pages → Source: Deploy from a branch → Select `main`
4. Site live at `https://codinglone.github.io/repo-name/`

### Update Workflow
1. Edit `projects.json` locally
2. `git add projects.json && git commit -m "Add project: X" && git push`
3. GitHub Pages auto-deploys in ~30 seconds
4. No build step, no CI needed

### Optional: Custom Domain
- Add a `CNAME` file with your domain (e.g., `fabrice.dev`)
- Configure DNS A/ALIAS records to GitHub Pages IPs
- Enable HTTPS in repo Settings → Pages

---

## 8. Out of Scope

These are intentionally excluded to keep the portfolio minimal and maintenance-free:
- Dark mode toggle
- Contact form (GitHub Pages has no backend)
- Blog / posts section
- Skills visualization (charts, progress bars)
- Analytics / tracking
- Service Worker / PWA features
- Multiple pages / routing
- Image galleries or screenshots

---

## 9. Acceptance Criteria

- [ ] Site renders as a single page on GitHub Pages
- [ ] White background with blue links matches Word document aesthetic
- [ ] GitHub pinned repos load dynamically on page load
- [ ] `projects.json` entries display alongside GitHub repos
- [ ] Adding a project requires only editing `projects.json` and pushing
- [ ] No external dependencies or build tools
- [ ] Works on mobile (responsive padding and font sizes)
- [ ] Graceful degradation when GitHub API is unavailable
- [ ] All links open in new tab (`target="_blank"`) except email

---

## 10. Open Questions

1. **LinkedIn URL:** The user mentioned LinkedIn — what is the exact profile URL? (Default assumed: `linkedin.com/in/fabrice-niyokwizerwa`)
2. **Custom domain:** Does the user want a custom domain, or is `codinglone.github.io` sufficient?
3. **Resume/CV link:** Should there be a link to download a PDF resume?

These can be resolved during implementation or post-launch.
