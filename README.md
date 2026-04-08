# HREVN Anthropic Skills

**Un solo núcleo. Tres superficies. Mismo resultado verificable.**

This repo is the Anthropic-facing HREVN surface: three skills plus a local runner that bridges to the live HREVN managed runtime.

## Why HREVN

AI agents and multi-step workflows fail in ambiguous ways. When a sequence is
interrupted, neither the user nor the system can always determine with
certainty what completed, what failed mid-execution, and where work can safely
resume. Without a verifiable record, context is reconstructed from memory or
chat history, wasting tokens, repeating work, and leaving no reliable trail.

HREVN adds a structured evidence layer: baseline checks before consequential
steps, tamper-evident receipts after execution, and manifests that allow
workflows to continue from the last verified point rather than restarting from
scratch.

For teams operating in regulated or high-stakes environments, HREVN also
supports evidentiary discipline: structured records of what ran, under what
authority, and when it stopped. This is particularly relevant for AI systems
that may fall within EU regulatory timelines in 2026 and beyond. HREVN does
not make a system legally compliant, but it provides structured, verifiable
evidence that compliance, audit, and governance processes can use.

In Anthropic-facing workflows, HREVN extends the skill layer with structured
records of what ran, under what authority, and where execution can safely
resume through the runner bridge to the managed runtime.

## What it is
- an Anthropic-facing skill repo
- a thin public surface
- a local runner bridge to `https://api.hrevn.com`
- a clean base for a later MCP iteration

## What it is not yet
- not a native remote-skill marketplace package
- not a finished MCP package
- not the private HREVN runtime
- not the private commercial toolkit

## Skill chain
1. `hrevn-baseline-check`
2. `hrevn-sign-on-complete`
3. `hrevn-verify-bundle`

## Quick Start

```bash
export HREVN_API_KEY="replace-me"
python3 scripts/hrevn_anthropic_runner.py baseline-check \
  --input examples/baseline_check_request.json
```

The command above should return a `BaselineResult` JSON.

## Test in Claude Code

1. Open Claude Code in this repository.
2. Make sure `HREVN_API_KEY` is exported in the shell environment Claude Code will use.
3. First verify the runner directly:

```bash
python3 scripts/hrevn_anthropic_runner.py baseline-check \
  --input examples/baseline_check_request.json
```

4. Then ask Claude Code:

> Run a baseline check on `examples/baseline_check_request.json`

The expected path is:

```text
skill instructions -> local runner -> https://api.hrevn.com
```

## What is already proven in this repo
- the local runner can call the live managed API
- the baseline-check example returns a real `BaselineResult`
- the current path is usable today without waiting for MCP

## Included
- `.claude/skills/...`
- `docs/MANAGED_API_USAGE.md`
- `scripts/hrevn_anthropic_runner.py`
- `examples/baseline_check_request.json`

## Managed Runtime Bridge
The live managed endpoint is:
- `https://api.hrevn.com`

Current path:
- skill guidance now
- local runner bridge now
- MCP later

## Current status
This is a public Anthropic surface candidate with a real testing path today.
It is intentionally honest about the current runner-first runtime model.

## Rule
The skills guide behavior, but the runtime truth stays in the managed API and private HREVN core.
The skill itself does not natively perform remote HTTPS on its own.
