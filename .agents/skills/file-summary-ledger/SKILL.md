---
name: file-summary-ledger
description: Maintain a compact 25-line-or-less file summary and change ledger at the top of source files, especially Python files, so future agents understand purpose, contracts, invariants, and recent meaningful edits.
license: MIT
metadata:
  audience: ai-agents
  applies_to: source-files
  languages:
    - python
---

# File Summary Ledger

## Purpose

Use this skill to maintain a compact file-level summary block at the top of source files. The block explains what the file currently does and gives AI agents a small ledger for tracking meaningful changes made to that file.

## Hard Limit

The summary ledger block must never exceed 25 physical lines total.

The 25-line count includes:

- start marker
- end marker
- blank comment lines
- summary lines
- change ledger lines

If the block would exceed 25 lines, remove or compress the oldest change entries first.

## When to Use

Use this skill when creating, editing, reviewing, or refactoring source files where future agents would benefit from durable file-level context.

Prefer using this for:

- Python files
- worker modules
- service modules
- scheduler files
- database access files
- files with important invariants
- files likely to be edited repeatedly by AI agents

Do not use this for:

- generated files
- lockfiles
- vendored code
- minified files
- one-off temporary files
- migration files unless explicitly useful

## Python Format

For Python, use line comments, not triple-quoted strings.

Use this format near the top of the file:

```python
# *** FILE SUMMARY LEDGER ***
# Purpose: <one-line purpose of this file>
# Main entry points: <functions/classes/CLI/hooks>
# Key data/contracts: <inputs, outputs, schemas, assumptions>
# Side effects: <db/files/network/env/logging/etc.>
# Important dependencies: <internal modules or external packages>
# Invariants: <rules that must stay true>
# Tests/verification: <how this file should be tested>
# Change ledger:
# - YYYY-MM-DD: <meaningful change made and why/result>
# Notes: <one concise warning, TODO, or operational caveat>
# *** END FILE SUMMARY LEDGER ***