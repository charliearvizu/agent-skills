# Harness support matrix

All harnesses below implement the open [Agent Skills](https://agentskills.io)
standard: a folder with `SKILL.md` + YAML frontmatter (`name`, `description`).
The portable core frontmatter works everywhere; harness-specific fields are
ignored by the others.

## Discovery paths

| Scope | opencode | Claude Code | Codex |
| --- | --- | --- | --- |
| **Project (native)** | `.agents/skills/`, `.opencode/skills/`, `.claude/skills/` | `.claude/skills/` | `.agents/skills/` |
| Global / personal | `~/.agents/skills/`, `~/.claude/skills/`, `~/.config/opencode/skills/` | `~/.claude/skills/` | `~/.agents/skills/` |
| Walks up to repo root | yes | yes (nested `.claude/skills/`) | yes (`.agents/skills/`) |
| Follows symlinks | yes | yes | yes |

> **Why `.agents/skills/`?** It is the one path discovered natively, with zero
> configuration, by **both** opencode and Codex. Claude Code reads the identical
> `SKILL.md` format but looks under `.claude/skills/`, so it needs a one-line
> mirror (see [INSTALL.md](INSTALL.md)).

## Frontmatter support

| Field | opencode | Claude Code | Codex | Portable? |
| --- | --- | --- | --- | --- |
| `name` | required | optional (defaults to dir) | required | yes |
| `description` | required (1–1024 chars) | recommended (listing truncated ~1536) | required | yes |
| `license` | yes | ignored | ignored | yes |
| `metadata` | yes (string map) | ignored | ignored | yes |
| `compatibility` | yes (optional) | ignored | ignored | optional |
| `allowed-tools` | ignored | yes | ignored | Claude-only |
| `paths` | ignored | yes | ignored | Claude-only |
| `disable-model-invocation` | ignored | yes | ignored | Claude-only |
| `when_to_use` | ignored | yes | ignored | Claude-only |
| Codex `agents/openai.yaml` | n/a | n/a | optional sidecar | Codex-only |

Unknown fields are ignored by every harness, so adding a Claude-only field does
not break opencode/Codex — it simply has no effect there.

## Project memory (rules)

| Harness | File read natively |
| --- | --- |
| opencode | `AGENTS.md` (falls back to `CLAUDE.md`) |
| Codex | `AGENTS.md` |
| Claude Code | `CLAUDE.md` |

This repo authors `AGENTS.md` as the single source. Claude Code users can
symlink `CLAUDE.md` → `AGENTS.md`.

## Consumption options

See [INSTALL.md](INSTALL.md) for clone, git submodule, global install,
opencode `skills.urls`, and the Claude Code mirror one-liner.
