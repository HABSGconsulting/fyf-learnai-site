# 05 — Deployment Guide

## Architecture

```
Push to main branch
  → GitHub Actions (deploy.yml)
    → Hugo build (hugo --minify)
      → Cloudflare Pages deploy
        → learnai.fundyourfreedom.in live
```

## One-Time Setup

### 1. Add PaperMod Theme (run locally once)
```bash
git clone --recurse-submodules https://github.com/HABSGconsulting/fyf-learnai-site
cd fyf-learnai-site
git submodule add https://github.com/adityatelange/hugo-PaperMod themes/PaperMod
git commit -m "add PaperMod theme as submodule"
git push
```

### 2. Create Cloudflare Pages Project
- Cloudflare Dashboard → Pages → Create a project
- Connect to GitHub → select `HABSGconsulting/fyf-learnai-site`
- Build settings:
  - Framework: Hugo
  - Build command: `hugo --minify`
  - Build output: `public`
- Deploy

### 3. Set GitHub Secrets
Repo Settings → Secrets and variables → Actions → New repository secret:

| Secret | Where to get it |
|---|---|
| `CLOUDFLARE_API_TOKEN` | Cloudflare Dashboard → My Profile → API Tokens → Create token (Cloudflare Pages: Edit) |
| `CLOUDFLARE_ACCOUNT_ID` | Cloudflare Dashboard → right sidebar on any page |

### 4. DNS — Point the Subdomain
In Cloudflare DNS for `fundyourfreedom.in`:
- Add CNAME: `learnai` → your Cloudflare Pages domain (e.g. `fyf-learnai-site.pages.dev`)
- Proxy status: ON (orange cloud)

## Ongoing Deployment

Every push to `main` automatically:
1. Triggers GitHub Actions (free — public repo)
2. Builds Hugo site (~5–15 seconds)
3. Deploys to Cloudflare Pages
4. Site live within ~60 seconds of push

## Local Dev

```bash
git clone --recurse-submodules https://github.com/HABSGconsulting/fyf-learnai-site
cd fyf-learnai-site
hugo server   # visit http://localhost:1313
```

`hugo server` hot-reloads on every file save — no refresh needed.
