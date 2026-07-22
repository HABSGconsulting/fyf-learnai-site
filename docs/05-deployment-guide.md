# 05 — Deployment Guide

## Live URL

**https://aicourses.fundyourfreedom.in**

---

## Architecture

- **Hugo** static site generator (extended, latest)
- **GitHub Actions** for CI/CD (free — public repo)
- **Cloudflare Pages** for hosting
- **Cloudflare DNS** for the subdomain

---

## One-Time Setup (Owner)

### 1. Add GitHub Secrets

Go to: `HABSGconsulting/fyf-learnai-site` → Settings → Secrets → Actions

Add these three secrets:

| Secret | Value |
|---|---|
| `CLOUDFLARE_API_TOKEN` | Cloudflare API token with Pages:Edit permission |
| `CLOUDFLARE_ACCOUNT_ID` | Your Cloudflare account ID |
| `GH_PAT` | GitHub Personal Access Token with `repo` scope *(needed to fetch private `fyf-hugo-theme` submodule)* |

> **Note on GH_PAT:** The default `GITHUB_TOKEN` in Actions only has access to the current repo.
> A PAT is required to fetch the private `fyf-hugo-theme` submodule during CI builds.
> This is the same pattern used in other FYF repos that use private submodules.

### 2. Create Cloudflare Pages Project

1. Cloudflare Dashboard → Pages → Create a project
2. Connect to GitHub → select `HABSGconsulting/fyf-learnai-site`
3. Build settings:
   - Build command: `hugo --minify`
   - Output directory: `public`
4. Deploy

### 3. DNS — Add CNAME

In Cloudflare DNS for `fundyourfreedom.in`:

| Type | Name | Target |
|---|---|---|
| CNAME | `aicourses` | `<your-pages-project>.pages.dev` |

Then in Cloudflare Pages → Custom Domains → add `aicourses.fundyourfreedom.in`.

---

## How Deploys Work

1. Push to `main` branch
2. GitHub Actions triggers `.github/workflows/deploy.yml`
3. Workflow checks out repo + submodules (PaperMod + fyf-hugo-theme) using `GH_PAT`
4. Runs `hugo --minify` → outputs to `public/`
5. Cloudflare Pages action deploys `public/` to the CDN
6. Live in ~60 seconds

---

## Build Notes

- Hugo version: `latest` (extended required for SCSS)
- Submodules: two — `themes/PaperMod` (public) and `themes/fyf-hugo-theme` (private, needs GH_PAT)
- No npm, no node_modules — Hugo-only build, fast and clean
