---
name: subagent-review
description: "Review the work just completed in the current thread by spawning two subagents for independent, unbiased code review: one general reviewer and one architecture/clean-patterns reviewer. Use when the user asks for a subagent review, independent review, second-pass review, adversarial review, or review of the current session's changes."
---

Run an independent review of the current thread's completed work by spawning two subagents.

If two subagents are not available, say so clearly. Do not pretend the review is independent.

Workflow:

1. Determine the review scope from this conversation, recent tool activity, commits/files changed in this thread, and the user's request.
   - Choose the narrowest scope that represents the completed work.
   - Do not assume the whole working tree belongs to this thread.
   - If scope is ambiguous, state your chosen scope or ask before continuing.

2. Spawn two read-only subagents with neutral prompts.
   - Subagent 1: general code review.
   - Subagent 2: code architecture and clean patterns only.
   - Do not include your reasoning, suspected bugs, or desired outcome.
   - Tell both subagents not to edit, stage, commit, or push.

Suggested prompt for subagent 1:

```text
You are a subagent performing an independent code review.

Repo: <absolute repo path>
Review scope: <files/commits/diff and why this is the current thread's work>
User focus: <focus or "general correctness review">

Do not modify files.

Review only for actionable issues:
- correctness or regressions
- edge cases and error handling
- security or privacy risks
- test gaps
- performance risks
- maintainability problems likely to cause bugs

Inspect surrounding context, not only changed lines.

For each finding, include severity, file/line, problem, evidence, and suggested fix.
If there are no actionable findings, say so.
```

Suggested prompt for subagent 2:

```text
You are a subagent performing an independent architecture and clean-patterns review.

Repo: <absolute repo path>
Review scope: <files/commits/diff and why this is the current thread's work>
User focus: <focus or "architecture and clean patterns only">

Do not modify files.

Review only for actionable architecture or clean-pattern issues:
- misplaced responsibilities or leaky abstractions
- inconsistent patterns versus nearby code
- unnecessary coupling or duplicated logic
- brittle boundaries, naming, or module structure
- complexity that is likely to cause future bugs

Ignore generic correctness, style, and test findings unless they expose an architecture problem.
Inspect surrounding context, not only changed lines.

For each finding, include severity, file/line, problem, evidence, and suggested fix.
If there are no actionable findings, say so.
```

3. Validate both subagents' findings yourself.
   - Re-open referenced code.
   - Drop false positives, speculation, duplicates, and unrelated pre-existing issues.
   - Merge overlapping findings, keeping the clearest version.

4. Report findings first, ordered by severity.
   - Include only confirmed actionable issues.
   - Include review scope and checks run.
   - If there are no findings, say that clearly and mention any remaining risk.
