# fyf-learnai-site

**FundYourFreedom — AI Learning Platform**  
Site: [learnai.fundyourfreedom.in](https://learnai.fundyourfreedom.in)  
Repo visibility: **Public** (free GitHub Actions minutes)  
Theme: Hugo PaperMod + FYF brand CSS  
Interactive labs: Pyodide (in-browser Python, zero backend)  

---

## What This Is

A Hugo static site that delivers GenZ-framed AI/ML learning content at `learnai.fundyourfreedom.in`.  
Content mirrors Google DeepMind's "Build Your Own Small Language Model" curriculum — same core concepts, redelivered as intuitive, interactive, step-by-step tutorials.

Every lesson is either:
- **Explainer** — concept-first, short bursts, real analogies, zero jargon walls
- **Lab** — live in-browser Python via Pyodide; student runs code directly on the page

---

## Repo Structure

```
fyf-learnai-site/
  assets/css/custom.css          ← FYF brand styles (ported from fyf-news-site)
  layouts/shortcodes/
    pyodide.html                 ← one-time setup; use {{< pyodide id="x" >}} anywhere
    callout.html                 ← "💭 Wait, but why?" callout boxes
  content/courses/
    build-your-own-slm/
      _index.md                  ← course landing page
      01-what-is-a-language-model/index.md    ← explainer
      02-probability-lab/index.md             ← lab (Pyodide)
  docs/                          ← internal project documentation
  .github/workflows/deploy.yml   ← Hugo build → Cloudflare Pages
  config.yaml                    ← Hugo config
  AI-NOTE.md                     ← AI session context primer (read first)
  STATUS.md                      ← current pipeline status + TODO
  DECISIONS.md                   ← architecture decision records
```

---

## Docs Index

| Doc | Topic |
|---|---|
| `docs/01-project-overview.md` | Vision, goals, audience |
| `docs/02-content-architecture.md` | Course/lesson/section structure |
| `docs/03-pyodide-setup.md` | How Pyodide is integrated |
| `docs/04-lesson-authoring-guide.md` | How to write explainer + lab lessons |
| `docs/05-deployment-guide.md` | GitHub Actions → Cloudflare Pages |

---

## Quick Start (local dev)

```bash
git clone --recurse-submodules https://github.com/HABSGconsulting/fyf-learnai-site
cd fyf-learnai-site
hugo server   # visit http://localhost:1313
```

---

## Related Repos

| Repo | Site | Purpose |
|---|---|---|
| [fyf-news-site](https://github.com/HABSGconsulting/fyf-news-site) | news.fundyourfreedom.in | Hugo PaperMod news (CSS donor) |
| [fyf-blog](https://github.com/HABSGconsulting/fyf-blog) | blog.fundyourfreedom.in | Hugo blog |
| [FYF-learn](https://github.com/HABSGconsulting/FYF-learn) | learn.fundyourfreedom.in | Hugo Relearn (finance courses) |
| [fyf-guides-engine](https://github.com/HABSGconsulting/fyf-guides-engine) | guides.fundyourfreedom.in | Astro + content engine |
