# 02 — Content Architecture

## Hierarchy

```
content/
  courses/
    {course-slug}/
      _index.md                    ← course landing page
      {NN-lesson-slug}/
        index.md                   ← individual lesson
```

`NN` is a zero-padded number (`01`, `02`...) — Hugo uses this + `weight` for ordering.

## Lesson Types

Every lesson has `lessonType` set in front matter:

| Type | Description | Key Elements |
|---|---|---|
| `explainer` | Concept-first reading | Hook, analogy, callout boxes, no code cells |
| `lab` | Hands-on Python | Short intro, Pyodide cells, reflection prompt |

## Front Matter Schema

```yaml
---
title: "Lesson Title"
description: "One-line description for SEO + course index"
weight: 1                      # controls lesson order
date: 2026-07-22
lessonType: explainer          # or: lab
course: build-your-own-slm     # parent course slug
lessonNumber: 1                # integer
source: "Google DeepMind — ..."
---
```

## Navigation

PaperMod's `ShowPostNavLinks: true` automatically renders "← Previous Lesson | Next Lesson →" at the bottom of every page. This creates the "lovely linked step-by-step" flow with zero extra configuration.

## Shortcodes Available

| Shortcode | Usage | Purpose |
|---|---|---|
| `{{< pyodide id="x" >}}` | Wrap Python code | Live in-browser Python cell |
| `{{< callout title="..." >}}` | Wrap any text | Amber callout box |

## Adding a New Course

1. Create `content/courses/{course-slug}/_index.md`
2. Add lessons as numbered subdirectories
3. Set `weight` in each lesson's front matter for ordering
4. Push to `main` — deploys automatically
