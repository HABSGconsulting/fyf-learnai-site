# 05 — Deployment Guide

## How the Theme Works (No Local Step Needed)

Hugo PaperMod is declared as a **git submodule** in `.gitmodules`:

```
[submodule "themes/PaperMod"]
    path = themes/PaperMod
    url = https://github.com/adityatelange/hugo-PaperMod.git
    branch = master
```

When GitHub Actions runs the deploy workflow, `actions/checkout` with `submodules: true` automatically pulls PaperMod from the [adityatelange/hugo-PaperMod](https://github.com/adityatelange/hugo-PaperMod) repo into `themes/PaperMod/` at build time. **Nothing needs to happen locally. The theme is never committed into this repo — it is fetched fresh on every build.**

This is identical to how `fyf-news-site` works.

---

## Deploy Architecture

```
Push to main branch (by AI or by you)
  → GitHub Actions triggers deploy.yml (free — public repo)
    → checkout repo + pull PaperMod submodule automatically
      → Hugo builds public/
        → Cloudflare Pages deploys
          → learnai.fundyourfreedom.in is live (~60 seconds total)
```

---

## One-Time Setup (You Do This — Two Places Only)

### Step 1 — GitHub Secrets

Go to: [fyf-learnai-site → Settings → Secrets → Actions](https://github.com/HABSGconsulting/fyf-learnai-site/settings/secrets/actions)

Add these two secrets:

| Secret Name | Where to Get It |
|---|---|
| `CLOUDFLARE_API_TOKEN` | Cloudflare Dashboard → My Profile → API Tokens → Create Token → use template "Cloudflare Pages: Edit" |
| `CLOUDFLARE_ACCOUNT_ID` | Cloudflare Dashboard → right sidebar (any page) |

### Step 2 — Cloudflare Pages Project

1. Cloudflare Dashboard → **Pages** → **Create a project**
2. Connect to GitHub → select `HABSGconsulting/fyf-learnai-site`
3. Build settings:
   - Framework preset: **Hugo**
   - Build command: `hugo --minify`
   - Build output directory: `public`
4. Click **Save and Deploy**

### Step 3 — DNS

In Cloudflare DNS for `fundyourfreedom.in`:
- Type: **CNAME**
- Name: `learnai`
- Target: your Cloudflare Pages domain (e.g. `fyf-learnai-site.pages.dev`)
- Proxy: **ON** (orange cloud)

---

## Ongoing Workflow

After one-time setup, everything is automatic:
- **Content changes** — I push to `main` via GitHub API
- **Secrets / DNS / Cloudflare config** — you manage in respective dashboards
- **Every push to `main`** — site rebuilds and deploys automatically, no action needed from either of us

---

## Updating the PaperMod Theme

The submodule tracks `branch = master` of PaperMod. To update to the latest PaperMod version, I can update the submodule SHA reference via a commit. Current latest release: **v8.0** (Nov 2024).
