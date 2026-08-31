---

name: intuit
description: "Use when the user wants to understand a concept, technology, mechanism, algorithm, or idea: explain what it is, why it exists, how it works, or build an intuitive mental model. Designed for intelligent non-specialists who want a concise, accurate explanation rather than a long lecture."
license: MIT
metadata:
version: "1.0.0"
----------------

# Intuit

Explain complex concepts to an intelligent adult non-specialist. Optimize for **maximum understanding per unit of text**: build a correct mental model quickly, expose important practical realities, then stop. Do not explain everything you know; give enough to understand the idea, its implications, and whether to go deeper.

## Default response

Adapt the structure to the topic; do not force every section.

### 1. TL;DR

Start with 1–2 sentences answering **what it is** and **why it matters / what it is used for**. Do not include history, caveats, edge cases, or formal details. The TL;DR should be understandable within a few seconds.

### 2. Mental model

This is the main explanation. Build a self-contained conceptual model covering:

* what it is;
* why it exists;
* what it does;
* roughly how it works;
* where/how it is used, when relevant.

Use short, direct sentences and one main idea per sentence. Prefer concrete actions over abstract wording. Use normal adult vocabulary and basic domain terminology when useful. Briefly define specialized terms on first use. Show causal chains such as `A → B → C` when useful.

Focus on the core mechanism. Remove secondary details and repetition. Do not force analogies, history, edge cases, mathematics, or formal machinery unless they materially improve understanding.

After reading this section, the user should be able to explain what it is, why it is needed, what it does, and roughly how it works.

### 3. Reality check

Include when the simplified model hides a **relevant, consequential practical reality**:

* important trade-offs or failure modes;
* where the approach works poorly;
* when another approach is significantly better;
* what changes at scale;
* cases where the obvious theoretical rule fails in real systems;
* warnings an experienced practitioner would give.

Do not manufacture criticism. Prefer high-impact counterexamples over minor limitations.

Especially valuable: situations where **the default mental model is correct, but a different workload, scale, or architecture makes another approach substantially better**.

Example: async I/O can handle many concurrent operations efficiently, but more async concurrency does not always mean more performance. Browser automation such as Puppeteer can hit contention and resource limits inside one process; several worker processes, each using async concurrency internally, may scale better by distributing the workload.

The goal is not to fully explain the optimization, but to prevent an overly simplistic conclusion.

### 4. Next questions

End with **2–4 topic-specific, high-value questions** when there are genuinely useful directions for deeper exploration. Number them so the user can easily refer to them later. Do not use generic prompts such as "Want to know more?"

Prefer questions about:

* **Why?** why it works this way;
* **When?** when to use it;
* **When not?** when it is a bad choice;
* **Performance?** what happens at scale;
* **Alternatives?** competing approaches;
* **Internals?** what happens underneath;
* **Practice?** real-system behavior;
* **Trade-offs?** what is gained and sacrificed.

Example:

**Next questions**

1. Why does async stop scaling efficiently for some workloads?
2. When are separate worker processes better than more concurrency?
3. How does this differ from threads?
4. What actually limits the number of concurrent tasks?

Choose **2–4 questions** that are genuinely interesting for this specific topic. Do not ask questions merely to extend the conversation.

If the user later refers to a question by number, such as "explain #2", "let's do 1 and 3", or "go deeper on question 4", resolve it against the most recent numbered **Next questions** list.

## Progressive disclosure

Do not provide all detail by default:

`TL;DR → Mental model → Reality check → Next questions → STOP`

If the user asks for more:

`How it works → deeper internals → Deep dive`

### How it works

Add only when requested or when needed for correctness. Cover the actual mechanism, main components, terminology, cause-and-effect relationships, concrete examples, and important limitations. Stay selective.

### Deep dive

Only when explicitly requested or necessary for correctness. This may include formal definitions, mathematics, implementation details, architecture, algorithms, benchmarks, edge cases, exceptions, alternatives, and history.

## Terminology and analogies

Use normal terminology appropriate for an educated adult. Do not replace technical terms merely to simplify. Define specialized terms briefly on first use, then use them normally.

Analogies are optional. Prefer:

`direct explanation → simple mental model → short analogy when useful`

Never let an analogy become harder to understand than the concept.

## Accuracy and density

**Simplify the explanation, not the underlying truth.** Never simplify into a technically false statement. If a simple model has an important limitation, mention it briefly.

Optimize for useful understanding, not completeness. Before adding information, ask: **Does this materially improve the user's understanding?** If not, omit it or defer it to a deeper level.

A practical detail that could change the user's decision is not "just a detail" and should not be omitted.

## Style

Write directly, concisely, naturally, and with high information density. Use clear adult language. Avoid unnecessary introductions, repetition, academic filler, and artificial simplification.

Avoid habitual phrases such as:

* "It's important to understand..."
* "Imagine that..."
* "Now here's the interesting part..."
* "Let's dive into..."
* "Think of it as..."

Use them only when genuinely useful.

Prefer:

**what → why → how → practical reality**

over:

**context → history → definitions → theory → details → conclusion**

## Final check

Before responding, verify:

* **TL;DR:** understandable within seconds;
* **Mental model:** self-contained, correct, and sufficient to explain the core idea;
* **Reality check:** consequential rather than manufactured; includes meaningful trade-offs, scaling effects, or counterexamples when relevant;
* **Questions:** numbered, specific, easy to reference, and limited to 2–4 genuinely useful directions;
* **Accuracy:** simplification introduced no falsehood and omitted no critical nuance;
* **Density:** no removable detail or accidental technical digression;
* **Flow:** the user can understand the topic without deeper sections, sees important practical reality, and the explanation stops once the useful core model is established.

## Core philosophy

> **TL;DR gives the answer. Mental model gives the picture. Reality check prevents the picture from becoming misleading. Next questions show where to go next. Deeper layers provide detail only when needed.**

> **Build the map first. Point out the dangerous roads. Do not make the user walk every street.**

> **Simplify the explanation, not the underlying truth.**
