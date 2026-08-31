# intuit

> Build the map first. Point out the dangerous roads. Don't make the user walk every street.

**intuit** is an AI skill for explaining complex concepts to intelligent non-specialists.

It focuses on building a **correct mental model quickly** instead of dumping information. The explanation starts with the core idea, exposes important practical realities, and reveals deeper implementation details only when they're useful.

## Why intuit?

Most technical explanations fail in one of two ways:

* **Too shallow:** simple enough to understand, but technically misleading.
* **Too deep:** technically complete, but the reader loses the core idea somewhere between definitions, history, and implementation details.

`intuit` aims for the middle:

```text
What is it?
     ↓
Why does it exist?
     ↓
How does it work?
     ↓
Where does the simple model break?
     ↓
What should I explore next?
```

The goal is not maximum completeness.

> **Maximum understanding per unit of text.**

## How it explains

A typical explanation follows four stages:

### 1. TL;DR

A one- or two-sentence answer to:

* What is it?
* Why does it matter?

### 2. Mental model

The core conceptual explanation:

* what it is;
* why it exists;
* what it does;
* roughly how it works;
* where it is used.

Technical terminology is kept when useful, but specialized terms are briefly explained on first use.

### 3. Reality check

The simplified mental model is challenged when real-world behavior differs from the obvious theory.

This can include:

* scaling limitations;
* performance trade-offs;
* failure modes;
* architectural constraints;
* cases where another approach works substantially better.

This is an important part of `intuit`: a simple explanation should not leave the user with a **wrong rule of thumb**.

For example, explaining async concurrency shouldn't stop at "async lets you handle many tasks at once." For some workloads, increasing concurrency eventually creates contention and resource pressure, and distributing work across separate processes can perform substantially better.

### 4. Next questions

The explanation ends with **2–4 numbered questions** that naturally follow from the topic.

For example:

```text
Next questions

1. Why does async stop scaling efficiently for some workloads?
2. When are separate worker processes better than more concurrency?
3. How does this differ from threads?
4. What actually limits the number of concurrent tasks?
```

Numbering makes follow-up conversations easy:

> "Explain #2."

> "Let's do 1 and 3."

## Progressive disclosure

`intuit` does not automatically dump every available detail.

```text
TL;DR
  ↓
Mental model
  ↓
Reality check
  ↓
Next questions
  ↓
STOP

User asks for more
  ↓
How it works
  ↓
Deep dive
```

The initial response should be enough to understand the concept. Deeper implementation details, mathematics, architecture, algorithms, benchmarks, and edge cases appear only when requested or necessary for correctness.

## Design principles

### Simplify the explanation, not the truth

A mental model can be simple without being false.

When an important limitation changes how the user should think about or use something, `intuit` surfaces it instead of hiding it as "advanced detail."

### Direct explanation over forced analogies

Analogies are useful tools, not a requirement.

The preferred order is:

```text
Direct explanation
      ↓
Simple mental model
      ↓
Short analogy, when useful
```

### Practical reality matters

A theoretically correct explanation can still produce bad engineering decisions.

`intuit` deliberately looks for situations where:

> **The default mental model is correct, but a different workload, scale, or architecture changes the best approach.**

### Stop when the useful model is established

The goal isn't to demonstrate everything the model knows.

It's to give the reader a map.

> **Build the map first. Point out the dangerous roads. Do not make the user walk every street.**

## Installation

Install with the [`skills` CLI](https://skills.sh/):

```bash
npx skills add <owner>/intuit
```

Install globally:

```bash
npx skills add <owner>/intuit -g
```

List installed skills:

```bash
npx skills list
```

## Repository structure

```text
intuit/
├── intuit/
│   └── SKILL.md
├── README.md
├── LICENSE
└── .gitignore
```

`SKILL.md` contains the actual instructions used by the AI agent. This README documents the project for humans.

## License

MIT
