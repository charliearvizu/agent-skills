# agent-skills

A harness-agnostic collection of [Agent Skills](https://agentskills.io) — reusable, version-controlled instructions that give any compatible AI coding agent (opencode, Claude Code, Codex, and 40+ others) new capabilities and workflows.

Each skill is a folder containing a `SKILL.md` file with YAML frontmatter (`name` + `description`) and markdown instructions. Skills are loaded on demand via progressive disclosure: the agent sees only the name/description until a task matches, then reads the full file.

## Layout

```
.agents/skills/<name>/SKILL.md   # canonical skills (the cross-harness standard path)
docs/                            # authoring guide, harness matrix, install instructions
```

Skills live under `.agents/skills/` because that path is discovered **natively, with zero configuration**, by opencode and Codex. Claude Code reads the same `SKILL.md` format; only its discovery path differs (see [docs/INSTALL.md](docs/INSTALL.md)).

## Use a skill

| Harness | How |
| --- | --- |
| **opencode** | Already discovers `.agents/skills/` in this repo. No setup. |
| **Codex** | Already discovers `.agents/skills/` up to the repo root. No setup. |
| **Claude Code** | One-liner to mirror a skill into `.claude/skills/`. See [INSTALL.md](docs/INSTALL.md). |

## Documentation

- [Authoring a portable skill](docs/AUTHORING.md)
- [Harness support matrix](docs/HARNESS-MATRIX.md)
- [Install / consume in each harness](docs/INSTALL.md)

## License

MIT — see [LICENSE](LICENSE). Individual skills declare their own `license` in frontmatter.
