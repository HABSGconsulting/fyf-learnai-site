# STATUS.md

Current state of fyf-learnai-site.  
Last updated: 2026-07-22

---

## Current Phase: Phase 1 — Content (Course 1 in progress)

### Infrastructure: Complete

- [x] Repo created: `HABSGconsulting/fyf-learnai-site` (public)
- [x] Hugo config (`config.yaml`) — hideMeta true, tutorial mode
- [x] FYF brand CSS (`assets/css/custom.css`) — blog meta hidden, course-index styles, lesson-row layout
- [x] Pyodide shortcode (`layouts/shortcodes/pyodide.html`)
- [x] Callout shortcode (`layouts/shortcodes/callout.html`)
- [x] GitHub Actions deploy workflow (`.github/workflows/deploy.yml`)
- [x] All documentation files (`docs/01`–`05`)
- [x] `AI-NOTE.md`, `STATUS.md`, `DECISIONS.md`, `README.md`
- [x] `.gitmodules` — PaperMod submodule declared (fetched automatically by CI)

### Pending (One-Time — Owner Action)

- [ ] GitHub repo Settings → Secrets: add `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`
- [ ] Create Cloudflare Pages project → connect repo → build `hugo --minify` → output `public`
- [ ] DNS: CNAME `learnai` → Cloudflare Pages domain

---

## Course 1: Build Your Own Small Language Model

Source: Google DeepMind — https://www.skills.google/course_templates/1341

| # | Lesson | Type | Status |
|---|---|---|---|
| 01 | What Is a Language Model? | Explainer | ✅ Written |
| 02 | Lab: Build a Probability Distribution | Lab | ✅ Written |
| 03 | Reflect on Your Findings | Reflection | ✅ Written |
| 04+ | (next — per Google course) | TBD | ❌ Not started |

---

## Immediate TODO (AI)

1. Continue adding lessons as Google course content is shared
2. Update course `_index.md` lesson index with each new lesson
3. Update this STATUS.md lesson table with each new lesson

---

## Key Decisions (see DECISIONS.md)

| # | Decision |
|---|---|
| ADR-001 | Repo is PUBLIC — free GitHub Actions minutes |
| ADR-002 | Pyodide for in-browser Python labs |
| ADR-003 | Hugo PaperMod — mirrors fyf-news-site CSS |
| ADR-004 | Separate repo from FYF-learn — AI is its own domain |
| ADR-005 | Content hierarchy: Course → Lesson (numbered folders) |
| ADR-006 | Tutorial mode: hideMeta=true, manual course index in _index.md |
