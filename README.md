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

### 1. Referee 2 (Systematic Audit & Replication Protocol)

**Location:** `personas/referee2.md`

The single most valuable practice I've developed. Referee 2 is a **health inspector for empirical research** — not a vague "be critical" persona, but a systematic audit and replication protocol with five specific audits, formal referee reports, and a revise & resubmit process.

**The Five Audits:**

| Audit | What It Does |
|-------|--------------|
| **Code Audit** | Scrutinizes for coding errors, missing value handling, merge diagnostics, variable construction |
| **Cross-Language Replication** | Creates replication scripts in 2 other languages (R/Stata/Python), compares results to 6 decimal places |
| **Directory Audit** | Checks folder structure, relative paths, naming conventions — is this replication-package ready? |
| **Output Automation Audit** | Are tables and figures programmatically generated or manually created? |
| **Econometrics Audit** | Are specifications coherent? Standard errors correct? Identification plausible? |

**Why Cross-Language Replication?**

Hallucination errors are likely **orthogonal** across languages. If Claude writes R code with a subtle bug, the Stata version will likely have a *different* bug. When results match to 6+ decimal places across R, Stata, and Python, you have high confidence the code is correct. When they don't match, you've caught a bug that single-language review would miss.

**Critical Rule: Referee 2 NEVER modifies author code.** Referee 2 only creates its own replication scripts in `code/replication/`. The author is the only one who modifies the author's code. This separation is essential — the audit must be independent.

**The Revise & Resubmit Workflow:**

1. Complete analysis in your main Claude session (the "author")
2. Open a **new terminal** (fresh context is essential)
3. Paste `referee2.md` and point Claude at your project
4. Referee 2 performs 5 audits, creates replication scripts at `code/replication/`, files a formal **referee report** at `correspondence/referee2/`
5. Close that terminal
6. Read the referee report, write a **response** addressing each concern (fix or justify)
7. File your response, open **another new terminal**, and **resubmit** for Round 2
8. Iterate until verdict is Accept

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
├── personas/                 # Systematic audit & replication protocols
│   ├── referee2.md          # The 5-audit protocol for empirical research
│   └── README.md
└── presentations/            # Everything about slide decks
    ├── rhetoric_of_decks.md           # Practical principles (condensed)
    ├── rhetoric_of_decks_full_essay.md # Full intellectual framework (600+ lines)
    ├── deck_generation_prompt.md      # The prompt + iterative workflow
    ├── README.md
    └── examples/
        ├── rhetoric_of_decks/         # The philosophy deck (45 slides)
        └── gov2001_probability/       # A lecture deck
```

---

## The Philosophy

### Design Before Results

During estimation and analysis, focus entirely on whether the specification is correct. Results are meaningless until the "experiment" is designed on purpose. Don't get excited or worried about point estimates until the design is intentional.

### Trust But Verify (Heavily on Verify)

AI makes confident mistakes. Cross-software replication (R = Stata = Python) catches bugs that single-language analysis misses. If results aren't identical to 6+ decimal places across implementations, something is wrong.

### Adversarial Review Requires Separation

If you ask the same Claude that wrote code to review it, you're asking a student to grade their own exam. True adversarial review requires a **new terminal** with fresh context and no prior commitments.

### Referee 2 Never Modifies Author Code

The audit must be independent. Referee 2 creates its own replication scripts but **never touches the author's code**. Only the author modifies the author's code. This separation ensures the audit is truly external.

### Formal Process > Informal Vibes

Checklists beat intuition. The Referee 2 protocol works because it specifies exactly what to check, requires concrete deliverables (replication scripts, comparison tables, referee reports), and creates a paper trail.

### Documentation Is First-Class Output

If it's not documented, it didn't happen. Every audit produces a dated referee report filed in `correspondence/`. Every response is documented. Replication scripts are permanent artifacts. Future you (or your collaborators) can reconstruct exactly what happened.

---

## Quick Start

### Using Referee 2

**Round 1 (Initial Submission):**

1. Complete your analysis in your main Claude session
2. Open a **new terminal** (true separation is essential)
3. Paste the contents of `personas/referee2.md` as the opening message
4. Say: "Please audit and replicate the project at [path]. Primary language is [R/Stata/Python]."
5. Referee 2 performs 5 audits, creates replication scripts at `code/replication/`, and files:
   - Referee report (markdown) at `correspondence/referee2/YYYY-MM-DD_round1_report.md`
   - Referee report deck (PDF) at `correspondence/referee2/YYYY-MM-DD_round1_deck.pdf` — beautiful tables and figures showing cross-language comparisons, following rhetoric of decks principles
6. Close that terminal

**Author Response:**

7. Read the referee report carefully
8. For each Major Concern: fix your code OR write a justification for not fixing
9. For each Minor Concern: fix your code OR acknowledge and deprioritize
10. Answer all Questions for Authors
11. File your response at `correspondence/referee2/YYYY-MM-DD_round1_response.md`

**Round 2+ (Revision Review):**

12. Open **another new terminal**
13. Paste `referee2.md`
14. Say: "This is Round 2 of the revise & resubmit. Read the original referee report, my response, and the revised code."
15. Referee 2 re-runs audits, assesses your responses, files Round 2 referee report
16. Repeat until verdict is Accept

### Using CLAUDE.md

1. Copy `claude/CLAUDE.md` to your project root
2. Fill in your project specifics
3. Claude Code will automatically read it and maintain context
4. Update it when you make important decisions ("we dropped X because Y")

**Note:** Referee reports do NOT go into `CLAUDE.md`. They go in `correspondence/referee2/`. The CLAUDE.md file is for project context, not audit trails.

---

## Project Directory Structure

For the Referee 2 workflow to function properly, your research projects should include:

```
your_project/
├── CLAUDE.md                 # Project context for Claude
├── correspondence/
│   └── referee2/
│       ├── 2026-02-01_round1_report.md      # Detailed written report
│       ├── 2026-02-01_round1_deck.pdf       # Visual presentation of findings
│       ├── 2026-02-02_round1_response.md    # Author response
│       ├── 2026-02-05_round2_report.md      # Round 2 referee report
│       ├── 2026-02-05_round2_deck.pdf
│       └── ...
├── code/
│   ├── R/                    # Author's code (ONLY author modifies)
│   ├── stata/
│   ├── python/
│   └── replication/          # Referee 2's replication scripts
│       ├── referee2_replicate_main_results.do
│       ├── referee2_replicate_main_results.R
│       ├── referee2_replicate_main_results.py
│       └── ...
├── data/
│   ├── raw/
│   └── clean/
└── output/
    ├── tables/
    └── figures/
```

**Note:** Referee 2 ONLY writes to `code/replication/` and `correspondence/referee2/`. It NEVER modifies author code in `code/R/`, `code/stata/`, or `code/python/`.

---

## Contributing

Have improvements or additions? PRs welcome. I'm particularly interested in:

- Additional audit protocols (security reviewer, pedagogy reviewer, etc.)
- Examples showing the Referee 2 workflow catching real bugs
- Tools for other aspects of coding and teaching

---

## Acknowledgments

Inspired by [Boris Cherny's ChernyCode](https://github.com/meleantonio/ChernyCode) template for AI coding best practices.

---

## License

Use freely. Attribution appreciated but not required.

---

*Last updated: February 2026*
