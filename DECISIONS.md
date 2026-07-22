# Architecture Decision Records

This file records significant technical decisions made during the development of fyf-learnai-site.

---

## ADR-001 — Repo Is Public (Free GitHub Actions Minutes)

**Date:** 2026-07-22  
**Status:** Accepted

### Decision
Repo is **public**. Unlimited free GitHub Actions minutes. All secrets stored in GitHub repo Secrets — never in code.

---

## ADR-002 — Pyodide for In-Browser Python Labs

**Date:** 2026-07-22  
**Status:** Accepted

### Decision
Use Pyodide from CDN. Implemented as a Hugo shortcode in `fyf-hugo-theme`. Set up once — usable on every lesson page. Students never leave `learnai.fundyourfreedom.in`.

---

## ADR-003 — Hugo PaperMod Theme (Base)

**Date:** 2026-07-22  
**Status:** Accepted

### Decision
Use Hugo PaperMod as the base theme. FYF-specific overrides live in `fyf-hugo-theme` (loaded second in theme cascade, wins on conflicts).

---

## ADR-004 — Separate Repo from FYF-learn

**Date:** 2026-07-22  
**Status:** Accepted

### Decision
Separate repo (`fyf-learnai-site`). AI education is a distinct, long-term domain — its own space, pipeline, content architecture, and growth trajectory.

---

## ADR-005 — Content Architecture: Course → Lesson (Numbered Folders)

**Date:** 2026-07-22  
**Status:** Accepted

### Decision
Content hierarchy: `content/courses/{course-slug}/{NN-lesson-slug}/index.md`. Hugo `weight` + `lessonNumber` params control ordering. `ShowPostNavLinks: true` gives automatic prev/next navigation.

---

## ADR-006 — Shared Theme Repo (`fyf-hugo-theme`)

**Date:** 2026-07-22  
**Status:** Accepted

### Context
Audit (2026-07-22) found that shortcodes, CSS, and course layouts were duplicated inside `fyf-learnai-site`. As more tutorial sites are added to the FYF network, this would require maintaining the same code in multiple repos.

### Decision
Extract all reusable theme code into a **private** shared repo: `HABSGconsulting/fyf-hugo-theme`. Each tutorial site declares it as a git submodule alongside PaperMod. Hugo's theme cascade loads it second, so it overrides PaperMod where needed.

### What Lives in fyf-hugo-theme
- `layouts/courses/list.html` — auto course index (no manual HTML)
- `layouts/courses/single.html` — lesson page (no blog meta)
- `layouts/partials/lesson-badge.html` — type badge logic
- `layouts/shortcodes/pyodide.html`, `callout.html`, `quiz.html`
- `assets/css/base.css`, `course.css`, `pyodide.css`, `callout.css`

### What Stays in Site Repo
- `content/` — all lesson content
- `config.yaml` — site config including `pyodideVersion` param
- `assets/css/custom.css` — site-specific overrides only (kept minimal)

---

## ADR-007 — Private Submodule via GH_PAT

**Date:** 2026-07-22  
**Status:** Accepted

### Context
`fyf-hugo-theme` is private (protects FYF brand CSS and layout IP). GitHub Actions `GITHUB_TOKEN` only accesses the current repo. A PAT is needed to fetch private submodules in CI.

### Decision
Add `GH_PAT` secret to `fyf-learnai-site` (and any future tutorial site repos). This is the same pattern used in `fyf-guides-engine` / `fyf-guides-runner`. The PAT needs `repo` scope. Set once, never needs updating unless rotated.

### Required Secret
`GH_PAT` — Personal Access Token with `repo` scope.
Set in: repo Settings → Secrets → Actions.
