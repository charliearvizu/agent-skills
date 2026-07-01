# AGENTS.md

This repo is a **harness-agnostic collection of Agent Skills** (see https://agentskills.io).
It is not an application — it contains no build, tests, or runtime. The only
artifacts are skill folders and documentation.

## Repo structure

- `.agents/skills/<name>/SKILL.md` — the canonical skills. **This is the only
  place skills are authored.** `.agents/skills/` is the cross-harness standard
  discovery path: opencode and Codex read it natively with zero configuration.
- `docs/` — authoring guide, harness support matrix, and per-harness install
  instructions.
- `AGENTS.md` (this file) — project memory for any agent working in the repo.
  Read natively by opencode and Codex. Claude Code users may symlink
  `CLAUDE.md` → `AGENTS.md`.

## Working in this repo

- To add or change a skill, edit files under `.agents/skills/<name>/` only.
  Never duplicate a skill into `.claude/skills/` or `.opencode/skills/` — those
  are local/consumer-side and are gitignored.
- A skill folder MUST contain exactly one `SKILL.md` with `name` and
  `description` frontmatter. The folder name must equal `name`.
- Keep frontmatter portable: `name`, `description`, optionally `license` and
  `metadata`. Do not add harness-specific fields (`allowed-tools`, `paths`, …)
  to a shared skill unless you accept that other harnesses will ignore them.
  See `docs/AUTHORING.md` for the rules.

## There is nothing to build, lint, or test

This is a content-only repository. Verification means confirming each skill's
frontmatter parses and its folder name matches its declared `name`. No test
framework or package manager is used.
