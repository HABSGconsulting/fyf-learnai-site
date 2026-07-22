# STATUS.md

Current state of fyf-learnai-site.  
Last updated: 2026-07-22

---

## Live URL

**https://aicourses.fundyourfreedom.in**

---

## Current Phase: Phase 1 — Content (Course 1 in progress)

### Infrastructure: Complete ✅

- [x] Repo: `HABSGconsulting/fyf-learnai-site` (public)
- [x] Hugo config (`config.yaml`) — dual theme cascade: PaperMod + fyf-hugo-theme
- [x] `fyf-hugo-theme` private submodule wired — course layouts, shortcodes, brand CSS all live there
- [x] `assets/css/custom.css` — site-specific overrides only (minimal)
- [x] GitHub Actions deploy workflow — uses `GH_PAT` to fetch private submodule
- [x] All documentation files (`docs/01`–`05`)
- [x] `AI-NOTE.md`, `STATUS.md`, `DECISIONS.md`, `README.md`
- [x] `.gitmodules` — PaperMod + fyf-hugo-theme submodules declared

### Pending (One-Time — Owner Action)

- [ ] GitHub repo Settings → Secrets: add `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`
- [ ] GitHub repo Settings → Secrets: add `GH_PAT` (repo-scoped PAT — needed for private fyf-hugo-theme submodule)
- [ ] Create Cloudflare Pages project → connect repo → build `hugo --minify` → output `public`
- [ ] DNS: CNAME `aicourses` → Cloudflare Pages domain  *(was: learnai)*

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

## Course 2: Using AI with Python

Status: **Stub created** — structure ready, content not yet written.

| # | Lesson | Type | Status |
|---|---|---|---|
| 01 | What Is AI and Why Python? | Explainer | 🔲 Stub only |
| 02+ | (to be planned) | TBD | ❌ Not started |

---

## Immediate TODO (AI)

1. Continue adding lessons for Course 1 as Google course content is shared
2. Plan and write Course 2 lessons when directed
3. `list.html` auto-renders both course indexes — no manual HTML needed
4. Update this STATUS.md lesson tables with each new lesson

---

## Key Decisions (see DECISIONS.md)

| # | Decision |
|---|---|
| ADR-001 | Repo is PUBLIC — free GitHub Actions minutes |
| ADR-002 | Pyodide for in-browser Python labs |
| ADR-003 | Hugo PaperMod base theme + fyf-hugo-theme override |
| ADR-004 | Separate repo from FYF-learn — AI courses is its own domain |
| ADR-005 | Content hierarchy: Course → Lesson (numbered folders) |
| ADR-006 | Shared theme repo `fyf-hugo-theme` (private submodule) |
| ADR-007 | Private submodule via GH_PAT |
| ADR-008 | Subdomain: aicourses.fundyourfreedom.in |
