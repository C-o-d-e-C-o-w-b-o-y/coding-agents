---
name: dirty-commit
description: Split a dirty working tree into logical concerns and make focused commits until the tree is clean.
disable-model-invocation: true
---

Turn a dirty working tree into a sequence of focused git commits.

Use this when the user asks to review many uncommitted changes, separate them into logical concerns, and commit everything so the working tree is clean.

Core goal:

- Understand every uncommitted change before staging it.
- Group changes by user-facing or implementation concern, not by file extension or directory alone.
- Create as many commits as needed so each commit is coherent and reviewable.
- End with no unstaged, staged, or untracked changes unless the user explicitly asked to leave something out.

Workflow:

1. Inspect the repository state.
   - Run `git status --short --branch`.
   - Review tracked changes with `git diff`.
   - Review staged changes with `git diff --cached` if anything is already staged.
   - Inspect untracked files before deciding where they belong.
   - Use `git log --oneline -n 10` when recent commit style would help with message wording.

2. Identify logical concerns.
   - Build a short mental inventory of the distinct pieces of work present in the diff.
   - Treat generated files, lockfiles, migrations, tests, docs, and config changes as part of the same concern when they directly support it.
   - Split unrelated fixes, feature work, formatting churn, dependency updates, and documentation-only edits into separate commits.
   - If a file contains mixed concerns, inspect it carefully and stage only the relevant hunks for each commit.

3. Stage and commit one concern at a time.
   - Prefer staging whole files when a file belongs entirely to one concern.
   - Use patch staging only when a single file genuinely contains multiple unrelated concerns.
   - Before each commit, check `git diff --cached --stat` and `git diff --cached` to confirm the staged set is coherent.
   - Commit with a concise message that describes the concern, not the mechanics of staging.

4. Validate between commits.
   - After each commit, re-run `git status --short`.
   - Continue until all remaining changes are either committed or explicitly identified as intentionally left uncommitted.
   - Do not run tests unless the user asked for validation or the repo's commit workflow requires it.

5. Finish cleanly.
   - Run `git status --short --branch`.
   - Report the commits created, in order, with one-line messages.
   - Mention any files intentionally left uncommitted. If none, state that the working tree is clean.

Commit constraints:

- Do not create, switch, or rename branches unless the user explicitly asks.
- Do not push unless the user explicitly asks.
- Do not rewrite, amend, squash, reset, or otherwise alter existing commits unless the user explicitly asks.
- Do not add the coding agent as an author, co-author, or mention it in commit messages.
- Never use destructive cleanup commands such as `git reset --hard`, `git checkout --`, or `git clean` to make the tree clean.
