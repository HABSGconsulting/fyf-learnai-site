---
title: "What Is a Language Model?"
description: "Your autocomplete is making predictions 24/7. Here's the math behind it — and why it's simpler than you think."
weight: 1
date: 2026-07-22
lessonType: explainer
course: build-your-own-slm
lessonNumber: 1
source: "Google DeepMind — Module 1: Introduction to the language modeling problem"
---

<span class="lesson-type-badge badge-explainer">📖 Explainer</span>

## The Hot Take

A language model is not magic. It's a very well-trained guesser.

Every time your phone suggests the next word, it's running a probability calculation: *"given these words, what word comes next most often?"* That's it. That's the whole idea.

## What a Language Model Actually Does

{{< callout title="💭 Wait — isn't it more complicated than that?" >}}
For massive models like GPT-4, yes — there are billions of parameters and complex neural architectures. But the *core idea* is the same: predict the next token using probability. We start here. Complexity comes later.
{{< /callout >}}

A language model answers one question: **"What comes next?"**

Given the sentence: *"The cat sat on the..."*

A language model assigns probabilities to every word in its vocabulary:
- `mat` → 0.31
- `floor` → 0.22
- `couch` → 0.18
- `roof` → 0.04
- `quantum` → 0.000001

The model picks (or samples) from this distribution. Higher probability = more likely to be chosen.

## The Key Insight

The model learned these probabilities from reading enormous amounts of human text. It didn't learn grammar rules. It learned *patterns* — "after this sequence of words, humans usually write this".

{{< callout title="🎵 Think of it like Spotify" >}}
Spotify doesn't know what song you *should* like next. It knows what songs people with similar listening history tend to play next. Language models work the same way — pattern matching at massive scale.
{{< /callout >}}

## Why Probabilities?

Language is not deterministic. After "The weather today is..." you could say "beautiful", "terrible", "unpredictable", or a hundred other things. All are valid.

A probability distribution captures this: it doesn't force one answer. It gives every possible next word a score, and the model samples from that distribution.

This is why language models can be *creative* — they're not always picking the top choice. Sometimes they sample a lower-probability word, and that's what gives text variety.

## What's Next

In the next lesson, you'll **build a probability distribution from scratch** — in Python, running right in your browser. No install. No setup. Just run it.

---
*Source: Google DeepMind — Build Your Own Small Language Model, Module 1*
