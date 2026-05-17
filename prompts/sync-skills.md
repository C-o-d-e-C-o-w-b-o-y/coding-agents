Update this repository to the latest shared `coding-agents` state.

Steps:

1. Find the `coding-agents` CLI. Prefer `.agent-config/bin/coding-agents`, then `coding-agents` on PATH, then `../coding-agents/bin/coding-agents`.
2. Run the real managed update flow for the current repo with `coding-agents update <repo>`.
3. Verify the result with `coding-agents doctor <repo>`.
4. Report what changed:
   - shared skills synced
   - whether `AGENTS.md` was regenerated
   - whether repo-specific instructions live in `agents.local.md`
   - whether `CLAUDE.md` remained a regular file or became a symlink
5. If new skills were added, remind the user to restart the agent app.

Do not manually copy files unless the CLI is unavailable and the user explicitly asks for a fallback.
