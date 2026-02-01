# Claude Tools

> **What's in this folder:** Templates for giving Claude Code persistent memory across sessions.

---

## Contents

### `CLAUDE.md` — Project Context Template

**What it is:** A template you copy into each research project to give Claude persistent memory.

**How to use it:**
```bash
# Copy to your project root
cp CLAUDE.md /path/to/your/project/

# Edit with your project specifics
# Claude Code will automatically read it every session
```

**What goes in it:**
- Project description and research question
- Collaborator names (so Claude addresses them correctly)
- Key decisions you've made (so Claude doesn't re-suggest dropped ideas)
- Data sources, identification strategy, variable definitions
- Current status ("we're in the estimation phase")

**Why it matters:** Without this, every new Claude session starts from zero. You waste time re-explaining context. Worse, Claude might suggest things you've already tried and rejected.

---

## Philosophy

This template exists because:

1. **Context gets lost** — without `CLAUDE.md`, every session starts fresh
2. **Decisions need documentation** — "we dropped X because Y" prevents circular discussions
3. **Collaborator names matter** — Claude should address Scott as Scott, not "the user"
4. **"Design before results"** — keep Claude focused on whether the design is correct, not whether we like the numbers

---

## Related Tools

Looking for adversarial review? See `personas/referee2.md` — that's a separate persona for code review, not a Claude configuration template.
