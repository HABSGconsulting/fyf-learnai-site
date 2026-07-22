# 04 — Lesson Authoring Guide

## The GenZ Delivery Principles

| Element | Do This | Not This |
|---|---|---|
| Opener | 1-2 line hot take or relatable scenario | "In this lesson we will cover..." |
| Analogies | Spotify, autocomplete, Reddit, texting | "Consider a corpus of documents" |
| Math | Intuition first, notation second | Notation first |
| Tone | Curious, direct, honest about what's hard | Authoritative, textbook |
| Length | Short bursts, bold callouts | Walls of text |
| Code | Central, runnable, editable | Optional appendix |

## Writing an Explainer Lesson

### Structure
```
1. Badge: <span class="lesson-type-badge badge-explainer">📖 Explainer</span>
2. ## The Hot Take  (1-2 bold sentences)
3. ## [Core concept section]
   - Use {{< callout >}} to pre-answer confusion
   - Short paragraphs, max 3 sentences each
   - One real-world analogy per major concept
4. ## The Key Insight  (what to remember)
5. ## What's Next  (1 sentence bridge to next lesson)
```

## Writing a Lab Lesson

### Structure
```
1. Badge: <span class="lesson-type-badge badge-lab">⚗️ Lab</span>
2. ## What You're Building  (1 paragraph — set expectations)
3. ## Step 1 — [task name]
   - 1-2 sentence intro
   - {{< pyodide id="step1" >}} cell with starter code
4. ## Step 2 — [next task]
   - Use {{< callout >}} after cells to explain surprising output
5. ## What You Just Built  (bullet list recap)
```

### Pyodide Cell Best Practices
- Starter code must **produce visible output immediately** — student runs it and sees something
- Keep starter code under 15 lines
- Each cell must be independently runnable (don't require running cell 1 before cell 2)
- Add a comment like `# Try changing this:` to invite experimentation

## Callout Box Usage

```
{{< callout title="💭 Wait, but why?" >}}
Your explanation here.
{{< /callout >}}

{{< callout title="🎵 Think of it like Spotify" >}}
Analogy here.
{{< /callout >}}

{{< callout title="⚠️ Common mistake" >}}
Warning here.
{{< /callout >}}
```

## Lesson Naming Convention

```
content/courses/{course-slug}/{NN-kebab-case-title}/index.md
```

Examples:
- `01-what-is-a-language-model/`
- `02-probability-lab/`
- `03-bigrams-and-context/`
