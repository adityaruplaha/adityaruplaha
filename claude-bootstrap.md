# Claude Code bootstrap

Point a fresh Claude Code session on a new machine at this file: "Follow https://github.com/adityaruplaha/adityaruplaha/blob/main/claude-bootstrap.md". Everything below is the instruction.

---

Set up my global Claude Code config on this machine from my two GitHub repos. Before you change anything, check what's already here and tell me.

Sources:

- git@github.com:adityaruplaha/my-claude-code-stuff.git → ~/.claude. It tracks CLAUDE.md, memory/ and skills/. Its .gitignore ignores everything by default, so transcripts, history.jsonl, settings.json, .credentials.json and the project auto-memories under projects/ are never in it. skills/synced/ and skills/.trash/ are Claude Code's own and are ignored too.
- git@github.com:adityaruplaha/my-claude-stuff.git → ~/Claude. This is layer 1: the memory/ and skills/ mirrors, README.md and the utilities.

Steps:

1. Check first and report:
   - whether ~/.claude, ~/.claude/.git, ~/Claude and ~/.agents/skills already exist. Syncthing replicates some of my trees, .git included, so a repo may already be here.
   - whether any project auto-memories already exist under ~/.claude/projects/*/memory/, and what settings.json already enables (plugins, marketplaces).
   - whether `ssh -T git@github.com` works.
   - whether git user.name and user.email are set globally.
   - whether uv and zotero-cli are installed.
   If SSH or the git identity is missing, ask me. Don't work around it. Never set a git identity yourself.
2. ~/.claude already exists because Claude Code created it, so don't clone over it. Run `git init` in place, add the remote as origin, fetch, then `git checkout -b main --track origin/main`. If any tracked file already exists locally with different content, stop and show me the diff. Don't overwrite it.
3. If ~/Claude doesn't exist, clone my-claude-stuff into it. I'm authorising you to create it this once. After that, the CLAUDE.md rule applies: ~/Claude is read-only from Claude Code.
4. For every directory under ~/.claude/skills/ except `synced` and `session-cleanup` (session-cleanup is Claude-specific), create a relative symlink `~/.agents/skills/<name> -> ../../.claude/skills/<name>`. Hidden directories such as `.trash` are not skills. If something already exists at that path and isn't that exact symlink, report it. Don't replace it.
5. Project auto-memories aren't in the repo. Don't create or copy any under ~/.claude/projects/. They build up on each machine as I work there. If some are already here, report them and leave them alone.
6. Verify:
   - `git -C ~/.claude status` and `git -C ~/Claude status` are both clean.
   - Every link in ~/.agents/skills resolves.
   - A fresh `claude` session in ~ (`claude -p` is fine) reports CLAUDE.md loaded, and the skills citing-sources, material-ingest, memory-capped-runs, sensible-math-reference, session-cleanup, terminology-reference and zotero-cli are listed.

Rules:

- Read ~/.claude/CLAUDE.md and ~/Claude/memory/guardrails.md once they're in place, and follow them.
- Ask before installing anything (uv, gh, zotero-cli, plugins). Python is uv, never pip.
- No `rm -f` or `rm -r`. Deletes should fail loudly, and you should ask me before any delete.
- Don't copy settings.json, credentials or plugin state. Those are set per machine. The old machine enabled the cloudflare plugin from the cloudflare/skills marketplace, and whether to add it here is my call.
- Don't commit or push anything.

End with a short report: what you did, what you skipped, and what's waiting on me.
