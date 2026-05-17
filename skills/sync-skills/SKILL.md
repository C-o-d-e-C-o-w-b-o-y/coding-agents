---
name: sync-skills
description: Update coding-agents from GitHub and sync the latest shared skills and base instructions into the current repo. Use when the user asks to sync skills, update coding-agents, refresh agent instructions, or explicitly invokes /sync-skills.
disable-model-invocation: true
---

Update the current repository to the latest shared `coding-agents` state by running the real CLI flow.

Workflow:

1. Find the `coding-agents` CLI.
   Prefer these locations in order:
   - `.agent-config/bin/coding-agents` from the current repo root
   - `coding-agents` on `PATH`
   - `../coding-agents/bin/coding-agents` relative to the current repo

2. Run the managed update flow for the current repo.
   - Use `.../bin/coding-agents update <current-repo>`
   - Do not manually copy skills unless the CLI is unavailable and the user explicitly asks for a fallback

3. Explain what the flow does.
   - Pulls the latest `coding-agents` changes from GitHub with `git pull --ff-only`
   - Symlinks shared skills into `.agents/skills/` and `.claude/skills/`
   - Regenerates `AGENTS.md` from shared base rules plus `agents.local.md`
   - Preserves repo-specific instructions in `agents.local.md`

4. Verify and report the resulting state.
   - Run `.../bin/coding-agents doctor <current-repo>`
   - Mention whether `CLAUDE.md` is a symlink or an existing regular file left in place
   - Tell the user to restart the agent app if brand-new skills were added

Notes:

- `AGENTS.md` is managed output. Do not hand-edit it after sync.
- `agents.local.md` is the repo-local layer. Edit that file for project-specific additions.
- On first adoption into a repo that already had a hand-written `AGENTS.md`, the sync should migrate the old repo-specific content into `agents.local.md` before regenerating `AGENTS.md`.
