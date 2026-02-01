# MixtapeTools

> Tools for coding, teaching, and presentations with AI assistance.

---

## About This Repo

This is a collection of tools, templates, and philosophies I've developed while using Claude Code for:

- **Coding** (data analysis scripts, replication code, automation)
- **Teaching** (course materials, lecture decks, pedagogical tools)
- **Presentations** (Beamer decks, slides for talks and seminars)

As I develop new approaches, I'll add them here. Anyone is free to use them.

**Take everything with a grain of salt.** These are workflows that work for me. Your mileage may vary.

---

## Who I Am

**Scott Cunningham** — Professor of Economics at Baylor University

- **Website:** [www.scunning.com](https://www.scunning.com)
- **Substack:** [causalinf.substack.com](https://causalinf.substack.com) — I write regularly about causal inference, Claude Code, and random things
- **Free book:** [Causal Inference: The Mixtape](https://mixtape.scunning.com) — available online

---

## What I Recommend

If you're new here, start with:

### 1. Referee 2 (Adversarial Review)

**Location:** `personas/referee2.md`

The single most valuable practice I've developed. After you finish code or analysis with Claude, open a *separate* Claude conversation, paste the referee2 persona, and have it tear your work apart. You cannot grade your own homework.

### 2. The Rhetoric of Decks

**Location:** `presentations/`

My philosophy of slide design, plus a tested prompt for generating Beamer presentations. The key insight: aim for MB/MC equivalence across slides (smoothness), not maximum density.

---

## Repository Structure

```
MixtapeTools/
├── README.md                 # You are here
├── claude/                   # Templates for working with Claude
│   ├── CLAUDE.md            # Project context template (copy to your projects)
│   └── README.md
├── personas/                 # Adversarial reviewers and critics
│   ├── referee2.md          # The adversarial code/analysis reviewer
│   └── README.md
└── presentations/            # Everything about slide decks
    ├── rhetoric_of_decks.md           # Practical principles (condensed)
    ├── rhetoric_of_decks_full_essay.md # Full intellectual framework (600+ lines)
    ├── deck_generation_prompt.md      # The prompt + iterative workflow
    ├── README.md
    └── examples/
        └── gov2001_probability/       # A real lecture deck
```

---

## The Philosophy

### Design Before Results

During estimation and analysis, focus entirely on whether the specification is correct. Results are meaningless until the "experiment" is designed on purpose. Don't get excited or worried about point estimates until the design is intentional.

### Trust But Verify (Heavily on Verify)

AI makes confident mistakes. Cross-software validation (R = Stata = Python) catches bugs that single-language analysis misses. If results aren't identical to 6+ decimal places across implementations, something is wrong.

### Adversarial Review Requires Separation

If you ask the same Claude that wrote code to review it, you're asking a student to grade their own exam. True adversarial review requires a separate conversation with fresh context and no prior commitments.

### Documentation Is First-Class Output

If it's not documented, it didn't happen. Future you (or your collaborators) need to reconstruct what happened. Every significant analysis produces artifacts: summaries, session logs, README files.

---

## Quick Start

### Using Referee 2

1. Complete some code or analysis with Claude
2. Open a **new conversation** (true separation is essential)
3. Paste the contents of `personas/referee2.md` as the opening message
4. Paste your code/analysis and ask for a referee report
5. Take the report back to your original Claude conversation
6. Address each concern or justify not addressing it
7. Iterate until Referee 2 accepts

**Why a new conversation?** Referee 2 in the same conversation is just you grading your own homework. True adversarial review requires separation.

### Using CLAUDE.md

1. Copy `claude/CLAUDE.md` to your project root
2. Fill in your project specifics
3. Claude Code will automatically read it and maintain context
4. Update it when you make important decisions ("we dropped X because Y")

---

## Contributing

Have improvements or additions? PRs welcome. I'm particularly interested in:

- New personas (security reviewer, performance critic, etc.)
- Additional examples showing workflows in practice
- Tools for other aspects of coding and teaching

---

## Acknowledgments

Inspired by [Boris Cherny's ChernyCode](https://github.com/meleantonio/ChernyCode) template for AI coding best practices.

---

## License

Use freely. Attribution appreciated but not required.

---

*Last updated: February 2026*
