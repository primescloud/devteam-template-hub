# AGENTS.md

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:

- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them - don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:

- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it - don't delete it.

When your changes create orphans:

- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:

- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, and clarifying questions come before implementation rather than after mistakes.

## Where things live

This is a **hub repository** — the coordination surface for one project. It holds documents and
design artifacts, never product code.

| What | Where |
| --- | --- |
| Domain vocabulary | `CONTEXT.md` — created lazily by `/domain-modeling`; don't stub it |
| Architecture decisions | `docs/adr/` — same, written when a decision is actually made |
| Research notes, every claim cited | `docs/research/` |
| What a release must achieve, and why it was cut that way | the **milestone description** on GitHub — not a document |
| What this round builds — scope, acceptance criteria | the **issue body**, prose is fine |
| Which roles a ticket passes through | the issue's **front-matter** |

Three rules follow from that table:

- **Link documents, never copy them.** An issue references the spec; it does not restate it. Two
  copies are two truths.
- **Documents record criteria, never progress.** Whether something is done lives in GitHub —
  milestone counts, `sub_issues_summary`. A document that also tracks progress gets read back stale
  by the very agent that wrote it.
- **No product code here.** Design artifacts (UI html/js) are fine: they build nothing, ship
  nothing, and never reach production.

## Agent skills

### Issue tracker

Issues are tracked in this repo's GitHub Issues, managed via the `gh` CLI. See `docs/agents/issue-tracker.md`.

### Triage labels

The five canonical triage roles map onto this repo's label strings — one of them differs from the skill's default. See `docs/agents/triage-labels.md`.

### Domain docs

Single-context: `CONTEXT.md` + `docs/adr/` at the repo root. See `docs/agents/domain.md`.
