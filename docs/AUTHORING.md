# Authoring a portable skill

A skill is a folder containing a `SKILL.md`. To stay portable across every
harness that implements the [Agent Skills](https://agentskills.io) standard
(opencode, Claude Code, Codex, and many others), follow these rules.

## Folder & file

- Put the skill at `.agents/skills/<name>/SKILL.md`.
- The folder name **must equal** the `name` in the frontmatter.
- `name`: lowercase, hyphen-separated, 1–64 chars, matching
  `^[a-z0-9]+(-[a-z0-9]+)*$`. No leading/trailing or consecutive hyphens.
- One `SKILL.md` per folder. Supporting files (scripts, references, templates)
  may sit alongside it and be referenced from the body.

## Frontmatter (the portable core)

```yaml
---
name: my-skill
description: One sentence covering WHAT it does and WHEN to trigger it.
license: MIT
metadata:
  audience: ai-agents
  applies_to: source-files
---
```

- `name` — required.
- `description` — required. Front-load literal trigger keywords and filenames
  the user is likely to say. Write in third person ("Use when…", not "I help…").
  Keep under ~1024 characters (opencode's hard limit; other harnesses truncate
  listings around 1500+ chars).
- `license` — optional.
- `metadata` — optional, a flat map of strings. Useful for categorization.

### Harness-specific fields — use sparingly

Harnesses silently **ignore** frontmatter fields they don't recognize, so you
*can* add fields like Claude Code's `allowed-tools`, `paths`, or
`disable-model-invocation`. But doing so bloats the file and only takes effect
in one harness. Prefer keeping shared skills to the portable core above. If a
skill genuinely needs harness-specific behavior, document it in `metadata`
rather than scattering proprietary fields.

Do **not** set `compatibility: <single-harness>` — it falsely narrows a shared
skill to one tool.

## Body

- Write instructions the agent follows when the skill loads.
- State what to do, not how the harness works.
- Keep it focused on one job. Move large reference material into sibling files
  and link to them from `SKILL.md`.
- No code comments unless they're part of an example.

## Checklist before adding a skill

1. `SKILL.md` exists with valid `name` + `description`.
2. Folder name equals `name` and matches the regex above.
3. No harness-specific frontmatter unless intentionally scoped.
4. `description` clearly says when to trigger *and* when not to.
5. If scripts are bundled, they're referenced and documented in the body.
