Update this repository to the latest shared `coding-agents` state.

Steps:

1. Run the real managed update flow for the current repo with `.agent-config/bin/coding-agents update <repo>`.
2. Verify the result with `.agent-config/bin/coding-agents doctor <repo>`.
3. If `.agent-config/bin/coding-agents` is unavailable, stop and say that the repo needs initial coding-agents setup first.
4. Report what changed:
   - shared skills synced
   - whether `.agent-config/bin/coding-agents` is present
   - whether `AGENTS.md` was regenerated
   - whether repo-specific instructions live in `agents.local.md`
   - whether `CLAUDE.md` remained a regular file or became a symlink
5. If new skills were added, remind the user to restart the agent app.

Do not manually copy files unless the CLI is unavailable and the user explicitly asks for a fallback.
