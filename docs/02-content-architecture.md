# 02 — Content Architecture

## Overview

This site uses a **two-theme Hugo cascade**:
- `PaperMod` — base theme (public submodule)
- `fyf-hugo-theme` — FYF overrides (private submodule at `HABSGconsulting/fyf-hugo-theme`)

Course layouts, shortcodes, and CSS all live in `fyf-hugo-theme`. This repo contains content only.

---

## Content Hierarchy

```
content/
  courses/
    {course-slug}/
      _index.md                    ← course landing page (intro text only)
      {NN-lesson-slug}/
        index.md                   ← individual lesson
```

`NN` is a zero-padded number (`01`, `02`...). Hugo uses `weight` front matter for ordering.

**`_index.md` contains only the course intro text.** The lesson index is auto-generated
by `fyf-hugo-theme/layouts/courses/list.html` from all child pages. No manual HTML needed.

---

## Lesson Types

Every lesson has `lessonType` in front matter:

| Type | Description | Key Elements |
|---|---|---|
| `explainer` | Concept-first reading | Hook, analogy, callout boxes, no code cells |
| `lab` | Hands-on Python | Short intro, Pyodide cells, reflection prompt |
| `reflection` | Guided reflection | Questions, no code |
| `quiz` | Knowledge check | Multiple choice (future — stub only) |

---

## Front Matter Schema

```yaml
---
title: "Lesson Title"
description: "One-line description for SEO + course index card"
weight: 1                      # controls lesson order within course
date: 2026-07-22
lessonType: explainer          # explainer | lab | reflection | quiz
course: build-your-own-slm     # parent course slug
lessonNumber: 1                # integer shown on lesson card
source: "Google DeepMind — ..."
---
```

---

## Navigation

PaperMod's `ShowPostNavLinks: true` renders "← Previous Lesson | Next Lesson →" automatically at the bottom of every lesson page.

---

## Shortcodes

All shortcodes live in `fyf-hugo-theme`. Available:

| Shortcode | Usage | Purpose |
|---|---|---|
| `{{< pyodide id="x" >}}` | Wrap Python code | Live in-browser Python cell |
| `{{< callout title="..." >}}` | Wrap any text | Amber callout box |
| `{{< quiz >}}` | (future) | Multiple choice quiz |

Pyodide CDN version is controlled by `params.pyodideVersion` in `config.yaml` — not in the shortcode.

---

## Adding a New Course

1. Create `content/courses/{course-slug}/_index.md` with title, description, weight, intro text
2. Add lessons as numbered subdirectories with `index.md`
3. Set `weight`, `lessonNumber`, `lessonType` in each lesson's front matter
4. Push to `main` — deploys automatically, course index renders itself

## Adding a New Lesson to an Existing Course

1. Create `content/courses/{course-slug}/{NN-lesson-slug}/index.md`
2. Set correct `weight` and `lessonNumber` (next in sequence)
3. Write the content
4. Push — course index updates automatically via `list.html`
5. Update `STATUS.md` lesson table
