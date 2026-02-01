# Personas

> **What's in this folder:** Distinct personas for specialized review processes. These are not Claude tools—they're adversarial reviewers, critics, and challengers that require separate conversations.

---

## Why Personas Are Different

A **persona** is not a template or a skill. It's a distinct reviewer with its own perspective and concerns. The key insight:

**You cannot grade your own homework.**

If you ask the same Claude instance that wrote code to review that code, you're asking a student to grade their own exam. The "review" will rationalize the existing choices rather than challenge them.

True adversarial review requires:
1. A **separate conversation** (fresh context, no prior commitments)
2. A **distinct persona** (different concerns, different priorities)
3. **Formal output** (structured reports, not casual feedback)

---

## Contents

### `referee2.md` — The Adversarial Reviewer

**What it is:** A persona document that turns Claude into Referee 2—the skeptical, demanding reviewer who looks for everything you missed.

**How to use it:**
1. Finish your code/analysis in your main Claude session
2. **Open a completely new Claude conversation**
3. Paste the entire contents of `referee2.md`
4. Paste your code or analysis
5. Ask for a referee report
6. Take the report back to your original session
7. Address concerns (or document why you're not)
8. Repeat until Referee 2 accepts

**What Referee 2 looks for:**
- Race conditions, edge cases, off-by-one errors
- File I/O issues, encoding problems, path assumptions
- Statistical assumptions, identification concerns
- Logic gaps, unstated assumptions
- The things you forgot because you were too close to the code

**Output format:** A formal referee report with:
- Major concerns (must address before deployment)
- Minor concerns (should address, quality issues)
- Questions for authors (things that need clarification)
- Verdict: Accept / Minor revisions / Major revisions / Reject

---

## Philosophy

The personas in this folder exist because:

1. **AI makes confident mistakes** — Subtle bugs that compile, pass tests, but fail silently in production
2. **Creators can't see their own blind spots** — You rationalize your own choices
3. **Academic peer review works** — The R&R process catches real problems
4. **Adversarial thinking finds different bugs** — A hostile reviewer looks for weaknesses, not confirmation

---

## Creating New Personas

Consider creating personas for:

- **The Statistician** — Challenges identification, assumptions, inference
- **The User** — Tests from a user's perspective (what's confusing? what breaks?)
- **The Security Reviewer** — Looks for vulnerabilities, attack vectors, data exposure
- **The Performance Critic** — Challenges efficiency, scalability, resource usage

Each persona should have:
1. A clear perspective (what do they care about?)
2. Specific concerns (what do they look for?)
3. A structured output format (how do they report findings?)
4. Instructions for use (when and how to invoke them)

The key is that each persona asks different questions than you would naturally ask yourself.
