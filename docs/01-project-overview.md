# 01 — Project Overview

## What Is This

`fyf-learnai-site` powers `learnai.fundyourfreedom.in` — FundYourFreedom's dedicated AI learning platform.

This is a **separate domain** from `learn.fundyourfreedom.in` (which covers personal finance). AI education is a big, long-term domain with its own audience, its own content format, and its own growth trajectory.

## The Problem We're Solving

Google DeepMind and others publish excellent AI/ML learning material. But it's written for people who are already somewhat technical — dense paragraphs, abstract examples, no interactivity.

GenZ learners (and frankly most people) need:
- Short, punchy explanations with real-world analogies
- Immediate hands-on experience — not reading about code, *running* code
- Content that acknowledges what's confusing and pre-answers it
- No install friction — everything in the browser

## What We're Building

GenZ-reframed AI/ML tutorials that:
- Use the same core concepts as Google's curriculum (no dumbing down)
- Deliver them with intuitive analogies (Spotify, autocomplete, Reddit)
- Include live in-browser Python labs (Pyodide — no Colab, no installs)
- Are structured as lovely linked step-by-step tutorials
- Render beautifully on `learnai.fundyourfreedom.in` via Hugo PaperMod

## First Course

**Build Your Own Small Language Model**  
Source: Google DeepMind (https://www.skills.google/course_templates/1341)  
Coverage: Language model fundamentals → probability distributions → building a working SLM

## Audience

- GenZ / young professionals curious about AI
- Non-CS graduates who want to understand AI, not just use it
- FundYourFreedom readers who want to upskill in AI/ML

## Tech Stack

| Layer | Choice |
|---|---|
| Static site generator | Hugo |
| Theme | PaperMod (mirrors fyf-news-site) |
| Interactive Python | Pyodide (in-browser, no backend) |
| Deployment | GitHub Actions → Cloudflare Pages |
| DNS | Cloudflare (subdomain of fundyourfreedom.in) |
