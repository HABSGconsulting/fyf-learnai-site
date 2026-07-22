# 01 — Project Overview

## What Is This

`fyf-learnai-site` powers **https://aicourses.fundyourfreedom.in** — FundYourFreedom's AI course platform.

This is a **separate domain** from `learn.fundyourfreedom.in` (personal finance) and `news.fundyourfreedom.in` (AI news). AI courses are a distinct, long-term product with their own audience, content format, and growth trajectory.

---

## The Problem We're Solving

Google DeepMind and others publish excellent AI/ML learning material. But it's written for people who are already somewhat technical — dense paragraphs, abstract examples, no interactivity.

FYF learners need:
- Short, punchy explanations with real-world analogies
- Immediate hands-on experience — not reading about code, *running* code
- Content that acknowledges what's confusing and pre-answers it
- No install friction — everything in the browser

---

## What We're Building

A growing catalog of AI courses that:
- Use the same core concepts as Google's curriculum (no dumbing down)
- Deliver them with intuitive analogies (Spotify, autocomplete, Reddit)
- Include live in-browser Python labs (Pyodide — no Colab, no installs)
- Are structured as step-by-step linked lessons with prev/next navigation
- Render beautifully at `aicourses.fundyourfreedom.in` via Hugo

---

## Courses

| # | Course | Status |
|---|---|---|
| 1 | Build Your Own Small Language Model | In progress |
| 2 | Using AI with Python | Stub — being written |

---

## Audience

- GenZ / young professionals curious about AI
- Non-CS graduates who want to understand AI, not just use it
- FundYourFreedom readers who want to upskill in AI/ML

---

## Tech Stack

| Layer | Choice | Notes |
|---|---|---|
| Static site generator | Hugo (extended, latest) | Fast builds, no Node |
| Base theme | PaperMod (public submodule) | Navigation, pagination, search |
| FYF theme | `fyf-hugo-theme` (private submodule) | Course layouts, shortcodes, brand CSS |
| Interactive Python | Pyodide (in-browser, no backend) | Version set in `config.yaml` |
| CI/CD | GitHub Actions | Free — public repo |
| Hosting | Cloudflare Pages | Global CDN, zero cost |
| DNS | Cloudflare | `aicourses.fundyourfreedom.in` |

---

## Repository Structure

```
fyf-learnai-site/
  config.yaml                     ← site config + pyodideVersion param
  assets/css/custom.css           ← site-specific overrides only
  content/courses/                ← ALL course and lesson content
  themes/
    PaperMod/                     ← base theme (public submodule)
    fyf-hugo-theme/               ← FYF overrides (private submodule)
  .github/workflows/deploy.yml    ← CI/CD pipeline
  docs/                           ← this documentation
  AI-NOTE.md                      ← AI assistant primer (read first)
  STATUS.md                       ← current build state
  DECISIONS.md                    ← architecture decision records
```
