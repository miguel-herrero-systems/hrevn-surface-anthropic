# HREVN Anthropic -> Managed API

## Goal

Connect the Claude Code surface to the same HREVN managed runtime used by the
other public surfaces.

## Current path

- skills-first Anthropic surface
- installable local runner for first validation
- managed API as runtime bridge
- MCP as the preferred Anthropic-facing discovery path

## Required environment

```bash
export HREVN_API_BASE_URL="https://api.hrevn.com"
export HREVN_API_KEY="replace-me"
```

Public managed endpoint:

- `https://api.hrevn.com`

## Installable runner

Recommended:

```bash
pipx install hrevn-anthropic-runner
hrevn-anthropic health-check
hrevn-anthropic self-test
hrevn-anthropic baseline
```

Repo-local fallback:

```bash
git clone https://github.com/miguel-herrero-systems/hrevn-surface-anthropic
cd hrevn-surface-anthropic
pipx install .
```

## First useful call

### Baseline check

`POST /v1/baseline-check`

Example:

```bash
hrevn-anthropic baseline-check --input examples/baseline_check_request.json
```

## Bundle operations

- `POST /v1/generate-bundle`
- `POST /v1/verify-bundle`
- `GET /v1/bundles/{bundle_id}/download`

## Rule

The Anthropic surface should not reimplement HREVN semantics locally.
It should call the managed runtime and present the result cleanly inside Claude
Code and companion skill flows.
