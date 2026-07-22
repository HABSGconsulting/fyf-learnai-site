---
title: "Lab: Build a Probability Distribution"
description: "Stop reading about probability distributions. Build one. Run it here, right now, no install needed."
weight: 2
date: 2026-07-22
lessonType: lab
course: build-your-own-slm
lessonNumber: 2
source: "Google DeepMind — Module 2: Lab: Create Your Own Probability Distribution"
---

<span class="lesson-type-badge badge-lab">⚗️ Lab</span>

## What You're Building

In the last lesson, you learned that a language model assigns probabilities to every possible next word. Now you're going to build the part that *creates* those probabilities — from real text.

This is called a **unigram probability distribution**: count how often each word appears, then divide by total words. Simple. Powerful. The foundation of everything.

## Step 1 — Count the Words

Run this. See what happens. Then edit the `text` variable with your own sentence.

{{< pyodide id="count-words" >}}
from collections import Counter

text = "the cat sat on the mat the cat sat"
words = text.split()
counts = Counter(words)

print("Word counts:")
for word, count in counts.most_common():
    print(f"  {word}: {count}")
{{< /pyodide >}}

## Step 2 — Turn Counts Into Probabilities

A count is just a count. A probability is a count divided by the total. Run this:

{{< pyodide id="make-probs" >}}
from collections import Counter

text = "the cat sat on the mat the cat sat"
words = text.split()
total = len(words)
counts = Counter(words)

print("Probability distribution:")
for word, count in counts.most_common():
    prob = count / total
    print(f"  {word}: {prob:.3f}")

# Sanity check: probabilities must sum to 1.0
print(f"\nSum of all probabilities: {sum(c/total for c in counts.values()):.3f}")
{{< /pyodide >}}

{{< callout title="💭 Why does the sum equal 1?" >}}
A probability distribution must always sum to 1.0 — because *something* has to come next, and all possibilities together account for 100% of outcomes. If your sum isn't 1.0, your distribution is broken.
{{< /callout >}}

## Step 3 — Sample From Your Distribution

This is the fun part. A real language model doesn't always pick the most probable word — it *samples* from the distribution. Run this a few times and watch the randomness:

{{< pyodide id="sample-dist" >}}
import random
from collections import Counter

text = "the cat sat on the mat the cat sat"
words = text.split()
total = len(words)
counts = Counter(words)

vocab = list(counts.keys())
probs = [counts[w] / total for w in vocab]

def sample_word():
    r = random.random()
    cumulative = 0
    for word, prob in zip(vocab, probs):
        cumulative += prob
        if r < cumulative:
            return word
    return vocab[-1]

print("10 sampled words:")
print([sample_word() for _ in range(10)])
{{< /pyodide >}}

## What You Just Built

You built the core of a language model:
1. **Corpus** — your input text
2. **Count** — how often each word appears
3. **Probability distribution** — counts normalised to sum to 1.0
4. **Sampler** — picks the next word probabilistically, not deterministically

Real language models do this at a *massively* larger scale — billions of words, not nine. But the principle is identical.

---
*Source: Google DeepMind — Build Your Own Small Language Model, Module 2*
