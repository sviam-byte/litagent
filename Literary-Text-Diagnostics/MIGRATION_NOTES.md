# Literary-Text-Diagnostics migration notes

## Target shape

`Literary-Text-Diagnostics/` is a single merged skill package:

- one root `Skill.md` with orchestration + output-mode policy
- one `resources/` directory with reusable branch and output references

## What is no longer needed as separate entities

For Claude-style skill packaging, the following should not be treated as independent runtime artifacts:

- `ORCHESTRATOR.md`
- `EXECUTION_GRAPH.md`
- `MODULE_CONTEXT_POLICY.md`
- standalone `skill_*.md` shards
- `prompt_wrappers/*`
- most `schemas/*`

## Why

These files are useful for internal multi-agent engineering, but too heavyweight for a single-skill runtime. In the merged shape, orchestration logic is embedded in `Skill.md` and (where needed) summarized in `resources/CORE_SYSTEM.md`.
