# HREVN Anthropic -> Managed API

## Goal
Keep the Anthropic-facing skill repo thin and connect real execution to the HREVN managed runtime.

## Current runtime reality
- the skill itself is instructional
- direct HTTPS does not happen "inside" the skill automatically
- serious execution path will be:
  - managed API first
  - MCP bridge later

## Shared backend
Use the same VPS-backed endpoints as the other HREVN surfaces.

Public managed endpoint:
- `https://api.hrevn.com`

## Minimal contract to expose in docs/examples
- `POST /v1/baseline-check`
- `POST /v1/generate-bundle`
- `POST /v1/verify-bundle`

## Anthropic-specific guidance
The skill should make clear:
- what call should happen first
- what structured output shape to expect
- that the backend is the source of truth

Minimal bridge shape today:

```text
skill instructions -> local runner or MCP bridge -> https://api.hrevn.com
```

This surface now includes a local runner:
- `scripts/hrevn_anthropic_runner.py`

Minimal usage:

```bash
export HREVN_API_KEY="replace-me"
python3 scripts/hrevn_anthropic_runner.py baseline-check \
  --input examples/baseline_check_request.json
```

Recommended first test:

1. run the command above directly
2. open Claude Code in this repo
3. ask:

```text
Run a baseline check on examples/baseline_check_request.json
```

The skill should not embed HREVN business logic in prompt text.
