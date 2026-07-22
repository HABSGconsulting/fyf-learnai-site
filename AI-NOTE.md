# AI-NOTE.md

Context primer for AI assistants resuming work on this project.  
**Read this file first. Then read STATUS.md. Then read the relevant doc.**

---

## What This Project Is

`fyf-learnai-site` is the Hugo static site for `learnai.fundyourfreedom.in` —  
FundYourFreedom's dedicated AI learning platform. It is a **separate, long-term domain**,  
not a subsection of learn.fundyourfreedom.in.

Content is GenZ-reframed versions of Google DeepMind's AI/ML curriculum  
(starting with "Build Your Own Small Language Model"). Same core concepts,  
delivered as intuitive, interactive, step-by-step tutorials.

---

## Architecture at a Glance

| Layer | Choice | Reason |
|---|---|---|
| Static site generator | Hugo | Existing FYF stack |
| Theme | PaperMod | Same as fyf-news-site (CSS already tuned) |
| Brand CSS | `assets/css/custom.css` | Ported directly from fyf-news-site |
| Interactive labs | Pyodide (in-browser Python) | Set up once via shortcode, works on every lesson forever |
| Deployment | GitHub Actions → Cloudflare Pages | Repo is PUBLIC = free Actions minutes |
| Hosting | Cloudflare Pages | Existing FYF infra |

---

## The Two Lesson Types

### Explainer (`type: explainer` in front matter)
- Concept-first, short paragraphs, real-world analogies
- GenZ tone: direct, curious, no jargon walls
- Uses `{{< callout >}}` shortcode for "💭 Wait, but why?" boxes
- No code execution required

### Lab (`type: lab` in front matter)
- Students write and run Python directly in the browser (Pyodide)
- Uses `{{< pyodide id="unique-id" >}}` shortcode
- Includes a short explainer intro, then the interactive cell, then a reflection prompt
- Never links out to Colab — everything stays on learnai.fundyourfreedom.in

---

## Key Files

| File | Purpose |
|---|---|
| `config.yaml` | Hugo config, baseURL, PaperMod params |
| `assets/css/custom.css` | FYF brand CSS (Inter + Source Serif 4, navy/amber palette) |
| `layouts/shortcodes/pyodide.html` | Pyodide interactive Python cell — set once, use everywhere |
| `layouts/shortcodes/callout.html` | Callout boxes for explainer lessons |
| `content/courses/` | All course content lives here |
| `docs/` | Internal project documentation |
| `.github/workflows/deploy.yml` | Build + deploy to Cloudflare Pages |

---

## Pyodide — Critical Notes

- Pyodide loads from CDN: `https://cdn.jsdelivr.net/pyodide/v0.27.0/full/pyodide.js`
- First page load is ~10MB (browser caches after that)
- Each `{{< pyodide id="x" >}}` cell is independent — no shared state between cells
- Supported: all Python standard library (collections, random, json, re, math, itertools)
- NOT supported: file I/O, network requests from within Pyodide cells
- To add numpy: `await py.loadPackage("numpy")` — see `docs/03-pyodide-setup.md`

---

## Content Source

Google DeepMind course: "Build Your Own Small Language Model"  
URL: https://www.skills.google/course_templates/1341  
Module 1 (explainer): https://www.skills.google/paths/3135/course_templates/1341/html_bundles/597240  
Module 2 (lab): https://www.skills.google/paths/3135/course_templates/1341/html_bundles/597241  

Approach: Same core concepts, redelivered with:
- GenZ tone (no jargon walls, direct, real analogies)
- Spotify / autocomplete / Reddit analogies (not dry academic examples)
- Live runnable code on every lab lesson
- "💭 Wait, but why?" callout boxes to pre-answer confusion

---

## Deployment

1. Push to `main` branch
2. GitHub Actions runs `deploy.yml` (free — public repo)
3. Hugo builds `public/`
4. Cloudflare Pages deploys to `learnai.fundyourfreedom.in`

Required GitHub secrets: `CLOUDFLARE_API_TOKEN` + `CLOUDFLARE_ACCOUNT_ID`  
See `docs/05-deployment-guide.md` for full setup.

---

## What To Do If Resuming

1. Read `STATUS.md` — check Immediate TODO
2. Run `hugo server` locally to verify build
3. Check `content/courses/build-your-own-slm/` for lesson status
4. Author next lesson per `docs/04-lesson-authoring-guide.md`
5. Push to `main` — deploy is automatic

---

## Docs Index

| Doc | Topic |
|---|---|
| `docs/01-project-overview.md` | Vision, goals, audience |
| `docs/02-content-architecture.md` | Course/lesson/section structure |
| `docs/03-pyodide-setup.md` | How Pyodide is integrated |
| `docs/04-lesson-authoring-guide.md` | How to write explainer + lab lessons |
| `docs/05-deployment-guide.md` | GitHub Actions → Cloudflare Pages |
