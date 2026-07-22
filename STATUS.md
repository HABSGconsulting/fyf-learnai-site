# STATUS.md

Current state of fyf-learnai-site.  
Last updated: 2026-07-22

---

## Current Phase: Phase 0 — Scaffold & First Lesson

### What Is Complete

- [x] Repo created: `HABSGconsulting/fyf-learnai-site` (public)
- [x] Hugo config scaffold (`config.yaml`)
- [x] FYF brand CSS (`assets/css/custom.css`) — ported from fyf-news-site
- [x] Pyodide shortcode (`layouts/shortcodes/pyodide.html`)
- [x] Callout shortcode (`layouts/shortcodes/callout.html`)
- [x] GitHub Actions deploy workflow (`.github/workflows/deploy.yml`)
- [x] All documentation files (docs/01–05)
- [x] `AI-NOTE.md`, `STATUS.md`, `DECISIONS.md`, `README.md`
- [x] Course scaffold: `build-your-own-slm` with 2 full lessons

### What Is Pending

- [ ] Add PaperMod as git submodule locally: `git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod`
- [ ] Set Cloudflare secrets in GitHub repo: `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`
- [ ] Create Cloudflare Pages project pointing to this repo
- [ ] Point `learnai.fundyourfreedom.in` DNS to Cloudflare Pages
- [ ] Verify Pyodide loads correctly in deployed environment
- [ ] Test dark mode rendering with FYF brand CSS
- [ ] Plan and write Lesson 03 onwards

---

## Course Status: Build Your Own Small Language Model

| # | Lesson | Type | Status |
|---|---|---|---|
| 01 | What Is a Language Model? | Explainer | ✅ Written |
| 02 | Build a Probability Distribution | Lab | ✅ Written |
| 03+ | (to be planned) | TBD | ❌ Not started |

---

## Required Secrets (set in GitHub repo Settings → Secrets → Actions)

| Secret | Purpose |
|---|---|
| `CLOUDFLARE_API_TOKEN` | Cloudflare Pages deployment |
| `CLOUDFLARE_ACCOUNT_ID` | Cloudflare account identifier |

---

## Immediate TODO

1. `git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod` locally + push
2. Set the two Cloudflare secrets in repo Settings → Secrets
3. Create Cloudflare Pages project → connect this repo → build command `hugo --minify` → output `public`
4. DNS: add CNAME `learnai` → Cloudflare Pages domain
5. Verify site renders at learnai.fundyourfreedom.in
6. Plan Lesson 03 onwards

---

## Key Decisions Made (see DECISIONS.md)

| # | Decision |
|---|---|
| ADR-001 | Repo is PUBLIC — free GitHub Actions minutes |
| ADR-002 | Pyodide for in-browser Python labs (not Colab redirects) |
| ADR-003 | Hugo PaperMod theme — mirrors fyf-news-site CSS |
| ADR-004 | Separate repo from FYF-learn — AI is its own domain |
| ADR-005 | Content hierarchy: Course → Lesson (numbered folders) |
