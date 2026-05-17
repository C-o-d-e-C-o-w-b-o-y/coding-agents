---
name: commit
description: Make a git commit for the work completed in this session. Only use when explicitly invoked
disable-model-invocation: true
---

Create exactly one git commit for the work completed in this session.

Before committing:

- Inspect the current repository state with git status and the diff to understand what will be committed.
- Include files that were modified as part of this session.
- Do not split individual files into partial hunks; if a file should be committed, commit the whole file.
- If a file contains both this session's changes and changes from another parallel agent, it is acceptable to commit the whole file rather than trying to separate them.
- Do not rewrite, amend, squash, or overwrite any commits that already exist.
- Do not run any tests or other validation steps.

Commit message:

- Write a concise message that describes only the changes being committed now.
- If earlier commits were already made during this session, describe only the delta since the most recent commit.

Constraints:

- Do not create a branch.
- Do not push.
- Do not open a pull request.
- Do not add the coding agent as an author, co-author, or mention it in the commit message.
