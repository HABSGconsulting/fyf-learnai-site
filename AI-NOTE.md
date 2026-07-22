# AI-NOTE.md — fyf-learnai-site

Context primer for AI assistants working on this repo.  
**Read this first. Then read STATUS.md and DECISIONS.md.**

---

## What This Repo Is

`fyf-learnai-site` is a Hugo-based course platform.  
Live URL: **https://aicourses.fundyourfreedom.in**  
Repo: `HABSGconsulting/fyf-learnai-site` (public)

It hosts structured AI courses — each with explainer lessons, Python labs (Pyodide), and reflection prompts.
This is a long-lived, growing platform. It will have many courses over time.

---

## Architecture

### Two-Theme Cascade

```
themes/
  PaperMod/            ← base theme (public submodule)
  fyf-hugo-theme/      ← FYF overrides (PRIVATE submodule — HABSGconsulting/fyf-hugo-theme)
```

Hugo loads themes left-to-right. `fyf-hugo-theme` is loaded second and wins on any conflict.
Do NOT put layouts or shortcodes directly in this repo — they belong in `fyf-hugo-theme`.

### What Lives Where

| Location | Contains |
|---|---|
| `content/courses/` | All course and lesson Markdown files |
| `config.yaml` | Site config, pyodideVersion param, baseURL |
| `assets/css/custom.css` | Site-specific CSS overrides (keep minimal) |
| `themes/fyf-hugo-theme/` | Course layouts, shortcodes, brand CSS (edit in fyf-hugo-theme repo) |
| `themes/PaperMod/` | Base theme (never edit directly) |

### Content Hierarchy

```
content/
  courses/
    build-your-own-slm/
      _index.md            ← course landing (title, description, intro text ONLY — no manual lesson list)
      01-what-is-a-language-model/
        index.md           ← lesson
      02-lab-probability-distribution/
        index.md
    using-ai-with-python/
      _index.md
      01-what-is-ai-and-python/
        index.md
```

**IMPORTANT:** `_index.md` files must NOT contain a manual lesson list.
The `fyf-hugo-theme` `list.html` template auto-generates the lesson index from child pages.
Just write the course intro in `_index.md` — the lesson cards appear automatically.

---

## Front Matter Schema

### Course landing (`_index.md`)
```yaml
---
title: "Course Title"
description: "One-line description"
weight: 1        # controls order on the /courses/ index
date: 2026-07-22
source: "Attribution string"
---
```

### Lesson (`index.md`)
```yaml
---
title: "Lesson Title"
description: "One-line description for SEO + course index card"
weight: 1                      # controls lesson order within course
date: 2026-07-22
lessonType: explainer          # explainer | lab | reflection | quiz
course: course-slug            # parent course slug
lessonNumber: 1                # integer, shown on card
source: "Attribution string"
---
```

---

## Shortcodes Available

All shortcodes live in `themes/fyf-hugo-theme/layouts/shortcodes/`.

| Shortcode | Usage |
|---|---|
| `{{< pyodide id="x" >}}...{{< /pyodide >}}` | In-browser Python cell |
| `{{< callout title="..." >}}...{{< /callout >}}` | Amber callout/annotation box |
| `{{< quiz >}}` | Multiple choice quiz (stub — future) |

Pyodide version is set in `config.yaml` → `params.pyodideVersion`. To upgrade: change that one value.

---

## CI / Deployment

- GitHub Actions: `.github/workflows/deploy.yml`
- Requires secrets: `CLOUDFLARE_API_TOKEN`, `CLOUDFLARE_ACCOUNT_ID`, `GH_PAT`
- `GH_PAT` is needed to fetch the private `fyf-hugo-theme` submodule during CI
- Deploys to Cloudflare Pages on every push to `main`
- Live at: https://aicourses.fundyourfreedom.in

---

## Rules for AI Working on This Repo

1. **Never put layouts or shortcodes here** — they go in `fyf-hugo-theme`
2. **Never add manual lesson HTML to `_index.md`** — the template does it automatically
3. **Always set `lessonNumber` and `weight`** in lesson front matter
4. **Always set `lessonType`** — explainer | lab | reflection | quiz
5. **Keep `custom.css` minimal** — brand styles are in the theme
6. **Update `STATUS.md`** after adding any new lesson or course
