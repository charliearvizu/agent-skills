# Install / consume skills

Skills are authored once in `.agents/skills/<name>/SKILL.md` and consumed by any
harness that implements the [Agent Skills](https://agentskills.io) standard.

## opencode — no setup

opencode discovers `.agents/skills/*/SKILL.md` in the project (walking up to the
repo root) natively. Just open this repo (or one that contains it) and the
skills are available to the `skill` tool.

Optional: load skills from a non-default location or a remote URL via
`skills.paths` / `skills.urls` in `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "skills": {
    "paths": [".agents/skills"],
    "urls": ["https://example.com/.well-known/skills/"]
  }
}
```

## Codex — no setup

Codex scans `.agents/skills` from the current directory up to the repo root.
Open this repo and run `codex`; invoke a skill with `$name` or let Codex match
it implicitly.

## Claude Code — one-line mirror

Claude Code reads `.claude/skills/<name>/SKILL.md` (not `.agents/`). Mirror a
skill with a symlink (Unix) or a copy (Windows):

```bash
# Unix
mkdir -p .claude/skills
ln -s ../../.agents/skills/file-summary-ledger .claude/skills/file-summary-ledger
```

```powershell
# Windows PowerShell (copy, since symlinks may need elevated permissions)
New-Item -ItemType Directory -Force .claude/skills | Out-Null
Copy-Item -Recurse .agents/skills/file-summary-ledger .claude/skills/
```

> These `.claude/` artifacts are local/consumer-side and are gitignored — do not
> commit them back to this collection.

Claude Code follows symlinks, so a symlinked skill stays in sync with the
canonical `.agents/skills/` copy automatically.

## Use the whole collection elsewhere

- **Clone into another project** and point your harness at it, or symlink the
  skills you want into the target project's `.agents/skills/`.
- **Git submodule** this repo, then symlink selected skills into
  `.agents/skills/` (opencode/Codex) or `.claude/skills/` (Claude Code).
- **Personal/global use**: copy or symlink skills into `~/.agents/skills/`
  (opencode + Codex) or `~/.claude/skills/` (Claude Code).

## Optional: project memory

This repo ships `AGENTS.md` (read natively by opencode + Codex). For Claude Code
to pick up the same project memory:

```bash
ln -s AGENTS.md CLAUDE.md
```
