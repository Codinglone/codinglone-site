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
