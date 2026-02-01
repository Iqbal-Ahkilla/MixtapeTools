# Presentation Tools

> **What's in this folder:** Philosophy, principles, and prompts for creating effective slide presentations with AI assistance.

---

## Contents

### `rhetoric_of_decks.md` — Practical Principles (Condensed)

**What it is:** A condensed guide to what makes presentations work. The actionable principles extracted from years of giving and watching academic talks.

**How to use it:**
- **Read it** to internalize the principles
- **Reference it** when designing a new deck
- **Paste it** into Claude when you want it to follow these principles

**Core concepts:**
- **The Three Laws**: Beauty is function, cognitive load is the enemy, slides serve speech
- **Aristotle**: Ethos (credibility), Pathos (emotion), Logos (logic)
- **MB/MC equivalence**: Every slide should have the same marginal benefit to marginal cost ratio
- **Titles are assertions**: "Treatment increased distance by 61 miles" not "Results"
- **Bullets are defeat**: Find the structure hiding in your list

---

### `rhetoric_of_decks_full_essay.md` — The Full Intellectual Framework

**What it is:** A 600+ line essay tracing rhetoric from Aristotle through LLMs. The complete intellectual foundation behind the practical principles.

**Covers:**
- The history of rhetoric (Aristotle, Cicero, Quintilian, Augustine)
- Technology's transformation of persuasion (printing press through PowerPoint)
- The economics of attention (Netflix streaming vs. theater viewing)
- Defamiliarization (Shklovsky's "making the stones feel like stones")
- The academic job market talk as case study
- What LLMs see when trained on presentations
- Tufte's critique and its limits

**When to use it:** When you want to understand *why* the principles work, not just *what* they are.

---

### `deck_generation_prompt.md` — The Prompt

**What it is:** A tested prompt for generating Beamer presentations with Claude Code, including an iterative multi-agent review process.

**How to use it:**
1. Open Claude Code in your project directory
2. Have existing content ready (notes, old slides, paper draft)
3. Customize the bracketed sections in the prompt
4. Paste the prompt
5. Follow the iterative workflow

**The Iterative Workflow:**

```
┌─────────────────────────────────────────┐
│  Step 1: Build deck with MB/MC          │
│          equivalence, compile           │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│  Step 2: Fix ALL compilation warnings   │
│          (no matter how small)          │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│  Step 3: Check silent visual errors     │
│          (Tikz coords, ggplot labels)   │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│  Step 4: Recompile, check flow          │
│          and MB/MC equivalence          │
└──────────────────┬──────────────────────┘
                   │
                   ▼
              ┌────┴────┐
              │ Pass?   │──No──┐
              └────┬────┘      │
                   │           │
                  Yes          │
                   │           │
                   ▼           │
          ┌────────────────┐   │
          │ Human reviews  │   │
          └────────────────┘   │
                               │
               ┌───────────────┘
               │
               ▼
        Back to Step 1
```

**Key insight:** The goal is NOT maximum cognitive density. The goal is **smoothness** — consistent MB/MC ratio across all slides. Exception: deliberate "jump scares" for rhetorical effect.

---

## The Silent Killers

Things that compile fine but look wrong:

**Tikz:**
- Labels not where you think they are
- Coordinate systems misaligned
- Shape constraints forcing misplacement

**ggplot2 / matplotlib:**
- Axis labels cut off
- Legends obscuring data
- Text sizing inconsistent

**How to catch them:** Explicitly verify coordinates. Ask Claude to check label positions against intended positions.

---

## Examples

See `examples/gov2001_probability/` for a complete worked example showing:
- A full probability lecture deck (Harvard Gov 2001)
- Custom Beamer theme (inline in preamble)
- The rhetoric principles in practice
- What the iterative workflow caught
