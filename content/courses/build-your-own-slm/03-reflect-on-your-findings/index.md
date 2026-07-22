---
title: "Reflect on Your Findings"
description: "You've built a probability distribution. Now the harder question: what does it actually tell you about how language models think?"
weight: 3
date: 2026-07-22
lessonType: reflection
course: build-your-own-slm
lessonNumber: 3
readingTime: 5
source: "Google DeepMind — Module 3: Reflect on your findings"
---

<span class="lesson-type-badge badge-explainer">🧠 Reflect</span>

## Pause Before Moving On

You just built a working probability distribution from scratch. Before writing more code, take 5 minutes to actually think about what you built — because the insights here will make every future lesson click faster.

These aren't quiz questions. There are no right answers. Write your thoughts in [NotebookLM](https://notebooklm.google/) or any notes app — you'll want them later.

---

## Prompt 1 — Context Changes Everything

> *What did manually assigning probabilities tell you about how sensitive language models are to context?*

Think about two prompts:
- *"Jide is hungry, so he..."*
- *"Jide is thirsty, so he..."*

The next word distribution shifts completely between these two — even though only one word changed. A model trained on real text would assign high probability to `eat` / `food` / `ordered` in the first case, and `drink` / `reached` / `grabbed` in the second.

{{< callout title="💭 The implication" >}}
Language models are not just predicting words — they're encoding *relationships between concepts*. "Hungry" activates a whole cluster of related words. "Thirsty" activates a different cluster. This is why context window size matters so much in real models.
{{< /callout >}}

**Write:** Where else in daily life does a single word completely change what comes next? Think about customer service, search engines, medical records.

---

## Prompt 2 — Single Words vs. Longer Text

> *How do differences in probability distributions affect predictions of longer texts, not just single words?*

In the lab you predicted one word at a time. But real language generation is this process repeated hundreds of times — each predicted word becomes part of the context for the next prediction.

This means small probability differences **compound**. A slightly wrong prediction early in a sentence nudges the next word, which nudges the next, which nudges the next. By sentence 3 you might be far from where you started.

{{< callout title="⚠️ This is called hallucination" >}}
When a language model confidently generates text that's factually wrong, this compounding effect is often why. It made a plausible-but-wrong early choice, then stayed internally consistent with that wrong choice all the way down.
{{< /callout >}}

**Write:** Think about an application — a legal document assistant, a medical chatbot, a news summariser — where compounding errors would be genuinely dangerous. What safeguards would you want?

---

## Prompt 3 — Bias Lives in the Data

> *How could stereotypes or biases in the input data affect predictions, and what could be done about it?*

Your model learned from whatever text you gave it. If that text had patterns — like always associating certain names with certain jobs, or certain groups with certain behaviours — your model learned those patterns too. It doesn't know they're biased. It just knows they're statistically common in the training data.

This is not a hypothetical problem. Early language models famously:
- Associated "doctor" predominantly with male pronouns
- Associated certain names with negative sentiment
- Generated different quality responses for different demographic groups

{{< callout title="💭 It's a data problem, not a model problem" >}}
The model is doing its job perfectly — it's accurately reflecting patterns in the data. The problem is the data reflects a biased world. You can't fix this by tweaking the model architecture alone.
{{< /callout >}}

**Write:** What are three concrete steps that could reduce bias in a language model's outputs? Think about: what goes into training data, how outputs are evaluated, and who is in the room making decisions.

---

## The Research Skill: Reflection

Reflection isn't soft filler between the "real" technical content. It's how you convert information into understanding.

The researchers who build the best AI systems are the ones who stop and ask *"wait, why does this work? And what could go wrong?"* before rushing to the next thing. That habit starts here.

---

## Before You Continue

Done reflecting? Good. In the next lesson you'll go beyond single-word prediction and give your model **memory** — by introducing bigrams, where the model looks at the previous word before predicting the next one.

---
*Source: Google DeepMind — Build Your Own Small Language Model, Module 3*
