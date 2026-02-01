# Deck Generation Prompt

A prompt for generating academic slide decks with Claude Code. This prompt encodes best practices for Beamer presentations with embedded code, figures, and multi-agent review.

## Prerequisites

- Claude Code opened in a local directory containing your course materials
- Existing slides, notes, or content to restructure (optional but recommended)
- R installed (or let Claude install it)
- LaTeX/Beamer installed (or let Claude install it)

## The Prompt

Customize the bracketed sections for your context, then paste into Claude Code:

---

```
I want you to design for me an original Beamer style design — something truly original, aesthetically pleasing, but professional for [AUDIENCE: e.g., "an undergraduate course on data science" / "a PhD seminar in applied microeconomics" / "a conference presentation on causal inference"].

I then want you to take [THE CONTENT: e.g., "the first deck" / "my lecture notes on regression discontinuity" / "this paper draft"] and restructure it.

I want you to emphasize a new rhetoric of the same subject matter and key learning points but maintaining my pedagogy as you detect it.

I want [CODE LANGUAGE: R/Python/Stata] scripts embedded in the decks, and also new [CODE LANGUAGE] scripts accompanying it so that I can do walk-throughs and provide those scripts to students.

Remember: to me a deck must be beautiful, it must have a consistent narrative flow that nonetheless maintains technical rigor, it must have beautiful slides with optimal cognitive density across all slides — a smooth delivery, not overloaded at the slide level, but distributed and balanced well so that slides do not become too dense — and I want beautiful figures and beautiful tables as I care about the visualization of data.

And then compile it.

Once you compile, then check and eliminate ALL overfull, underfull, vbox and hbox errors. No matter how small. Recompile.

Then have a second agent evaluate the deck for whether these instructions were met and make adjustments based on that recommendation and criticism.

I want the figures and tables to be based on [CODE LANGUAGE] output (png and tex), so it is critical you run the code first and then be sure to have it inserted well.

Always be aware of labeling issues with Tikz and graphics from ggplot. You can often easily miss the mislabeling positioning because it will not show up as compile overfull etc errors. They are more often due to restrictions you placed inadvertently on positions and coordinate placements being wrong.

Have a third agent check only the graphics for those problems including numerical accuracy.

Then compile a third and last time.
```

---

## What This Prompt Does

### 1. Design Phase
Creates an original Beamer theme rather than using defaults. The aesthetic should be:
- Professional but distinctive
- Consistent color palette
- Clean typography
- Appropriate for the audience

### 2. Rhetoric Restructuring
Takes existing content and applies the principles from `rhetoric_of_decks.md`:
- One idea per slide
- Titles as assertions
- Pyramid principle (conclusion first)
- Optimal cognitive load distribution

### 3. Code Integration
- Embeds executable code in slides
- Creates standalone scripts for walkthroughs
- Runs code FIRST to generate figures
- Inserts outputs (PNG, tex tables) into slides

### 4. Multi-Agent Review Process

**Agent 1 (Builder):** Creates the deck

**Agent 2 (Rhetoric Reviewer):** Evaluates:
- Narrative flow
- Cognitive density balance
- Technical rigor maintained
- Pedagogical consistency

**Agent 3 (Graphics Reviewer):** Checks:
- Tikz positioning errors
- ggplot label placement
- Numerical accuracy in figures
- Coordinate/position restrictions

### 5. Compilation Discipline
Three compilation passes:
1. Initial compile
2. Fix ALL overfull/underfull/vbox/hbox warnings (no matter how small)
3. Final compile after agent reviews

## Customization Tips

### For Different Audiences

**Undergraduates:**
```
...professional for an undergraduate course on [SUBJECT].
The students are mostly [YEAR] majors in [FIELD],
many are commuter students with jobs,
and approximately [X]% have prior exposure to [PREREQUISITE].
```

**PhD Students:**
```
...professional for a PhD seminar in [FIELD].
Assume strong mathematical background but varying exposure to [METHOD].
Emphasize intuition alongside formal results.
```

**Conference Presentation:**
```
...professional for a 20-minute conference presentation.
The audience is academic economists familiar with [BROAD AREA]
but not specialists in [YOUR SPECIFIC TOPIC].
Emphasize the identification strategy and key results.
```

### For Different Code Languages

**Stata:**
```
I want Stata do-files embedded in the decks...
figures based on Stata graph export (png)...
```

**Python:**
```
I want Python scripts embedded in the decks...
figures based on matplotlib/seaborn output (png)...
```

### If You Have Student Data

```
Before designing, please review the attached class roster [roster.pdf]
which contains student majors and years.
Tailor the rhetoric to this specific audience composition.
```

## Why This Works

The prompt succeeds because it:

1. **Specifies aesthetics AND function** - "beautiful" but also "professional" and "technically rigorous"

2. **Names the enemy explicitly** - "not overloaded at the slide level, but distributed and balanced"

3. **Demands code-first workflow** - run code → generate figures → insert (not the reverse)

4. **Builds in adversarial review** - second and third agents catch what the first missed

5. **Treats warnings as errors** - "no matter how small" forces Claude to fix LaTeX warnings that humans ignore

6. **Calls out the silent failures** - Tikz/ggplot positioning issues don't throw errors but ruin slides

## Example Output Structure

After running this prompt, you should have:

```
lecture_01/
├── lecture_01.tex          # Main Beamer file
├── lecture_01.pdf          # Compiled deck
├── beamertheme_custom.sty  # Original theme
├── scripts/
│   ├── figure_1.R          # Standalone script
│   ├── figure_2.R
│   └── table_1.R
├── figures/
│   ├── figure_1.png
│   └── figure_2.png
└── tables/
    └── table_1.tex
```

---

*This prompt was developed through iterative refinement across multiple teaching and research presentation projects. The multi-agent review process catches errors that single-pass generation misses.*
