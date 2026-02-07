---
name: newproject
description: Scaffold a new research project with standard structure and CLAUDE.md
allowed-tools: Bash(mkdir*), Bash(cp*), Write, Read
argument-hint: [project-name]
---

# New Project Scaffold

Create a new research project folder with Scott's standard structure.

## Usage

```
/newproject craigslist-media-bias
```

## What Gets Created

```
[project-name]/
├── CLAUDE.md           # Project-specific rules (from template)
├── README.md           # Project overview
├── code/
│   ├── R/
│   ├── stata/
│   └── python/
├── data/
│   ├── raw/            # Original source data (never modify)
│   └── clean/          # Cleaned/merged datasets
├── output/
│   ├── figures/
│   └── tables/
├── docs/
│   ├── manuscript/
│   └── references/
├── decks/              # Beamer presentations
├── misc/               # Miscellaneous files
└── log/                # Progress logs for session continuity
```

## Steps

1. **Get the project name**
   - From argument, or ask user
   - Convert spaces to hyphens if needed

2. **Determine location**
   - Default: current directory
   - Ask user to confirm if unclear

3. **Create directory structure**
   ```bash
   mkdir -p [project-name]/{code/{R,stata,python},data/{raw,clean},output/{figures,tables},docs/{manuscript,references},decks,misc,log}
   ```

4. **Create CLAUDE.md from template**

   Copy the template from `~/mixtapetools/claude/CLAUDE.md` and update:
   - Replace `[Your Name]` with `Scott`
   - Update project overview section with project name

5. **Create README.md**

   ```markdown
   # [Project Name]

   ## Overview

   [To be filled in]

   ## Collaborators

   - Scott Cunningham

   ## Status

   Phase: Setup

   ## Key Files

   - Analysis: `code/`
   - Data: `data/`
   - Output: `output/`
   - Paper: `docs/manuscript/`
   - Presentations: `decks/`
   ```

6. **Create initial log entry**

   Create `log/YYYY-MM-DD_setup.md`:

   ```markdown
   # Project Log

   ## [Today's Date] - Project Created

   Initial project setup. Directory structure created.

   Next steps:
   - [ ] Define research question
   - [ ] Identify data sources
   - [ ] Update CLAUDE.md with project details
   ```

7. **Report success**
   - Show the created structure using `ls -la`
   - Remind user to update CLAUDE.md with project-specific details
   - Suggest opening the project folder

## Example

```
User: /newproject texas-fertility-study

Claude: Created project structure at ./texas-fertility-study/

texas-fertility-study/
├── CLAUDE.md
├── README.md
├── code/
│   ├── R/
│   ├── stata/
│   └── python/
├── data/
│   ├── raw/
│   └── clean/
├── output/
│   ├── figures/
│   └── tables/
├── docs/
│   ├── manuscript/
│   └── references/
├── decks/
├── misc/
└── log/
    └── 2026-02-07_setup.md

Next steps:
1. Update CLAUDE.md with your research question and identification strategy
2. Add collaborator information
3. Place raw data files in data/raw/
```
