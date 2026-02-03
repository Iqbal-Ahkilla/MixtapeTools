# `/split-pdf` — Download, Split, and Deep-Read Academic Papers

**Skill location:** [`.claude/skills/split-pdf/SKILL.md`](../../.claude/skills/split-pdf/SKILL.md)

---

## The Problem

Claude Code can read PDFs, but long academic papers cause two failures:

1. **Session crash.** PDFs are token-expensive (fonts, vector graphics, tables, math notation). A 40-page paper can exceed the context window, producing an unrecoverable "prompt too long" error that destroys the entire session and all context.

2. **Shallow reading.** Even when the PDF fits, Claude's attention degrades over long documents — it reads the abstract carefully, skims the methodology, and often hallucinates details from the results. You get a confident summary that's subtly wrong.

These are related but distinct problems. The first kills the session. The second produces unreliable output while the session continues normally. Splitting addresses both.

---

## The Solution

Split the PDF into 4-page chunks, read 3 chunks at a time (~12 pages), and write structured notes incrementally.

### How It Works

| Step | Action |
|------|--------|
| **Acquire** | Download the PDF (via web search) or use a local file |
| **Split** | PyPDF2 splits into 4-page chunks in `articles/split_<name>/` |
| **Read** | Read 3 splits at a time, pause after each batch |
| **Extract** | Update running `notes.md` with structured information |
| **Confirm** | Wait for user approval before continuing to next batch |

### Usage

```
/split-pdf path/to/paper.pdf
/split-pdf "Gruber 1994 health insurance"
```

**You must tell Claude what paper to read.** Claude cannot webcrawl for a paper it doesn't know exists. Provide either a local file path or a search query specific enough to find the paper — an author name, title, keywords, year, or some combination. If you just type `/split-pdf` with nothing else, Claude will ask you what you're looking for.

### What Gets Extracted (8 Dimensions)

The skill doesn't produce a summary. It produces a **structured extraction** — the information a researcher needs to build on or replicate the work:

1. **Research question** — What is the paper asking and why does it matter?
2. **Audience** — Which sub-community of researchers cares about this?
3. **Method** — How do they answer the question? What is the identification strategy?
4. **Data** — What data do they use? Where did they find it? Unit of observation? Sample size? Time period?
5. **Statistical methods** — What econometric or statistical techniques? Key specifications?
6. **Findings** — Main results? Key coefficient estimates and standard errors?
7. **Contributions** — What is learned that we didn't know before?
8. **Replication feasibility** — Public data? Replication archive? Data appendix? URLs?

---

## Why This Design

**Why 4-page chunks?** Small enough for careful attention, large enough to keep logical sections (a methodology subsection, a results table with discussion) together. A 40-page paper becomes 10 chunks read in 4 rounds.

**Why 3 chunks per batch (~12 pages)?** Balances throughput against attention quality. Twelve pages is enough to make progress but not so much that comprehension degrades.

**Why pause between batches?** So you can:
- Review intermediate output and catch errors before they compound
- Redirect the reading or ask follow-up questions
- Skip sections that aren't relevant
- Control pacing for sections that need more care

**Why incremental notes instead of a final summary?** When Claude reads a full paper at once, it produces a summary — lossy compression. When it reads in batches and updates running notes, it accumulates detail. The final notes are richer than any one-shot summary.

For the full methodology, see [`.claude/skills/split-pdf/methodology.md`](../../.claude/skills/split-pdf/methodology.md).

---

## Directory Structure After Running

```
articles/
├── smith_2024.pdf                    # original PDF — ALWAYS preserved, never deleted
└── split_smith_2024/                 # split subdirectory
    ├── smith_2024_pp1-4.pdf          # 4-page chunks
    ├── smith_2024_pp5-8.pdf
    ├── smith_2024_pp9-12.pdf
    ├── ...
    └── notes.md                      # structured reading notes
```

**The original PDF is never deleted.** Whether Claude downloaded it via web search or you pointed it to a local file, the original always stays in `articles/`. The split files are derivatives. If anything goes wrong — a corrupted split, a re-read with different parameters — you can always re-split from the original.

---

## Examples

This directory may contain example outputs from running the skill — split PDFs and the notes they produce. These show what the skill's output looks like in practice.

---

## Limitations

- **It is slow.** A 37-page paper requires ~4 rounds of reading with user confirmation between each. This is a deliberate trade-off: careful reading over fast reading.
- **Notes can become repetitive** if the paper revisits themes. Some manual editing of the final notes may be useful.
- **Not for triage.** If you just need to decide whether a paper is relevant, read only the first split (pages 1-4, which usually contains the abstract and introduction). You don't need the full protocol.
- **Papers under ~15 pages** can be read directly without splitting.
