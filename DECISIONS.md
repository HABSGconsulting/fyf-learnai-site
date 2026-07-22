# Architecture Decision Records

This file records significant technical decisions made during the development of fyf-learnai-site.

---

## ADR-001 — Repo Is Public (Free GitHub Actions Minutes)

**Date:** 2026-07-22  
**Status:** Accepted

### Context
Deploying to Cloudflare Pages via GitHub Actions requires CI minutes. Private repos consume the free quota (2,000 min/month on free plan). The content in this repo is educational and public-facing anyway.

### Decision
Repo is **public**. This gives unlimited free GitHub Actions minutes. All secrets (Cloudflare tokens) are stored in GitHub repo Secrets — never in code. Nothing sensitive is in this repo.

---

## ADR-002 — Pyodide for In-Browser Python Labs

**Date:** 2026-07-22  
**Status:** Accepted

### Options Considered

| Option | Pros | Cons | Decision |
|---|---|---|---|
| Google Colab link-out | Zero setup | Leaves the site; breaks flow | Rejected |
| Embedded Colab iframe | Stays on page | Auth wall, not mobile friendly | Rejected |
| Pyodide (in-browser Python) | Runs on page, no backend, cacheable | ~10MB first load | **Accepted** |

### Decision
Use Pyodide loaded from CDN. Implemented as a single Hugo shortcode (`layouts/shortcodes/pyodide.html`). Set up once — usable on every lesson page forever. Students never leave `learnai.fundyourfreedom.in`.

---

## ADR-003 — Hugo PaperMod Theme (Mirroring fyf-news-site)

**Date:** 2026-07-22  
**Status:** Accepted

### Decision
Use Hugo PaperMod — the same theme as `fyf-news-site`. The `custom.css` from fyf-news-site is ported directly: Inter + Source Serif 4 fonts, FYF navy/amber palette, dark mode variables. This gives brand consistency across the FYF network with zero extra design work.

---

## ADR-004 — Separate Repo from FYF-learn

**Date:** 2026-07-22  
**Status:** Accepted

### Context
`FYF-learn` (private) serves `learn.fundyourfreedom.in` with Hugo Relearn theme for finance courses. The new AI curriculum is going to `learnai.fundyourfreedom.in`.

### Decision
Separate repo (`fyf-learnai-site`). AI education is a distinct, long-term domain — it needs its own space, its own deployment pipeline, its own content architecture, and room to grow independently of the finance learning content.

---

## ADR-005 — Content Architecture: Course → Lesson (Numbered Folders)

**Date:** 2026-07-22  
**Status:** Accepted

### Decision
Content hierarchy:
- `content/courses/{course-slug}/` — one folder per course
- `content/courses/{course-slug}/{NN-lesson-slug}/index.md` — one folder per lesson (numbered for order)
- Each lesson has `type: explainer` or `type: lab` in front matter
- Hugo's `weight` param controls lesson sequence
- `ShowPostNavLinks: true` in PaperMod gives automatic "← Previous | Next →" navigation

This mirrors the fyf-news-site pattern and renders as a naturally linked step-by-step tutorial on the site.
